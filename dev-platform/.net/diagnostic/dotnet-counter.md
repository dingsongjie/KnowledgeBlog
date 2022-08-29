---
description: dotnet counter 工具
---

# Dotnet counter

#### Dotnet counter

```bash
dotnet tool install --global dotnet-counters \
&& export PATH=$PATH:$HOME/.dotnet/tools
```

#### Monitor

```bash
dotnet-counters monitor -p 1 --refresh-interval 1
```
