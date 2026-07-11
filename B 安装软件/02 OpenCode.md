---

# OpenCode 使用手册（桌面版 / CLI 版）

---

## 0.1 一、桌面使用（GUI 版）

### 0.1.1 安装  
（已通过 DNF 安装）  
```bash
sudo dnf install opencode
```

### 0.1.2 启动  
- **从系统菜单**：点击 “OpenCode” 图标。  
- **或命令行启动**（可选）：  
  ```bash
  gtk-launch opencode-desktop.desktop
  ```
![[Pasted image 20260710202744.png]]
### 0.1.3 检查版本  
```bash
#检查版本
rpm -q opencode
# 更新
sudo dnf update opencode
```
![[Pasted image 20260710203012.png|568]]
### 0.1.4 卸载  
```bash
sudo dnf remove opencode
```

## 0.2 二、CLI 使用（命令行版）

### 0.2.1 安装  
（已通过官方脚本安装）  
```bash
curl -fsSL https://opencode.ai/install | bash
```

### 0.2.2 启动  
直接在终端输入：  
```bash
opencode
```
常用子命令（示例）：  
- `opencode --help` 查看帮助  
- `opencode <project>` 打开项目
![[Pasted image 20260710203226.png]]

```bash
#检查版本
opencode --version

# 更新
curl -fsSL https://opencode.ai/install | bash
```
![[Pasted image 20260710203530.png]]
### 0.2.3 卸载  
```bash
rm -rf ~/.opencode
# 并手动编辑 ~/.bashrc，删除脚本添加的 PATH 行（如 export PATH="$HOME/.opencode/bin:$PATH"）
```

---

**提示**：桌面版与 CLI 版为独立程序，配置目录可能不同，插件/技能不共享，需分别管理。