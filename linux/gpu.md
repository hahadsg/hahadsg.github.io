## GPU envs install

### apt-get (ubuntu)

```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-390
sudo apt install nvidia-cuda-toolkit
sudo reboot
```

### yum (centos)

```bash
# 添加ELRepo源
sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm

# One must install kernel-devel and gcc kernel on a CentOS 7:
sudo yum group install "Development Tools"
sudo yum -y install gcc kernel-devel kernel-headers

# You must install dkms for registering the NVIDA kernel module with DKMS:
sudo yum -y install epel-release
sudo yum -y install dkms

sudo yum -y install nvidia-detect

# 检查显卡型号
nvidia-detect -v

# 根据显卡型号安装驱动，下面这个是最新的
sudo yum -y install kmod-nvidia

# 重启
sudo reboot

# 安装CUDA9.0（注意tensorflow1.x都是用CUDA9.0）
sudo yum remove "cuda*"
wget https://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/cuda-repo-rhel7-9.0.176-1.x86_64.rpm
sudo yum install cuda-9-0

# 安装cuDNN7.+
# 到这里链接下载CUDA9.0对应的cuDNN（对于centos三个lib都下载）
# https://developer.nvidia.com/rdp/cudnn-archive
sudo rpm -ivh libcudnn7-7.6.4.38-1.cuda9.0.x86_64.rpm
sudo rpm -ivh libcudnn7-devel-7.6.4.38-1.cuda9.0.x86_64.rpm
sudo rpm -ivh libcudnn7-doc-7.6.4.38-1.cuda9.0.x86_64.rpm
```

### 查询命令

* 显示nvidia情况

```bash
nvidia-smi
```

