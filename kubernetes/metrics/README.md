# Metrics



```ini
container_working_set_in_bytes = container_memory_usage_bytes - total_inactive_file
```

kubectl top 中内存用的是 container\_memory\_usage\_bytes ,oomkill 也是 看 container\_memory\_usage\_bytes 指标

```json
apiVersion: v1
data:
  config.yaml: |-
    "resourceRules":
      "cpu":
        "containerLabel": "container"
        "containerQuery": "sum(irate(container_cpu_usage_seconds_total{<<.LabelMatchers>>,container!=\"POD\",container!=\"\",pod!=\"\"}[5m])) by (<<.GroupBy>>)"
        "nodeQuery": "sum(1 - irate(node_cpu_seconds_total{mode=\"idle\"}[5m]) * on(namespace, pod) group_left(node) node_namespace_pod:kube_pod_info:{<<.LabelMatchers>>}) by (<<.GroupBy>>)"
        "resources":
          "overrides":
            "namespace":
              "resource": "namespace"
            "node":
              "resource": "node"
            "pod":
              "resource": "pod"
      "memory":
        "containerLabel": "container"
        "containerQuery": "sum(container_memory_working_set_bytes{<<.LabelMatchers>>,container!=\"POD\",container!=\"\",pod!=\"\"}) by (<<.GroupBy>>)"
        "nodeQuery": "sum(node_memory_MemTotal_bytes{job=\"node-exporter\",<<.LabelMatchers>>} - node_memory_MemAvailable_bytes{job=\"node-exporter\",<<.LabelMatchers>>}) by (<<.GroupBy>>)"
        "resources":
          "overrides":
            "instance":
              "resource": "node"
            "namespace":
              "resource": "namespace"
            "pod":
              "resource": "pod"
      "window": "5m"
kind: ConfigMap
metadata:
  name: adapter-config
  namespace: monitoring

```
