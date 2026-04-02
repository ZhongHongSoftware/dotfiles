# MengXiOS Dotfiles

> MengXiOS 桌面环境的配置文件集，为 Hyprland + DMS 套件提供开箱即用的现代化体验。

## 📌 简介

这套 dotfiles 是为 **MengXiOS** 量身打造的配置文件集合，旨在提供一个美观、高效、可定制的 Arch Linux 桌面环境。集成平铺式窗口管理、终端复用、编辑器增强和主题化登录管理器。

## ✨ 特性

- 🪟 **Hyprland** – 动态平铺 Wayland 合成器，预设动画、透明、毛玻璃效果
- 🐱 **Kitty** – GPU 加速终端模拟器，预配置主题和字体
- 📝 **Neovim** – 现代化编辑器，预装 LSP、补全、文件树
- 🐚 **DMS-Shell** – ZDK 组件，提供状态栏、启动器、通知中心
- 🔐 **SDDM** + **Silent Theme** – 极简登录管理器主题
- 📦 **MengXiOS Arch 源** – 自动配置，获取 DMS 套件和定制包

## 📦 依赖清单

| 软件包 | 用途 | 备注 |
|--------|------|------|
| `hyprland` | Wayland 合成器 | 核心窗口管理 |
| `kitty` | 终端模拟器 | GPU 加速 |
| `neovim` | 文本编辑器 | >= 0.9 版本 |
| `dms-shell` | DMS 桌面外壳 | ZDK 组件 |
| `sddm` | 显示管理器 | 登录界面 |
| `sddm-silent-theme` | SDDM 主题 | 极简风格 |

> 注：`dms-shell` 和 `sddm-silent-theme` 需从 MengXiOS Arch 源获取。

## 🚀 快速安装

### 1. 添加 MengXiOS Arch 源

```bash
# 编辑 pacman.conf
sudo nano /etc/pacman.conf

# 在文件末尾添加以下内容
[mengxios]
Server = http://repo.zhsoft.tech/$arch

# 更新软件包数据库
sudo pacman -Sy
```

### 2. 安装依赖

```bash
# 安装核心依赖（从官方源）
sudo pacman -S hyprland kitty neovim sddm

# 从 MengXiOS 源安装 DMS 套件和 SDDM 主题
sudo pacman -S dms-shell sddm-silent-theme
```

### 3. 安装 dotfiles

```bash
# 克隆仓库
git clone https://github.com/mengxios/dotfiles.git
cd dotfiles

# 直接构建并安装
makepkg -si
```

该命令将：
- 检查依赖项
- 复制配置文件到 `~/.config/`
- 设置必要的环境变量
- 可选：备份现有配置

### 4. 配置 SDDM

```bash
# 设置 SDDM 主题
sudo nano /etc/sddm.conf
```

添加以下内容：

```ini
[Theme]
Current=silent

[Users]
HideUsers=root
HideShells=/bin/nologin

[Autologin]
User=你的用户名
Session=hyprland
```

### 5. 启动

```bash
# 启用 SDDM 服务
sudo systemctl enable sddm
sudo systemctl start sddm

# 或直接从 TTY 启动 Hyprland（测试用）
Hyprland
```


## 🎛️ 默认快捷键（Hyprland）

| 快捷键 | 功能 |
|--------|------|
| `Super + T` | 打开 Kitty 终端 |
| `Super + Space` | 打开 DMS 启动器 |
| `Super + Q` | 关闭活动窗口 |
| `Super + H/J/K/L` | Vim 风格窗口导航 |
| `Super + Shift + H/J/K/L` | 移动窗口方向 |
| `Super + 1-9` | 切换工作区 |
| `Super + Shift + 1-9` | 移动窗口到工作区 |
| `Super + F` | 切换浮动模式 |
| `PrtSc` | 截图（区域截图） |
| `Super + M` | 打开系统监视器 |

完整快捷键请查看 `~/.config/hypr/binds.conf`。

## 🎨 主题与外观

- **终端配色**: Catppuccin Mocha（可切换）
- **编辑器主题**: Catppuccin + Tokyo Night
- **状态栏**: DMS-Bar（毛玻璃效果，显示工作区、时间、系统托盘）
- **应用启动器**: DMS-Launcher（模糊背景，应用搜索）
- **通知中心**: DMS-Notifd（右上角弹窗）
- **登录界面**: SDDM Silent Theme（极简居中输入框）

## 🔧 自定义配置

### 修改 Hyprland 设置

```bash
nano ~/.config/hypr/hyprland.conf
```

## 📦 更新

```bash
# 进入 dotfiles 目录
cd ~/path/to/dotfiles

# 拉取最新代码
git pull

# 重新构建安装
makepkg -si
```

## 🗑️ 卸载

```bash
# 使用 pacman 卸载
sudo pacman -R mengxios-dotfiles

# 手动清理配置文件（可选）
rm -rf ~/.config/hypr ~/.config/kitty ~/.config/nvim 
```

## 🐛 故障排除

### Hyprland 无法启动

```bash
# 检查显卡驱动
lspci -k | grep -A 2 -E "(VGA|3D)"

# 确保环境变量
export XDG_RUNTIME_DIR=/run/user/$(id -u)
export QT_QPA_PLATFORM=wayland
```

### SDDM 主题不生效

```bash
# 检查主题路径
ls /usr/share/sddm/themes/silent/

# 重新生成配置
sudo sddm-greeter --test-mode --theme /usr/share/sddm/themes/silent
```

### DMS-Shell 未启动

```bash
# 手动启动调试
dms run
```

## 🤝 贡献

欢迎提交 Issue 和 PR。  
提交前请确保：

1. 配置与现有风格一致
2. 更新相关文档
3. 测试在纯净环境中可用

## 📄 许可证

GPL V3 License © 2023-Now MengXiOS Team

## 🔗 相关链接

- [MengXiOS 官网](https://mengxios.org)
- [MengXiOS Arch 源](http://repo.zhsoft.tech)
- [Hyprland Wiki](https://wiki.hyprland.org)
- [DMS 套件文档](https://danklinux.com)
