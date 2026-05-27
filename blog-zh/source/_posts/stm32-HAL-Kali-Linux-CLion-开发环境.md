---
title: stm32 HAL 开发环境搭建（Kali Linux + CLion）
date: 2026-05-21 10:04:35
tags: 
    - stm32
    - HAL
    - 嵌入式
    - Kali
    - Linux
    - CLion
---

## 为什么会有这篇文章
Windows 又一次占满了我的 C 盘！我一退再退，从 100G、200G 到 300G。但这次绝对不行！
我决定把所有开发工作迁移到 Linux 上。我选择了比较熟悉的 Kali Linux，顺便说一句，它的界面确实很好看。
我最近做得最多的开发之一就是 stm32，所以笔记本装上 Kali 之后，我就立刻搭建了开发环境。
来看看怎么搞。

## 开始
确保你的电脑已经装好了 Linux。（没错，确保一下）
你可能想先升级一下系统。
```
#Debian 系
sudo apt update
sudo apt upgrade
```
# 安装

## 需要安装的东西

- CubeMX  （stm32 图形化配置工具）
- CLion   （C/C++ IDE）
- CubeCLT  （编译所需的所有工具）

## CubeMX
前往 <https://www.st.com.cn/zh/development-tools/stm32cubemx.html> 下载 Linux 版本
![](photo/CubeMX.png)
你会得到一个 .zip 文件，解压它。

```
mkdir CubeMX
mv <zip 包> CubeMX
cd CubeMX
unzip <zip 包>
rm <zip 包>
#以我为例
unzip stm32cubemx-lin-v6-17-0.zip
```
然后你会看到一个名为 SetupSTM32CubeMX-x.x.x 的文件，运行它
```
sudo ./SetupSTM32CubeMX-x.x.x
#以我为例
sudo ./SetupSTM32CubeMX-6.17.0
```
如果一切顺利，你会看到一个安装窗口，跟着引导走就能完成 CubeMX 的安装。到你安装的目录下运行 STM32CubeMX 即可启动软件。
另外，这样启动软件不太方便，你可以在桌面添加一个 .desktop 文件，以便双击启动 CubeMX。参考 <https://comate.baidu.com/zh/page/9kqwoz7ac6m>

## CLion
前往 <https://www.jetbrains.com.cn/clion/download/?section=linux> 下载。
然后解压。
```
tar -zxvf CLion-xxxx.x.x.tar.gz
#以我为例
tar -zxvf CLion-2026.1.2.tar.gz
```
把整个文件夹移动到你想要安装的位置，比如 /opt
```
mv clion-xxxx.x.x /opt/
```
运行 /clion-xxxx.x.x/bin/clion 启动 CLion
和 CubeMX 一样，你也可以为 CLion 创建 .desktop 文件

## CubeCLT
前往 <https://www.st.com.cn/zh/development-tools/stm32cubeclt.html> 下载 Linux 版本。
解压。
```
unzip <zip 文件名>
#以我为例
unzip st-stm32cubeclt_1.21.0_27995_20260219_1804_amd64.sh.zip
```
运行 .sh 脚本
```
bash <*.sh>
#以我为例
bash st-stm32cubeclt_1.21.0_27995_20260219_1804_amd64.sh
```
你需要输入几个 'y' 来接受许可协议，然后选择安装目录（我用了默认的）
恭喜！现在你已经安装了所有需要的工具。

# 配置
首先启动 CLion，新建一个项目。在 Embedded 分类下找到 STM32CubeMX，填入 CubeMX 和 CubeMXCLT 的安装路径。
![](photo/CLion.png)
然后点击 Launch STM32CubeMX，完成 stm32 芯片的配置。
现在进入 Project Manager 页面，输入项目名称和路径，并选择 Toolchain/IDE 为 CMake。
![](photo/Cubemx.png)
生成代码！
回到 CLion，第一次会要求你选择工具链。如下图所示选择目录，cubeMXctl 文件夹里包含了所有需要的工具
![](photo/clion.png)
然后配置 CMake
![](photo/CMake.png)
提示：确保在 CMake options 中添加 "--preset=Debug"。

# 享受开发吧！
现在你已经拥有了一个 Linux 下的 stm32 HAL 开发环境！

---

[English Version](http://juliantree.top/en)
