---
abbrlink: ''
categories:
- - nvidia
- - ubuntu
- - kvm
cover: https://s2.loli.net/2023/02/26/sgJ63I8YMKDb7cv.png
date: '2023-03-04 11:25:21'
tags:
- nvidia
- ubuntu
- kvm
title: nvidia-intel-passthrough independent display
updated: Sat, 04 Mar 2023 10:18:23 GMT
---
This article was translated by the Chinese version using Google Translate

Chinese : [nvidia-intel-nvidia-直通独显 | Juana's Blog (gw.to)](https://hexo.gw.to/nvidia-intel-nvidia-%E7%9B%B4%E9%80%9A%E7%8B%AC%E6%98%BE/)

# This article was translated by the Chinese version using Google Translate

## 1. Please make sure your bios supports pci passthrough (VT-D virtualization)

## 2. Linux cannot use CUDA after passthrough

# Environment preparation

## 1.[windows iso file](https://www.microsoft.com/zh-cn/software-download/windows10) [windows distribution in China](https://latest10.win/), [viro driver iso](https://github.com/virtio-win/virtio-win-pkg-scripts/blob/master/README.md)

## 2. A computer equipped with ubuntu uses grub as boot

# start installation

## 1. Install KVM

```
sudo apt-get update
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager ovmf
```

![image.png](https://s2.loli.net/2023/02/26/uzSdp5t3wb12Ji6.png)

## 2. Setup libvirt

```
sudo systemctl start libvirtd
sudo systemctl enable libvirtd
```

# 3. Give users permission to manage kvm

```
sudo usermod -aG libvirt $USER
sudo usermod -aG kvm $USER
```

# 4. Open iommu

## Check if iommu is enabled

```
cat /proc/cmdline | grep iommu

```

![image.png](https://s2.loli.net/2023/02/26/vRDheJwtNLp7E4A.png) If the output is like the picture above, please go to the next step

```

sudo nano /etc/default/grub
```

Add `intel_iommu=on` inside ="" of `GRUB_CMDLINE_LINUX_DEFAULT`

![image.png](https://s2.loli.net/2023/02/26/dqGXbwa21RlPscj.png)

After adding, press `ctrl + x` to save and exit

```
sudo update-grub
```

Then restart the computer with `sudo reboot`

# 5. Unbind the graphics card from the host

Change nvidia driver to open source driver

![image.png](https://s2.loli.net/2023/02/26/yVCBpN54ARDfbSx.png)

Change root password: `sudo passwd root`

`su`

```
echo 'blacklist nouveau
blacklist snd_hda_intel' >> /etc/modprobe.d/blacklist.conf
```

![image.png](https://s2.loli.net/2023/02/26/pVbHm2cCz38irwQ.png)

Reboot system `sudo reboot`

# Install the system and configure the independent display passthrough

Open `virt-manager` to create a new virtual machine

![image.png](https://s2.loli.net/2023/02/26/XYMzBbWSsH7x4Ag.png)

In the second step, choose the iso of windows

![image.png](https://s2.loli.net/2023/02/26/aBUs2ncmYCyzvRN.png)

Tick `Customize configuration before installation` Click Finish

![image.png](https://s2.loli.net/2023/02/26/UhKidjpCDMeT7Oz.png)

If it is windows10, select according to the above picture

For win11, select x86_64 with secboot

![image.png](https://s2.loli.net/2023/02/26/cxfa7qwH6ObPr8L.png)

Change hard drive from sata to virtio

Add viro driver iso

![image.png](https://s2.loli.net/2023/02/26/36kQMusdR5XjVFe.png)

pci passthrough independent display

![image.png](https://s2.loli.net/2023/02/26/3q9tZHuUd2eochB.png)

# Be sure to modify the boot option

After modifying the configuration, click `Start Installation`

Press any button (do not press the power button) to enter the Windows installation when booting

![image.png](https://s2.loli.net/2023/02/26/aTFp1ZHguJUl5ni.png)

Select `Custom`

Click `Load Driver` `OK` to select the applicable driver for your Windows version

![image.png](https://s2.loli.net/2023/02/26/fOlHAvXVYuWh9ib.png)

Install guest-tools as administrator

# Be sure to go to [nvidia official website] (https://nvidia.cn/) to install the latest driver

![image.png](https://s2.loli.net/2023/02/26/sgJ63I8YMKDb7cv.png)

Straight through to success, enjoy it!
