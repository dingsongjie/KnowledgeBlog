# Dotnet stack



#### Dotnet stack

```bash
dotnet tool install --global dotnet-stack \
&& export PATH=$PATH:$HOME/.dotnet/tools
```

#### Collect

```bash
dotnet-stack report  --process-id 1 -n DiagnosticScenarios
```



#### Analyze

```bash
 dotnet-dump analyze  core1
```

analyze 里名的命令通过 help 查找 使用方式，help, help command
