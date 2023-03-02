# 安装

### Centos7.7 or newer  &#x20;

```bash
yum install -y python3
```

### Centos7.6 or lower

```bash
yum install https://repo.ius.io/ius-release-el$(rpm -E '%{rhel}').rpm
yum update -y
yum install -y python3
```

### 安装虚拟环境库

```bash
pip3 install virtualenv
```

### 创建虚拟环境

```bash
virtualenv <envname>

python -m venv  <envname>

```

### 激活当前目录的虚拟环境

```bash
./Scripts/activate
```

### 退出虚拟环境

```bash
deactivate 
```

### 设置默认包地址为清华大学镜像地址

```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

### pip 生成requirements

```bash
pip freeze > ./requirements.txt 
```

### pip 根据清单安装

pip install -r ./requirements.txt
