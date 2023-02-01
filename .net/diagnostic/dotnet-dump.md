# Dotnet dump



#### Collect dumps on crash <a href="#collect-dumps-on-crash" id="collect-dumps-on-crash"></a>

<pre class="language-bash"><code class="lang-bash">export COMPlus_DbgEnableMiniDump 1
export COMPlus_DbgMiniDumpType 4 

<strong># .net 7 
</strong>export DOTNET_DbgEnableMiniDump 1
export DOTNET_DbgEnableMiniDump 4 
</code></pre>

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
