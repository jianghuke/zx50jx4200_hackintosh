# Asus ZX50J

zx50jx4200_hackintosh
华硕zx50jx4200 黑苹果Clover 可用于安装10.14.4
## 配置：

CPU：i5-4200h

内存：8g 

显卡：Intel HD 4600 + gtx950M(已屏蔽）

外存：东芝120g m.2 SSD + 原厂1t机械

网卡/蓝牙：无线网卡蓝牙更换为 DW1560 NGFF接口
注：未换网卡的看清楚使用说明

注：

本CLOVER由远景论坛Mr.xiaoban分享的EFI修改

http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1761359&highlight=zx50



## 目前bug 
1.fn+F1会导致睡死 

2.开启HIDPI后开机画面闪现8苹果 进系统后画面正常

3.无法使用pppoe拨号 未测试（原efi有这个bug）

4.HDMI音频有输出，但是会破音

5.其他未发现bug

音频输入需要用工具修复

目前还挺完美的 包括变频 睡眠 键盘灯 亮度调节 等
启用睡眠需要关闭bios的CPU节能功能
bios中关闭power off energy saving

## 其他
1.打开安全和隐私中的任何来源 
终端输入 sudo spctl --master-disable

2.建立一个在Win和Mac下都能读取的分区

    在win系统下自带的磁盘管理工具中压缩一个适量空间的分区然后新建简单卷分配盘符然后格式化为exFAT格式,这个分区的内容就能在win和mac系统下都能读取了。）

3.开启Hidpi 

用RDM这个软件

4.修复声卡输入 

    使用麦克风修复目录下载教程修复

5.修复睡眠

bios中关闭power off energy saving

6.查看加载的驱动
kextstat | grep -v "com.apple"      显示除了苹果之外的驱动加载
kextstat | grep -v "com.apple" | grep -v "Energy"   查看加载的非官方驱动

7.解决Mojave在低分屏上字体发虚需要做两件事情：
1）打开 【终端】应用，输入下面命令，全局启用 次像素抗锯齿 渲染：
defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO
2）设置字体 次像素抗锯齿 级别 (类似 Linux 的 hintstyle 微调样式) 的命令：
defaults -currentHost write -globalDomain AppleFontSmoothing -int 3
还原命令为：
1）defaults write -g CGFontRenderingFontSmoothingDisabled -bool YES
2）defaults -currentHost delete -globalDomain AppleFontSmoothing

8.如果没有更换dw1560网卡（如果打算长期使用黑苹果并打算使用隔空投送的话建议更换网卡）

删除Clover/kexts/others下面四个驱动
AirportBrcmFixup.kext 
FakePCIID_Broadcom_WiFi.kext 
BrcmFirmwareData.kext
BrcmPatchRAM2.kext 
