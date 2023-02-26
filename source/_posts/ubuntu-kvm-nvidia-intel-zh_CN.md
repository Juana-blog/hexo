---
abbrlink: KVM-nvidia-CN
categories:
- - ubuntu
- - KVM
- - Nvidia
cover: https://s2.loli.net/2023/02/26/yjoYgdfcRX6QCJM.png
date: '2023-02-26 17:42:39'
tags:
- ubuntu
- KVM
- Nvidia
title: ubuntu KVM I+N Nvidia独显直通
updated: Sun, 26 Feb 2023 10:41:04 GMT
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
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager ovmf
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

![image.png](https://s2.loli.net/2023/02/26/vRDheJwtNLp7E4A.png)如像上图一样输出了，请执行下一步

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

# 5.宿主机解绑显卡

将nvidia驱动改为开源驱动

![image.png](https://s2.loli.net/2023/02/26/yVCBpN54ARDfbSx.png)

修改root密码: `sudo passwd root`

`su`

```
echo 'blacklist nouveau
blacklist snd_hda_intel' >> /etc/modprobe.d/blacklist.conf
```

![image.png](https://s2.loli.net/2023/02/26/pVbHm2cCz38irwQ.png)

重启系统 `sudo reboot`

# 安装系统并配置独显直通

打开 `virt-manager` 新建虚拟机

![image.png](https://s2.loli.net/2023/02/26/XYMzBbWSsH7x4Ag.png)

在第二步中，选择windows的iso

![image.png](https://s2.loli.net/2023/02/26/aBUs2ncmYCyzvRN.png)

勾选 `在安装前自定义配置` 单击完成

![image.png](https://s2.loli.net/2023/02/26/UhKidjpCDMeT7Oz.png)

如为windows10，按上图选择

如为win11，选择 x86_64后带有secboot的

![image.png](https://s2.loli.net/2023/02/26/cxfa7qwH6ObPr8L.png)

将硬盘从sata改为virtio

添加 viro驱动iso

![image.png](https://s2.loli.net/2023/02/26/36kQMusdR5XjVFe.png)

pci直通独显

![image.png](https://s2.loli.net/2023/02/26/3q9tZHuUd2eochB.png)

# 一定要修改boot选项

修改好配置后点击 `开始安装`

开机时按任意按键（不要按电源键）进入windows安装

![image.png](https://s2.loli.net/2023/02/26/aTFp1ZHguJUl5ni.png)

选择 `自定义`

点击 `加载驱动程序` `确定`选择自己windows版本适用驱动

![image.png](https://s2.loli.net/2023/02/26/fOlHAvXVYuWh9ib.png)

以管理员身份安装 guest-tools

# 一定要去[nvidia官网](https://nvidia.cn/)安装独显最新驱动

![image.png](https://s2.loli.net/2023/02/26/sgJ63I8YMKDb7cv.png)

直通成功，enjoy it！
