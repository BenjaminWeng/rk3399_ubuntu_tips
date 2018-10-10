# rk3399_ubuntu_tips
1. download rk official ubuntu
Firefly-RK3399_xubuntu16.04_20180910.img
https://drive.google.com/drive/folders/0B7HO8lbGgAqAYVI4OVhvdjBkVFE

2. enter maskrom mode and connect type-c USB to PC:
http://wiki.t-firefly.com/zh_CN/Firefly-RK3399/maskrom_mode.html

3. using upgrade_tool in ubuntu
sudo upgrade_tool uf Firefly-RK3399_xubuntu16.04_20180910.img
reboot

4. download firefly kernel src
git clone https://TeeFirefly@gitlab.com/TeeFirefly/linux-kernel.git
git clone https://TeeFirefly@gitlab.com/TeeFirefly/prebuilts.git
http://dev.t-firefly.com/thread-12739-1-1.html
build:
        make ARCH=arm64 firefly_linux_defconfig
        make ARCH=arm64 rk3399-firefly-linux.img -j8
        编译后在内核源码的目录下生成kernel.img和resource.img文件。

5. rkflashkit
安装：
sudo apt-get install build-essential fakeroot 
git clone https://github.com/linuxerwang/rkflashkit
cd rkflashkit
./waf debian
sudo apt-get install python-gtk2
sudo dpkg -i rkflashkit_0.1.4_all.deb
图形界面：
sudo rkflashkit

6. enter rkusb(not maskrom) and using rkflashkit to replace kernel.img and resource.img
