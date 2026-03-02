# 安装指南

本文档提供 Code Vanguard (代码先锋) 团队系统的详细安装步骤。

---

## 前置要求

- Claude Code 已安装并正常运行
- 有权访问 `~/.claude/` 目录（Windows: `C:\Users\{用户名}\.claude\`）

---

## 安装步骤

### 方法一：手动复制（推荐）

#### 1. 安装专家 Agent

将 `agents/` 目录下的所有 `.md` 文件复制到 Claude Code 的 agents 目录：

**Windows:**
```powershell
copy "agents\*.md" "%USERPROFILE%\.claude\agents\"
```

**macOS/Linux:**
```bash
cp agents/*.md ~/.claude/agents/
```

#### 2. 安装协调器 Skill

将整个 `skills/code-vanguard-coordinator/` 目录复制到 Claude Code 的 skills 目录：

**Windows:**
```powershell
xcopy /E /I "skills\code-vanguard-coordinator" "%USERPROFILE%\.claude\skills\code-vanguard-coordinator"
```

**macOS/Linux:**
```bash
cp -r skills/code-vanguard-coordinator ~/.claude/skills/
```

### 方法二：使用 Bash 一键安装

在项目根目录执行：

**Windows (Git Bash / PowerShell):**
```bash
# 创建目录（如果不存在）
mkdir -p "$HOME/.claude/agents"
mkdir -p "$HOME/.claude/skills"

# 复制 agents
cp agents/*.md "$HOME/.claude/agents/"

# 复制 skills
cp -r skills/code-vanguard-coordinator "$HOME/.claude/skills/"
```

**macOS/Linux:**
```bash
# 创建目录（如果不存在）
mkdir -p ~/.claude/agents
mkdir -p ~/.claude/skills

# 复制 agents
cp agents/*.md ~/.claude/agents/

# 复制 skills
cp -r skills/code-vanguard-coordinator ~/.claude/skills/
```

---

## 验证安装

### 1. 检查文件是否正确复制

**Windows:**
```powershell
dir "%USERPROFILE%\.claude\agents\code-vanguard-*.md"
dir "%USERPROFILE%\.claude\skills\code-vanguard-coordinator\skill.md"
```

**macOS/Linux:**
```bash
ls ~/.claude/agents/code-vanguard-*.md
ls ~/.claude/skills/code-vanguard-coordinator/skill.md
```

应该看到：
- `code-vanguard-phoenix.md`
- `code-vanguard-viper.md`
- `code-vanguard-ghost.md`
- `code-vanguard-oracle.md`
- `skill.md` (协调器)

### 2. 重启 Claude Code

安装后**必须**重启 Claude Code 会话才能加载新配置。

### 3. 测试安装

重启后，尝试以下命令测试是否正常工作：

```
/code-vanguard-coordinator 帮我设计一个简单的用户登录系统
```

如果协调器正确识别任务并开始分配专家，则安装成功。

---

## 卸载

如需卸载，删除对应文件即可：

**Windows:**
```powershell
del "%USERPROFILE%\.claude\agents\code-vanguard-*.md"
rmdir /S /Q "%USERPROFILE%\.claude\skills\code-vanguard-coordinator"
```

**macOS/Linux:**
```bash
rm ~/.claude/agents/code-vanguard-*.md
rm -rf ~/.claude/skills/code-vanguard-coordinator
```

---

## 常见问题

### Q1: 安装后没有生效？

**A:** 确保：
1. 文件复制到了正确的目录
2. 已经重启 Claude Code 会话
3. 文件名没有变化（保持 `code-vanguard-*.md` 格式）

### Q2: 协调器无法触发专家？

**A:** 检查：
1. 专家 agent 文件是否在 `~/.claude/agents/` 目录
2. 专家文件的 `name` 字段是否正确（如 `code-vanguard-phoenix`）
3. 协调器是否使用正确的 subagent_type 参数

### Q3: 如何更新到新版本？

**A:**
1. 删除旧文件（参考卸载步骤）
2. 复制新版本文件
3. 重启 Claude Code 会话

### Q4: 可以自定义专家配置吗？

**A:** 可以。编辑 `~/.claude/agents/` 目录下的 `.md` 文件即可自定义专家行为。但建议保留核心原则不变。

---

## 文件位置速查

| 组件 | 位置 |
|------|------|
| 专家 Agents | `~/.claude/agents/code-vanguard-*.md` |
| 协调器 Skill | `~/.claude/skills/code-vanguard-coordinator/skill.md` |
| 参考文档 | `~/.claude/skills/code-vanguard-coordinator/references/` |

---

## 下一步

安装完成后，请阅读 [README.md](README.md) 了解如何使用代码先锋团队。
