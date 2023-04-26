# 磁盘-文件系统相关



### df&#x20;

查看文件系统和磁盘的使用

### du&#x20;

查看磁盘空间

### blkid

获取磁盘id

### fdisk

磁盘分区

### mkfs

格式化磁盘

### 分区

* 分区扩容 **parted \[dev]**
* **分区扩容** growpart \[dev] \[parteNumber]
* 分区更新 **partprobe**

### LVM

* 创建pv  **pvcreate**&#x20;
* 显示pv **pvdisplay**
* 创建vg **vgcreate**
* 显示vg **vgdisplay**
* vg扩容 **vgextend**
* 创建逻辑卷 **lvcreate**
* 显示逻辑卷 **lvdisplay**
* 逻辑卷扩容 **lvextend -l** +100%FREE

### XFS

* 操作系统扩容  **xfs\_growfs \[mounted]**

### **fsck**

**文件系统检查**

* 修复磁盘  fsck -f-y devName



