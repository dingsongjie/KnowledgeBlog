# fio

### 创建文件夹

```bash
TEST_DIR=/mnt/disks1/fiotest
mkdir -p $TEST_DIR
```

### 1M顺序并发写入测试

```bash
fio --name=write_throughput --directory=$TEST_DIR --numjobs=16 \--size=10G --time_based --runtime=60s --ramp_time=2s --ioengine=libaio \--direct=1 --verify=0 --bs=1M --iodepth=64 --rw=write \--group_reporting=1
```

### 4K随机写入测试

```bash
fio --name=write_iops --directory=$TEST_DIR --size=10G \--time_based --runtime=60s --ramp_time=2s --ioengine=libaio --direct=1 \--verify=0 --bs=4K --iodepth=256 --rw=randwrite --group_reporting=1
```

### 1M顺序并发读取测试

```bash
fio --name=read_throughput --directory=$TEST_DIR --numjobs=16 \--size=10G --time_based --runtime=60s --ramp_time=2s --ioengine=libaio \--direct=1 --verify=0 --bs=1M --iodepth=64 --rw=read \--group_reporting=1
```

### 4K随机写入测试

```bash
fio --name=read_iops --directory=$TEST_DIR --size=10G \--time_based --runtime=60s --ramp_time=2s --ioengine=libaio --direct=1 \--verify=0 --bs=4K --iodepth=256 --rw=randread --group_reporting=1
```

### 清理

```bash
rm $TEST_DIR/write* $TEST_DIR/read*
```
