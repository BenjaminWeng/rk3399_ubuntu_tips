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
        sudo make ARCH=arm64 firefly_linux_defconfig  
        sudo make ARCH=arm64 rockchip_linux_defconfig    
        sudo make ARCH=arm64 rk3399-firefly-linux.img -j8  
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

7. modify firefly kernel:  
git clone https://github.com/FireflyTeam/kernel
using branch : firefly ; and checkout to the commit at least after 986a277676d350d020866ab9295a40003afb0fd3  
commit 986a277676d350d020866ab9295a40003afb0fd3  
Author: hzq <service@t-firefly.com>  
Date:   Fri Sep 7 15:36:32 2018 +0800  
    arm64: dts: support camera ov13850  

8. modify files with git diff below:  
https://github.com/FireflyTeam/kernel/commit/986a277676d350d020866ab9295a40003afb0fd3  
add modifications to rk3399-firefly-linux.dts  
http://dev.t-firefly.com/thread-14127-1-1.html  
modify Kconfig of cameras and cif_10  
drivers/media/i2c/soc_camera/rockchip/Kconfig : turn ov13850/4689 on.  
drivers/media/platform/rk-isp10/Kconfig : turn rk-isp10 on.  

9. replace kernel/resource.img with rkflashtool and then test with command below:  
gst-launch-1.0 v4l2src ! video/x-raw,format=NV12,width=640,height=480 ! videoconvert ! autovideosink  
and the image should be shown on the screen!  
