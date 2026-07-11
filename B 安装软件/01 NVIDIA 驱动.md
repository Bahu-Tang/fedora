# 1 一、安装
[github教程1](https://github.com/Maomaokuxs/Biyuan-Fedora-Learning/wiki/%E5%AE%89%E8%A3%85Nvidia%E6%98%BE%E5%8D%A1%E9%A9%B1%E5%8A%A8%E5%B9%B6%E5%BC%80%E5%90%AF%E7%A1%AC%E4%BB%B6%E7%BC%96%E8%A7%A3%E7%A0%81
)
# 2 二、查看
## 2.1 方法一：图形化界面查看（推荐，最直观）

### 2.1.1 第 1 步：打开软件

-**“NVIDIA X Server Settings”** **点击打开它**。 
![[Pasted image 20260710035910.png]]
### 2.1.2 第 2 步：查看驱动版本号

![[Pasted image 20260710035846.png]]
### 2.1.3 第 3 步：查看显卡实时使用情况（温度/负载/功耗）

你的显卡型号 **“GPU 0 - (GeForce RTX 3060)”**。找到 **“PowerMizer”**（电源管理）选项卡，旁边的 **“Thermal Settings”**（热设置）选项卡。
## 2.2 方法二：终端查看（黑框框方法，适合快速看一眼）

这个方法不需要鼠标，适合远程连接（SSH）或者喜欢敲命令的场景。

### 2.2.1 第 1 步：打开终端

### 2.2.2 第 2 步：查看驱动版本

nvidia-smi | head -n 3

![[Pasted image 20260710040513.png]]

### 2.2.3 第 3 步：查看当前显卡实时状态（静态快照）

nvidia-smi
![[Pasted image 20260710040743.png]]
- 表格里面的这几列：
    
    - **Temp**：当前温度（比如 40°C）。
        
    - **GPU-Util**：当前显卡计算占用率（比如 34%，如果玩游戏会跳到 90% 以上）。
        
    - **Memory-Usage**：显存用了多少（比如 41MiB / 6144MiB，后面的是总显存）。
        

### 2.2.4 第 4 步（进阶操作）：数据自动刷新

连续盯着看：这会让屏幕上的表格**每隔 1 秒自动刷新一次

watch -n 1 nvidia-smi
![[Pasted image 20260710041038.png]]
## 2.3 额外彩蛋：像任务管理器一样的彩色界面（可选安装）

如果你觉得 `nvidia-smi` 的黑白字看着累，可以安装 `nvtop`，它长得像 Windows 的任务管理器：

1. 先安装（只需装一次）：
	sudo dnf install nvtop
2. 以后想看了，直接在终端输入：看到彩色的柱状图，显示每个进程吃了多少显存
	nvtop
![[Pasted image 20260710041107.png]]