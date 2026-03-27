---
title: unbantu上查看串口方法
date: 2026-01-11 16:41:43
tags: 'Linux命令'
categories: 'Linux'
---

在 **Ubuntu** 下查看串口连接的几种方法如下：

### 1. 查看可用串口设备
使用以下命令列出所有可用的串口设备：

```plain
ls /dev/ttyS* /dev/ttyUSB* /dev/ttyACM*
```

常见的串口设备：

+ `/dev/ttyS*` → 传统串口（如 COM1、COM2）
+ `/dev/ttyUSB*` → USB 转串口设备
+ `/dev/ttyACM*` → 现代 USB CDC 设备（如某些开发板）

### 2. 查看串口设备的详细信息
```plain
dmesg | grep tty
```

如果插入 USB 串口设备，执行 `dmesg` 命令可以看到新的设备被分配的端口。

### 3. 使用 `udevadm` 查询设备信息
```plain
udevadm info -q property -n /dev/ttyUSB0
```

将 `/dev/ttyUSB0` 替换为你的设备端口。

### 4. 查看设备是否被识别
```plain
lsusb
```

这个命令会列出所有 USB 设备，查找你的串口转换器是否被正确识别。

### 5. 检查设备占用情况
```plain
lsof | grep ttyUSB
```

或者：

```plain
sudo fuser -v /dev/ttyUSB0
```

可以查看是否有进程正在占用该串口。

### 6. 使用 `minicom` 或 `screen` 连接串口
如果想直接查看串口数据，可以使用 `minicom` 或 `screen`：

```plain
sudo apt install minicom
sudo minicom -D /dev/ttyUSB0 -b 115200
```

或者：

```plain
sudo screen /dev/ttyUSB0 115200
```

你可以先用 `ls /dev/tty*` 确认串口设备是否存在，再选择合适的方法进行查看和调试。

### 7. 查看串口接收到数据
```plain
sudo stty -F /dev/ttyUSB1 921600 cs8 -cstopb -parenb -ixon raw
cat /dev/ttyUSB1
```



