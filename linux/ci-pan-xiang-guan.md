# 磁盘相关



### 分区

* 分区扩容 **parted \[dev]**
* 分区更新 **partprobe**

### LVM

* 创建pv  **pvcreate**
* 显示pv **pvdisplay**
* 创建vg **vgcreate**
* 显示vg **vgdisplay**
* vg扩容 **vgextend**
* 创建逻辑卷 **lvcreate**
* 显示逻辑卷 **lvdisplay**
* 逻辑卷扩容 **lvextend -l** +100%FREE

### XFS

* 操作系统扩容  **xfs\_growfs \[mounted]**

****
