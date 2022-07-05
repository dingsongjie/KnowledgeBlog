# JsonNode.Parse(ref reader) create large byte\[] object in .NET6

* 起因

该方法内部通过生成JsonDocument，并使用RootElement 来生成 JsonNode。在生成JsonDocument的时候

```csharp
bool flag = JsonDocument.TryParseValue(ref reader, out document, shouldThrow: true, useArrayPools: false);
```

默认不使用ArrayPools

```csharp
            if (useArrayPools)
            {
                byte[] array = ArrayPool<byte>.Shared.Rent(num4);
                Span<byte> destination = MemoryExtensions.AsSpan(array, 0, num4);
                try
                {
                    if (readOnlySpan.IsEmpty)
                    {
                        sequence.CopyTo(destination);
                    }
                    else
                    {
                        readOnlySpan.CopyTo(destination);
                    }

                    document = Parse(MemoryExtensions.AsMemory(array, 0, num4), currentState.Options, array);
                }
                catch
                {
                    destination.Clear();
                    ArrayPool<byte>.Shared.Return(array);
                    throw;
                }
            }
            else
            {
                byte[] array2 = (!readOnlySpan.IsEmpty) ? readOnlySpan.ToArray() : sequence.ToArray();
                document = ParseUnrented(array2, currentState.Options, reader.TokenType);
            }
```

如果这个数组超过85000字节，会生成大对象。

* 解决方法

生成 JsonDcoument,并通过RootElement**生成**JsonNode，最后dispose JsonDcoument 对象

```csharp
                using (var jsonDocument = System.Text.Json.JsonSerializer.Deserialize<JsonDocument>(ref reader))
                {
                    return jsonDocument.RootElement.ToJsonNodeForLessAllocation() as JsonObject;
                }
```

```csharp
public static class JsonElementExtensions
    {
        public static JsonNode ToJsonNodeForLessAllocation(this JsonElement jsonElement)
        {
            if (jsonElement.ValueKind == JsonValueKind.Array)
            {
                var jsonArray = GetJsonArray(jsonElement);
                return jsonArray;
            }
            else if (jsonElement.ValueKind == JsonValueKind.Object)
            {
                var jsonObject = GetJsonObject(jsonElement);
                return jsonObject;
            }
            else
            {
                return jsonElement.Deserialize<JsonNode>();
            }
        }

        private static JsonArray GetJsonArray(JsonElement jsonElement)
        {
            var array = new JsonArray();
            foreach (var item in jsonElement.EnumerateArray())
            {
                var node = item.ToJsonNodeForLessAllocation();
                array.Add(node);
            }
            return array;
        }
        private static JsonObject GetJsonObject(JsonElement jsonElement)
        {
            Dictionary<string, JsonNode?> keyValuePairs = new Dictionary<string, JsonNode?>();
            foreach (var item in jsonElement.EnumerateObject())
            {
                var jsonNode = item.Value.ToJsonNodeForLessAllocation();
                keyValuePairs.Add(item.Name, jsonNode);
            }
            return new JsonObject(keyValuePairs);
        }
    }
```
