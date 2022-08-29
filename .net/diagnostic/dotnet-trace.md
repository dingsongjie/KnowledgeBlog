# Dotnet trace



#### Dotnet counter

```bash
dotnet tool install --global dotnet-trace \
&& export PATH=$PATH:$HOME/.dotnet/tools
```

#### Collect

```bash
dotnet-trace collect -p 1 --providers Microsoft-Windows-DotNETRuntime --output trace.nettrace
```
