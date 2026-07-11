# 1 Linux与Windows共享NTFS分区无法识别问题修复流程

## 1.1 排查过程

### 1.1.1 检查Windows磁盘状态（可直接到1.1.2）
在Windows的`diskpart`工具中查看分区信息：
```cmd
diskpart
list disk
select disk X          # 选择存放共享分区的磁盘
list partition
```
- 如果分区显示为 **“未知”**，说明Windows无法识别该分区的类型标识。
- 正常NTFS分区应显示为 **“主要”** 或 **“基本数据分区”**。

### 1.1.2 检查Linux分区表信息
在Linux中查看磁盘详细分区状态：

```
sudo fdisk -l
```
![[附件/Pasted image 20260712020329.png]]
重点确认：
- 磁盘分区表类型：**GPT** 或 **MBR**
- 共享分区的当前类型标识（如 `Linux filesystem`）
- 分区的文件系统是否为 `ntfs`

---

## 1.2 解决方案

### 1.2.1 第一步：在Linux中修改分区类型标识

#### 1.2.1.1 使用 `parted`（推荐，适用于GPT磁盘）
记得替换为共享盘所在硬盘的设备名，上一步可以获得。
使用第一条命令进入交互界面后，依次执行后面5条，说明在后面：
```
sudo parted /dev/nvme1n1    # 替换为你的磁盘设备名
unit s                      # 使用扇区为单位
print                       # 查看分区表
set 4 msftdata on           # 将分区4设为Microsoft基本数据分区（替换为实际分区号）
print                       # 确认标志已变为 msftdata
quit
```

---

### 1.2.2 第三步：在Windows中分配盘符

成功进入Windows后：
#### 1.2.2.1 方法一：磁盘管理（图形界面）
1. 右键“此电脑” → “管理” → “磁盘管理”。
2. 找到修复后的NTFS分区（状态应为“状态良好”）。
3. 右键 → “更改驱动器号和路径” → “添加” → 分配一个盘符（如E:）。

#### 1.2.2.2 方法二：diskpart（命令行）
```cmd
diskpart
select disk 1
list partition
select partition 4
assign letter=E:
exit
```

---

### 1.2.3 第四步：清理系统自动生成的文件夹（可选）

分配盘符后，如果分区中出现了 `ProgramData`、`System Volume Information` 等文件夹：
- 这些是Windows自动生成的，可直接删除（`ProgramData`、`$RECYCLE.BIN` 可安全删除）。
- `System Volume Information` 若无法删除可忽略，不影响使用。

---
