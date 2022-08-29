# Dotnet dump



#### Dotnet dump

```bash
dotnet tool install --global dotnet-dump \
&& export PATH=$PATH:$HOME/.dotnet/tools
```

#### Collect

```bash
dotnet-dump collect -p 1 --type Full -o core1
```



#### Analyze

```bash
 dotnet-dump analyze  core1
```

analyze 里名的命令通过 help 查找 使用方式，help, help command
