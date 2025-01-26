# FT8

FT8 是一种使用计算机进行 QSO 的通讯模式，相较于 SSB 和 CW 来说，FT8 对操作员的技术及能力要求都更低，即使面对低效率的天线系统 + 恶劣的传播条件，FT8 也有几乎最高的几率完成 QSO。

无论你对 FT8 持有何种看法，但不可否认的是，FT8 是一种对整套短波系统工作状态进行快速验证的最佳方式。

(tr)uSDX 内置 USB CAT 模式，可以直接使用 USB 线连接 Android 设备或 Windows 设备进行通讯，即使是不支持 OTG 功能的设备（ 例如 iOS ），也可以使用音频线的方式进行 FT8 操作。

## 使用 Android 设备进行 FT8 操作

在 Android 平台进行 FT8 操作我个人推荐使用 FT8CN app，除了功能全面（ 支持所有 FT8 消息类型，支持日志功能 ），FT8CN 还直接内置了 (tr)uSDX CAT 模式参数，简单设置即可使用。DL2MAN为(tr)uSDX提供了建伍TS-480电台的CAT控制命令子集支持，让手机能够通过USB上模拟的串口协议上的CAT指令，获取/设置 (tr)uSDX的频率、调制模式，甚至双向传输音频流。

首先是在官方渠道下载 [FT8CN](https://github.com/N0BOY/FT8CN/releases/) app 并安装，截止目前（2025年1月），FT8CN的最新版本为0.93

然后，转到“设置”选项卡，在“电台型号”处选择 **(tr)uSDX (TS-480）** 或者**(tr)uSDX (audio over cat)** 这两种模式有所区别：

- trusdx(TS-480)
这种模式主要通过USB线连接trusdx和设备（如手机或电脑），实现对trusdx的CAT控制。
它使用的是标准的Kenwood TS-480的CAT协议，波特率通常设置为38400（或115200，在2.00t及以上版本的固件）。
在这种模式下，音频信号需要通过单独的音频线连接到设备的音频输入/输出接口。

- trusdx(audio over cat)
这种模式不仅实现了CAT控制，还通过USB线将音频信号流式传输到设备（或从设备传输到手机），无需额外的音频线。
音频信号和CAT控制信号通过同一个USB接口传输，大大简化了连接方式。
这种模式需要trusdx固件版本至少为2.00u或更新版本


关于FT8CN的更多操作说明，可参考[FT8CN](https://github.com/N0BOY/FT8CN) 官方提供的快速指南和使用说明。

## 使用 iOS 设备进行 FT8 操作

施工中...

## 使用 Windows或Linux 设备进行 FT8 操作

该操作需要先安装[(tr)uSDX audio驱动程序](https://github.com/threeme3/trusdx-audio)，且(tr)uSDX的固件版本应当在2.00u及以上。
驱动安装后，打开，应显示以下字样

> (tr)usDx driver ok! Available devices = [CABLE Input, CABLE Output, COM8]

该驱动程序的功能是虚拟一个音频设备（ Virtual Audio Cable），并打开一个虚拟的串行端口COM8，在WSJT-X等应用程序和电台之间充当中介通过 CAT 流协议传输CAT命令和音频流。（类似上述FT8CN android app内建的支持。）

以WSJT-X为例，在WSJT-X中打开设置——音频选项卡，把音频输入设备改为CABLE Output (VB-Audio Virtual Cable)，音频输出设备改为CABLE Input (VB-Audio Virtual Cable)

再切换到radio选项卡，电台设备改为“TS-480”，CAT控制中选择COM8（刚才的驱动程序为我们打开的虚拟端口），波特率改为115200
实际上，该WSJT-X、WSJT-Z、JS8CALL、FlDigi （PSK31，RTTY模式）、Winlink 、UZ7HO SoundModem等。


## 故障排除
USB通讯可能受到周围电磁环境的影响，导致CAT音频流传输断续。如条件允许，可以购买或制作带有扼流磁环的USB线。

部分国外DIY爱好者提到CAT控制可能会干扰音频流，为了减少这种情况，可将 CAT 轮询间隔（Poll Interval）设置得长一些。

