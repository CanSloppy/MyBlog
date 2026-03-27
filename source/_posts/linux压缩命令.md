---
title: linux压缩命令
date: 2025-08-18 16:41:43
tags: 'Linux命令'
categories: 'Linux'
---

在 Linux 中，你可以使用多种工具进行**压缩和解压**，常见的格式包括 `tar.gz`、`zip`、`7z` 等。

---

## **1. **`**tar**`**（最常用的压缩/解压工具）**
### **（1）压缩 **`**tar.gz**`
```plain
bash


复制编辑
tar -czvf 压缩文件.tar.gz 需要压缩的文件或文件夹
```

**示例：**

```plain
bash


复制编辑
tar -czvf my_files.tar.gz my_folder
```

+ `-c`：创建压缩包
+ `-z`：使用 `gzip` 压缩
+ `-v`：显示压缩过程（可选）
+ `-f`：指定文件名

---

### **（2）解压 **`**tar.gz**`
```plain
bash


复制编辑
tar -xzvf 压缩文件.tar.gz
```

**示例：**

```plain
bash


复制编辑
tar -xzvf my_files.tar.gz
```

如果想解压到指定目录：

```plain
bash


复制编辑
tar -xzvf my_files.tar.gz -C /home/user/extracted/
```

---

### **（3）压缩 **`**tar.bz2**`**（更高压缩率）**
```plain
bash


复制编辑
tar -cjvf my_files.tar.bz2 my_folder
```

解压：

```plain
bash


复制编辑
tar -xjvf my_files.tar.bz2
```

---

## **2. **`**zip**`**（Windows 兼容）**
### **（1）压缩**
```plain
bash


复制编辑
zip -r my_files.zip my_folder
```

`-r` 选项用于递归压缩整个文件夹。

### **（2）解压**
```plain
bash


复制编辑
unzip my_files.zip
```

---

## **3. **`**7z**`**（高压缩比，适合大文件）**
如果没有安装 `7z`，可以先安装：

```plain
bash


复制编辑
sudo apt install p7zip-full
```

### **（1）压缩**
```plain
bash


复制编辑
7z a my_files.7z my_folder
```

### **（2）解压**
```plain
bash


复制编辑
7z x my_files.7z
```

---

## **4. **`**xz**`**（单文件高压缩）**
### **（1）压缩**
```plain
bash


复制编辑
xz -z myfile.txt
```

### **（2）解压**
```plain
bash


复制编辑
xz -d myfile.txt.xz
```

---

## **推荐使用**
+ `**tar.gz**`：最常见，适用于 Linux，`tar -czvf` / `tar -xzvf`
+ `**zip**`：跨平台兼容性好，适用于 Windows 交互，`zip -r` / `unzip`
+ `**7z**`：适用于大文件高压缩率，`7z a` / `7z x`



