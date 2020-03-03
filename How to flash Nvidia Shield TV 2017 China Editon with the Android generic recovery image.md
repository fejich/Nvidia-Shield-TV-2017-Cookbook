# Nvidia Shield TV 2017 国行刷美版固件指南

## 必备文件

1. 命令行工具[minimal_adb_fastboot_v1.4.3_setup.exe](https://forum.xda-developers.com/showthread.php?t=2317790)
2. 驱动程序[SHIELD_Family_WHQL_USB_driver_201801.zip](https://developer.nvidia.com/gameworksdownload#?search=SHIELD%20Family%20Windows%20USB)
3. 美版固件[nv-recovery-image-shield-atv-2017-7.0.1.zip](https://developer.nvidia.com/gameworksdownload#?tx=$additional,shield)

## 准备工作

1. 安装minimal_adb_fastboot_v1.4.3_setup.exe

2. 解压驱动程序SHIELD_Family_WHQL_USB_driver_201801.zip至桌面

3. 解压美版固件nv-recovery-image-shield-atv-2017-7.0.1.zip至任意文件夹，将下列文件移至minimal_adb_fastboot的安装目录

   > - blob
   > - boot.img
   > - recovery.img
   > - system.img
   > - vendor.img

4. 在断电状态下，将Nvidia Shield TV 2017接入如下设备

   > - 通过HDMI接口连接电视或显示器
   > - 通过紧挨HDMI接口的USB接口连接Shield手柄连线，并将连线的另一端接入手柄
   > - 通过靠近散热孔的USB接口连接USB 3.0公对公数据线，并将数据线的另一端留空
   > - 确保路由器可联网（此时无需翻墙）
   > - 打开电视或显示器

## 刷机过程

1. 接通Nvidia Shield TV 2017的电源，依照显示器上的提示，联网并激活设备

2. 进入“设置”-“关于”，将光标定位在“内部版本号”上，连续按7次手柄A键，此时屏幕提示“您现在已处于开发者模式！”

3. 按手柄B键后退，进入“开发者选项”，开启“USB调试”，此时屏幕提示“是否允许USB调试”，在“确定”上按手柄A键，此时屏幕提示“已启用USB调试”

4. 拔除连接至计算机的一切Android设备

5. 将USB 3.0数据线的另一端连接至电脑的USB 3.0端口，计算机会自动安装Nvidia Shield TV驱动。安装完成后，在“设备管理器”-“通用串行总线设备”中，可以看到“ADB Interface”，它的前面没有叹号

6. 使用管理员身份运行“Minimal ADB and Fastboot”，执行如下指令

   ```
   adb devices
   ```

   若看到命令提示符中最后一行为“数字+device”，则表示该设备已连接成功，可继续执行下述操作，否则，必须重新安装驱动程序

7. 执行如下指令

   ```
   adb reboot bootloader
   ```
   重启Nvidia Shield TV 2017进入bootloader界面

8. 此时，Nvidia Shield TV 2017重启并进入bootloader界面，此时，计算机会安装Fastboot驱动，选择从磁盘安装，找到SHIELD_Family_WHQL_USB_driver_201801.zip的解压文件夹并执行安装，屏幕提示Android ADB Interface驱动安装成功

9. 执行如下指令

   ```
   fastboot oem unlock
   ```

   > 注意，执行该指令会擦除Nvidia Shield TV 2017中的全部数据，如有必要，务必提前备份相关文件

   进入bootloader解锁提示界面，此时，按手柄A键

10. 等待一段时间，看到命令提示符中“finished”，之后按手柄A键，Nvidia Shield TV 2017会自动重启两次，重启过程中会有两次警示界面，此时不要做任何操作

11. 待Nvidia Shield TV 2017重启后，依照显示器上的提示，联网并激活设备

12. 进入“设置”-“关于”，将光标定位在“内部版本号”上，连续按7次手柄A键，此时屏幕提示“您现在已处于开发者模式！”

13. 按手柄B键后退，进入“开发者选项”，开启“USB调试”，此时屏幕提示“是否允许USB调试”，在“确定”上按手柄A键。在随之出现的对话框中，选中“一律允许使用这台计算机进行调试”并在“确定”上按手柄A键，此时屏幕提示“已启用USB调试”

14. 执行如下指令

    ```
    adb reboot bootloader
    ```

    重启Nvidia Shield TV 2017进入bootloader界面

15. 按次序逐一执行如下指令

    ```
    fastboot flash staging blob
    fastboot flash boot boot.img
    fastboot flash recovery recovery.img
    fastboot flash system system.img
    fastboot flash vendor vendor.img
    ```

    有几条指令需要较长时间，务必耐心等待。途中不要做任何操作

16.使用手柄X键和Y键，将绿色光标定位于“Boot recovery kernel”，按手柄A键

17. 此时，屏幕显示一个躺着的Android小人，并提示“No Command”。按手柄B键，可进入类似原生Android的刷机界面，在此处，分别执行以“wipe”开头的两条  命令，即“双清”

18. 执行该界面中“reboot”命令，重启Nvidia Shield TV 2017
    > 注意：Nvidia Shield TV 2017国行版本即使刷了Nvidia Shield TV 2017美版固件，开机画面还是会有“爱奇艺”字样，这并不造成任何影响
    > 更新：2018-6-27：NVIDIA官方推送了SHIELD Experience 7.0.2，更新后，Nvidia Shield TV 2017国行版本刷美版固件后遗留的“爱奇艺”图标终于消失，仅剩“NVIDIA”图标
    
19. 将路由器翻墙，待Nvidia Shield TV 2017重启后，依照显示器上的提示，联网并激活设备

20. 进入“设置”-“关于”，将光标定位在“内部版本号”上，连续按7次手柄A键，此时屏幕提示“您现在已处于开发者模式！”

21. 按手柄B键后退，进入“开发者选项”，开启“USB调试”，此时屏幕提示“是否允许USB调试”，在“确定”上按手柄A键。在随之出现的对话框中，选中“一律允许使用这台计算机进行调试”并在“确定”上按手柄A键，此时屏幕提示“已启用USB调试”

22. 执行如下指令

    ```
    adb reboot bootloader
    ```

    重启Nvidia Shield TV 2017进入bootloader界面

23. 执行如下指令

    ```
    fastboot oem lock
    ```
    > 如果这个命令在电脑上报错，可操作手柄于 Shield TV 显示器上选择上锁。效果一样
    > 注意，执行该指令会擦除Nvidia Shield TV 2017中的全部数据，如有必要，务必提前备份相关文件

    进入bootloader锁定提示界面，此时，按手柄A键

24. 等待一段时间，看到命令提示符中“finished”，之后按手柄A键，Nvidia Shield TV 2017会自动重启两次，重启过程中会有两次警示界面，此时不要做任何操作

25. 待Nvidia Shield TV 2017重启后，依照显示器上的提示，联网并激活设备。至此完成刷机

> 1）进入到桌面后无需翻墙，更新至最新版系统方可观看 Netflix

> 2）不翻墙情况下会弹出：”网络已连接，但提示无法连接到互联网“，解决办法是打开 adb 调试，修改联网监测服务器为 google.cn

> adb shell settings put global captive_portal_https_url https://www.google.cn/generate_204
