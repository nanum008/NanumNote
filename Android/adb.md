```
1.adb devices  
2.adb install xxx.apk
3.adb pull	手机端路径 电脑端路径  用于手机提出文件
eg：adb pull /sdcard/DCIM D:/    即可从将DCIM文件夹复制到D盘
4.adb push 电脑端路径 手机端路径 用于将文件推送到手机
eg：adb push D:/DCIM /sdcard/    即可从将D盘的DCIM文件夹复制到存储根目录
5.adb reboot 参数
adb reboot 正常重启
adb reboot recovery 手机重启到recovery卡刷模式
adb reboot bootloader 手机进入BootLoader（fastboot）进入线刷模式
adb reboot edl 手机会重启到9008刷机模式，仅限高通部分机型使用，
6.adb sideload xxx.zip 用于sideload模式推送刷机包
在rec打开sideload模式后发送刷机包。
7.   adb shell    用于进入手机的shell
8. 刷入第三方recovery和启动recovery 
fastboot flash recovery xxx.img
9. 解锁bootloader和上锁
这个不适用于大多数小米手机！特殊情况用！
           fastboot oem lock
           fastboot oem unlock


```

