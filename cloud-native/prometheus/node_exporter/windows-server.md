# windows-server

### 文档地址

&#x20;[https://github.com/prometheus-community/windows\_exporter](https://github.com/prometheus-community/windows\_exporter)



### 配合grafana启动命令

```powershell
ps1msiexec /i windows_exporter-0.19.0-386.msi ENABLED_COLLECTORS="ad,adfs,cache,cpu,cpu_info,cs,container,dfsr,dhcp,dns,fsrmquota,iis,logical_disk,logon,memory,msmq,mssql,netframework_clrexceptions,netframework_clrinterop,netframework_clrjit,netframework_clrloading,netframework_clrlocksandthreads,netframework_clrmemory,netframework_clrremoting,netframework_clrsecurity,net,os,process,remote_fx,service,tcp,time,vmware" LISTEN_PORT="9182"
```
