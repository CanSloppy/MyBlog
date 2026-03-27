---
title: Linux查看日志方法
date: 2025-09-18 16:41:43
tags: 'Linux命令'
categories: 'Linux'
---

在 Linux 下查看程序日志的方法取决于程序的日志输出方式和运行方式。有几种常用方式：

------

## 1. 程序输出到控制台（stdout/stderr）

如果程序直接打印日志到终端：

```
./my_program
```

- stdout（标准输出）和 stderr（标准错误）会直接显示在终端。
- 可以通过重定向保存日志：

```
./my_program > program.log 2>&1
```

- `>`：重定向 stdout
- `2>&1`：把 stderr 也重定向到同一个文件

查看日志：

```
tail -f program.log   # 实时查看
less program.log      # 分页查看
```

------

## 2. 系统服务（Systemd / daemon）

如果程序作为系统服务运行：

```
sudo systemctl status my_service
sudo journalctl -u my_service
```

- `systemctl status` 查看服务状态和最近日志
- `journalctl -u` 查看完整日志
- 加 `-f` 实时跟踪：

```
sudo journalctl -u my_service -f
```

------

## 3. 日志写入文件

一些程序自己写日志到文件，例如 `/var/log/my_program.log`。

- 查看：

```
tail -f /var/log/my_program.log
```

- 或者分页查看：

```
less /var/log/my_program.log
```

------

## 4. 查看运行中进程的输出

如果程序已经运行在后台，但没有日志文件：

- 可以尝试找到它的 stdout/stderr 文件描述符：

```
ls -l /proc/<PID>/fd
```

- 通常 `/proc/<PID>/fd/1` 是 stdout，`/proc/<PID>/fd/2` 是 stderr
- 如果是管道或者重定向的文件，你可以用 `cat` 或 `tail -f` 查看。