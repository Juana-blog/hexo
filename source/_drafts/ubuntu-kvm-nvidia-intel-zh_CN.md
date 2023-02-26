---
abbrlink: KVM-nvidia-CN
categories:
- - ubuntu
- - KVM
- - Nvidia
date: '2023-02-26 17:42:39'
tags:
- ubuntu
- KVM
- Nvidia
title: ubuntu KVM I+N Nvidia独显直通
updated: Sun, 26 Feb 2023 10:19:55 GMT
---
# 注意事项

## 1.请确保你的bios支持pci直通（VT-D 虚拟化）

## 2.直通后 linux无法使用 CUDA

# 环境准备

## 1.[windows iso文件](https://www.microsoft.com/zh-cn/software-download/windows10) [windows中国境内分流](https://latest10.win/) , [viro驱动iso](https://github.com/virtio-win/virtio-win-pkg-scripts/blob/master/README.md)

## 2.一台搭载ubuntu的电脑 使用grub作为boot

# 开始安装

## 1.安装KVM

```
sudo apt-get update
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager
```

![image.png](https://s2.loli.net/2023/02/26/uzSdp5t3wb12Ji6.png)

## 2.设置libvirt

```
sudo systemctl start libvirtd
sudo systemctl enable libvirtd
```

# 3.给予用户管理kvm权限

```
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
```

# 4.开启iommu

## 查看是否开启了iommu

```
cat /proc/cmdline | grep iommu

```

```

sudo nano /etc/default/grub
```

在 `GRUB_CMDLINE_LINUX_DEFAULT` 的 =“” 内添加 `intel_iommu=on`

![image.png](https://s2.loli.net/2023/02/26/dqGXbwa21RlPscj.png)

添加完后按 `ctrl + x` 保存并退出

```
sudo update-grub
```

然后使用 `sudo reboot` 重启电脑
