# iTerm2 安装配置使用指南

> macOS 最强终端工具完全指南 —— 从安装到精通

---

## 目录

- [简介](#简介)
- [安装](#安装)
- [基础配置](#基础配置)
- [外观美化](#外观美化)
- [Oh My Zsh 集成](#oh-my-zsh-集成)
- [实用功能详解](#实用功能详解)
- [快捷键速查](#快捷键速查)
- [高级功能](#高级功能)
- [常见问题](#常见问题)

---

## 简介

iTerm2 是 macOS 上功能最强大的终端模拟器，是系统自带 Terminal.app 的完美替代品。它提供了：

- 分屏、标签页管理
- 丰富的主题和配色方案
- 搜索、自动补全
- 触发器、Profiles、Arrangements
- 与 tmux 深度集成
- 脚本自动化支持

**系统要求：** macOS 10.14 (Mojave) 及以上

---

## 安装

### 方式一：官网下载（推荐）

1. 访问 [https://iterm2.com](https://iterm2.com)
2. 点击 **Download** 下载最新稳定版
3. 解压后将 `iTerm.app` 拖入 `/Applications` 文件夹

### 方式二：Homebrew 安装

```bash
# 安装 Homebrew（如果还没有）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 通过 Homebrew Cask 安装 iTerm2
brew install --cask iterm2
```

### 验证安装

打开 Spotlight（`⌘ + Space`），搜索 `iTerm` 并启动。

---

## 基础配置

### 进入偏好设置

```
iTerm2 菜单 → Settings（⌘ + ,）
```

### General（通用）

| 选项 | 推荐设置 | 说明 |
|------|----------|------|
| Startup | Use System Window Restoration Setting | 启动时恢复上次窗口 |
| Closing | Confirm closing multiple sessions | 关闭多会话时确认 |
| Magic | Enable Python API | 开启 Python 脚本支持 |

### Appearance（外观）

```
Settings → Appearance → General
```

- **Theme**：推荐选 `Minimal` 或 `Compact`（更现代简洁）
- **Tab Bar Location**：`Top`（标签栏置顶）
- **Status Bar Location**：`Bottom`（状态栏置底）

### Profiles（配置文件）

Profiles 是 iTerm2 的核心概念，每个 Profile 可以有独立的颜色、字体、快捷键等配置。

**创建新 Profile：**
1. `Settings → Profiles → 左下角 +`
2. 设置名称，如 `Default`

#### Colors（颜色）

推荐导入流行配色方案：

```bash
# 下载 Dracula 配色（示例）
git clone https://github.com/dracula/iterm.git ~/Downloads/dracula-iterm

# 然后在 Settings → Profiles → Colors → Color Presets → Import
# 选择下载的 .itermcolors 文件
```

常用配色方案：
- **Dracula** — 暗紫色主题，护眼
- **Solarized Dark** — 经典暗色方案
- **One Dark** — Atom 编辑器风格
- **Nord** — 北欧蓝色调
- **Catppuccin** — 现代柔和风格

#### Text（字体）

推荐使用支持连字符的等宽字体：

```bash
# 安装 Nerd Fonts（包含图标字体，配合 Oh My Zsh 主题）
brew tap homebrew/cask-fonts
brew install --cask font-meslo-lg-nerd-font
brew install --cask font-fira-code-nerd-font
brew install --cask font-jetbrains-mono-nerd-font
```

设置路径：`Settings → Profiles → Text → Font`

推荐配置：
- Font: `MesloLGS NF` 或 `JetBrainsMono Nerd Font`
- Size: `13` 或 `14`
- 勾选 `Use ligatures`（启用连字符）

#### Window（窗口）

```
Settings → Profiles → Window
```

- **Transparency**：透明度，推荐 `10-20`
- **Blur**：毛玻璃效果，搭配透明度使用
- **Columns / Rows**：默认窗口大小，推荐 `220 x 50`

#### Terminal（终端）

```
Settings → Profiles → Terminal
```

- **Scrollback lines**：设置为 `10000`（增大滚动缓冲区）
- **Silence bell**：勾选（关闭响铃）

### Keys（快捷键）

```
Settings → Profiles → Keys → Key Mappings
```

**推荐添加 Option 键跳词映射（像 macOS 文本框一样用 Option+← → 跳词）：**

| 快捷键 | Action | 参数 |
|--------|--------|------|
| `⌥ + ←` | Send Escape Sequence | `b` |
| `⌥ + →` | Send Escape Sequence | `f` |
| `⌥ + ⌫` | Send Hex Code | `0x17` |

---

## 外观美化

### 状态栏（Status Bar）

```
Settings → Profiles → Session → Status bar enabled ✓ → Configure Status Bar
```

可拖入的组件：
- CPU Utilization（CPU 使用率）
- Memory Utilization（内存使用）
- Network Throughput（网络速率）
- Current Directory（当前目录）
- Git State（Git 状态）
- Clock（时钟）

### 窗口透明度 + 毛玻璃

```
Settings → Profiles → Window
→ Transparency: 15
→ Blur: ✓ (Radius: 20)
```

> 快捷切换透明度：`⌘ + U`

### 隐藏标题栏（Minimal 主题）

```
Settings → Appearance → General → Theme: Minimal
Settings → Appearance → Windows → Hide scrollbars ✓
```

---

## Oh My Zsh 集成

### 安装 Zsh + Oh My Zsh

macOS 已默认使用 Zsh，直接安装 Oh My Zsh：

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 安装 Powerlevel10k 主题（最推荐）

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

编辑 `~/.zshrc`：

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

重新加载并配置：

```bash
source ~/.zshrc
# 首次运行会自动启动交互式配置向导
p10k configure
```

### 安装实用插件

```bash
# zsh-autosuggestions：命令历史自动建议
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting：命令语法高亮
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# zsh-z：智能目录跳转（类似 autojump）
git clone https://github.com/agkozak/zsh-z \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-z
```

编辑 `~/.zshrc` 启用插件：

```bash
plugins=(
  git
  z
  zsh-autosuggestions
  zsh-syntax-highlighting
  macos
  docker
  kubectl
)
```

```bash
source ~/.zshrc
```

---

## 实用功能详解

### 分屏（Split Panes）

| 操作 | 快捷键 |
|------|--------|
| 水平分屏 | `⌘ + D` |
| 垂直分屏 | `⌘ + Shift + D` |
| 切换分屏 | `⌘ + Option + 方向键` |
| 调整分屏大小 | `Ctrl + ⌘ + 方向键` |
| 关闭当前分屏 | `⌘ + W` |
| 最大化当前分屏 | `⌘ + Shift + Enter` |

### 标签页管理

| 操作 | 快捷键 |
|------|--------|
| 新建标签页 | `⌘ + T` |
| 关闭标签页 | `⌘ + W` |
| 切换下一个 | `⌘ + →` 或 `⌘ + Shift + ]` |
| 切换上一个 | `⌘ + ←` 或 `⌘ + Shift + [` |
| 跳转到第 N 个 | `⌘ + 数字` |
| 移动标签页 | 拖拽 |

### 搜索

| 操作 | 快捷键 |
|------|--------|
| 在当前窗口搜索 | `⌘ + F` |
| 向上/向下查找 | `Enter` / `Shift + Enter` |
| 退出搜索 | `Esc` |

### 全屏与 Hotkey Window

**Hotkey Window（热键窗口）** 是 iTerm2 最实用的功能之一 —— 随时按快捷键呼出/隐藏终端：

```
Settings → Keys → Hotkey
→ Show/hide all windows with a system-wide hotkey ✓
→ 设置快捷键，如 Option + Space 或 ⌃ + `
```

推荐配置：创建一个专门的 `Hotkey` Profile，设置为半透明、无边框风格。

### 自动补全

- `⌘ + ;`：打开自动补全弹窗（基于历史命令）
- 输入时会显示灰色建议，按 `→` 接受建议

### 命令历史

- `⌘ + Shift + H`：打开粘贴板历史
- `⌃ + R`：反向搜索命令历史（标准 shell 功能）

### 标记（Marks）与导航

iTerm2 会自动标记每个命令的起始位置：

| 操作 | 快捷键 |
|------|--------|
| 跳转到上一条命令 | `⌘ + ↑` |
| 跳转到下一条命令 | `⌘ + ↓` |
| 选中上一条命令输出 | `⌘ + Shift + ↑` |

### 即时回放（Instant Replay）

回放终端内容历史（类似录像回放）：

```
⌘ + Option + B  →  进入即时回放模式
← →             →  时间轴前进/后退
Esc             →  退出回放
```

### Triggers（触发器）

根据终端输出内容自动执行动作，例如：

- 匹配 `ERROR` 关键词时高亮显示
- 匹配 IP 地址时自动打开 SSH

```
Settings → Profiles → Advanced → Triggers → +
```

示例触发器：高亮 ERROR：
- Regular Expression: `\bERROR\b`
- Action: `Highlight Text`
- Parameters: 红色背景

### Shell Integration

安装 Shell Integration 后可获得额外功能：

```bash
curl -L https://iterm2.com/shell_integration/install_shell_integration.sh | bash
```

功能包括：
- 命令执行时间显示
- 上传/下载文件（`imgcat`、`it2dl`）
- 标记命令成功/失败
- 在 SSH 远程主机上也能使用部分功能

---

## 快捷键速查

### 窗口与标签

| 快捷键 | 功能 |
|--------|------|
| `⌘ + N` | 新建窗口 |
| `⌘ + T` | 新建标签页 |
| `⌘ + W` | 关闭标签/分屏 |
| `⌘ + D` | 水平分屏 |
| `⌘ + Shift + D` | 垂直分屏 |
| `⌘ + Enter` | 切换全屏 |
| `⌘ + Shift + Enter` | 最大化/还原当前分屏 |

### 编辑

| 快捷键 | 功能 |
|--------|------|
| `⌘ + C` | 复制（无需选中，自动复制选中内容） |
| `⌘ + V` | 粘贴 |
| `⌘ + F` | 搜索 |
| `⌘ + K` | 清屏（清除缓冲区） |
| `⌃ + L` | 清屏（保留缓冲区） |
| `⌃ + U` | 清除当前行 |
| `⌃ + A` | 移动到行首 |
| `⌃ + E` | 移动到行尾 |
| `⌃ + W` | 删除前一个单词 |

### 光标移动

| 快捷键 | 功能 |
|--------|------|
| `⌃ + A` | 行首 |
| `⌃ + E` | 行尾 |
| `⌥ + ←` | 向左跳一个词（需配置） |
| `⌥ + →` | 向右跳一个词（需配置） |
| `⌃ + F` | 向前一个字符 |
| `⌃ + B` | 向后一个字符 |

### 其他

| 快捷键 | 功能 |
|--------|------|
| `⌘ + ,` | 打开偏好设置 |
| `⌘ + ;` | 自动补全 |
| `⌘ + Shift + H` | 粘贴板历史 |
| `⌘ + Option + B` | 即时回放 |
| `⌘ + U` | 切换透明度 |
| `⌘ + /` | 高亮光标位置 |
| `⌘ + Alt + E` | 所有标签内容搜索 |

---

## 高级功能

### Arrangements（窗口布局保存）

保存并恢复窗口布局，适合固定工作流：

```
Window → Save Window Arrangement
Window → Restore Window Arrangement
```

设置启动时自动恢复：
```
Settings → General → Startup → Open Arrangement
```

### Coprocess（协同进程）

将终端输出管道到另一个程序，实现高级自动化：

```
Shell → Run Coprocess...
```

### Python API 自动化

iTerm2 提供完整的 Python API 用于脚本自动化：

```python
#!/usr/bin/env python3
import iterm2

async def main(connection):
    app = await iterm2.async_get_app(connection)
    window = app.current_terminal_window
    if window:
        tab = await window.async_create_tab()
        session = tab.current_session
        await session.async_send_text("echo Hello iTerm2\n")

iterm2.run_until_complete(main)
```

脚本存放路径：`~/Library/Application Support/iTerm2/Scripts/`

### SSH 配置集成

在 `.ssh/config` 中配合 iTerm2 Profile 使用：

```
Settings → Profiles → 创建 "Remote" Profile
→ Command: ssh user@hostname
→ 设置特定颜色方案（如红色边框提醒当前在远程）
```

### 与 tmux 集成

```bash
# 使用 iTerm2 原生模式连接 tmux
tmux -CC        # 新建 tmux 会话（iTerm2 原生集成模式）
tmux -CC attach # 连接已有会话
```

---

## 常见问题

### Q: 字体图标显示为方块或乱码？

安装并设置 Nerd Font：

```bash
brew install --cask font-meslo-lg-nerd-font
# Settings → Profiles → Text → Font → 选择 MesloLGS NF
```

### Q: 颜色主题在 SSH 远程机器上不生效？

确保远程机器的终端类型设置正确：

```bash
# 本地 ~/.zshrc 或 ~/.bashrc 添加
export TERM=xterm-256color
```

### Q: Option 键无法跳词？

按照 [Keys 章节](#keys快捷键) 中的说明，在 Key Mappings 中手动添加 `⌥+←` 和 `⌥+→` 的 Escape Sequence 映射。

### Q: 如何导出/同步配置？

```bash
# 导出配置
defaults export com.googlecode.iterm2 ~/iterm2-backup.plist

# 导入配置
defaults import com.googlecode.iterm2 ~/iterm2-backup.plist
```

或使用内置的配置文件功能：
```
Settings → General → Settings → Load preferences from a custom folder or URL
```
指定一个 iCloud Drive 或 Git 仓库目录，实现多机同步。

### Q: 如何彻底重置 iTerm2 设置？

```bash
defaults delete com.googlecode.iterm2
```

---

## 推荐工具链

完整的高效终端工作流推荐：

| 工具 | 用途 | 安装 |
|------|------|------|
| iTerm2 | 终端模拟器 | `brew install --cask iterm2` |
| Oh My Zsh | Zsh 框架 | `sh -c "$(curl -fsSL ...)"` |
| Powerlevel10k | Shell 主题 | `brew install romkatv/powerlevel10k/powerlevel10k` |
| zsh-autosuggestions | 命令建议 | Git clone |
| zsh-syntax-highlighting | 语法高亮 | Git clone |
| fzf | 模糊搜索 | `brew install fzf` |
| bat | 增强版 cat | `brew install bat` |
| eza | 增强版 ls | `brew install eza` |
| ripgrep | 快速搜索 | `brew install ripgrep` |
| tldr | 简化版 man | `brew install tldr` |
| zoxide | 智能 cd | `brew install zoxide` |

---

## 参考资源

- [iTerm2 官方文档](https://iterm2.com/documentation.html)
- [Oh My Zsh 官网](https://ohmyz.sh)
- [Powerlevel10k GitHub](https://github.com/romkatv/powerlevel10k)
- [Nerd Fonts](https://www.nerdfonts.com)
- [iTerm2 Color Schemes](https://iterm2colorschemes.com)

---

*最后更新：2026-03-09*
