### create boot.img for SC02G 
  
#### source modified  
1. arch/arm/mach-msm/board-8974-sec-kactive-gpiomux.c  
2. drivers/felica  
  
#### enviroment   
``` sh 
$ export ARCH=arm  
$ export CROSS_COMPILE=~/arm-linux-androideabi-4.9/bin/arm-linux-androideabi-  
``` 
  
#### build kernel  
``` sh 
$ cd kernel  
$ make lineage_kltedcmactive_defconfig  
$ make -j4  
```
  
#### create dt.img  
``` sh
$ dtbTool -s 2048 -o arch/arm/boot/dt.img -p scripts/dtc/ arch/arm/boot/  
```
  
#### unpack klteactivexx boot.img  
``` sh 
$ mkboot boot.img boot 
```
  
#### repack boot.img  
``` sh 
$ cp kernel/arch/arm/boot/zImage boot/kernel  
$ cp kernel/arch/arm/boot/dt.img boot/dt.img  
$ mv boot.img boot.img.old  
$ mkboot boot boot.img  
```
  
#### make tar for odin  
``` sh 
$ tar --format=ustar -cf android-10.0-boot-sc02g.tar boot.img  
```
    

