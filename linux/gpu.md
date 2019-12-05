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
```

