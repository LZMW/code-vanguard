# Code Vanguard 团队安装指南

> **团队名称**：code-vanguard
> **团队类型**：混合型（支持串行/并行/混合执行）
> **配置包版本**：3.0

---

## 📦 安装步骤

### 步骤 1️⃣：安装协调器 Skill

协调器是团队的入口，必须先安装。

**文件位置**：
```
skills/code-vanguard-coordinator/skill.md
```

**安装位置**：
```
%USERPROFILE%\.claude\skills\code-vanguard-coordinator\skill.md
```

**操作**：
1. 复制 `skills/code-vanguard-coordinator/skill.md`
2. 粘贴到 `C:\Users\Mr.Chen\.claude\skills\code-vanguard-coordinator\skill.md`
3. 如需覆盖现有文件，请先备份

---

### 步骤 2️⃣：安装专家 Agent 配置

安装所有 4 位专家成员的配置。

**文件位置**：
```
agents/
├── code-vanguard-phoenix.md    # 架构师
├── code-vanguard-viper.md      # 开发者
├── code-vanguard-ghost.md      # 测试专家
└── code-vanguard-oracle.md     # 创新者
```

**安装位置**：
```
%USERPROFILE%\.claude\agents\
├── code-vanguard-phoenix.md
├── code-vanguard-viper.md
├── code-vanguard-ghost.md
└── code-vanguard-oracle.md
```

**操作**：
1. 复制 `agents/` 目录下所有 `.md` 文件
2. 粘贴到 `C:\Users\Mr.Chen\.claude\agents\` 目录
3. 如需覆盖现有文件，请先备份

---

### 步骤 3️⃣：验证安装

安装完成后，验证配置是否正确。

**验证方法**：
```markdown
# 触发协调器测试
用户: 帮我设计一个用户认证系统
协调器: 我是 Code Vanguard 协调器，我将协调团队完成此任务...
```

**验证清单**：
- [ ] 协调器能正确响应
- [ ] 协调器显示团队成员列表
- [ ] 协调器能触发专家 agent
- [ ] 专家 agent 能正常工作

---

## 🔍 配置文件说明

### 协调器配置

**文件**：`skills/code-vanguard-coordinator/skill.md`

**关键字段**：
```yaml
---
name: code-vanguard-coordinator
description: Code Vanguard (代码先锋) team coordinator skill...
---

# 以下是协调器的正文内容
# 包含核心原则、执行流程、MCP 授权机制等
```

**要点**：
- `name` 必须是 `code-vanguard-coordinator`
- `description` 不使用双引号（Skill 与 Agent 不同）
- 正文包含完整的协作流程规范

---

### 专家配置

**文件**：`agents/code-vanguard-[expert].md`

**关键字段**：
```yaml
---
name: code-vanguard-phoenix
description: "Use this agent when you need to..."
tools:
  - Read
  - Glob
  - Grep
  - Write
  - Edit
  - Bash
  - mcp__sequential-thinking__sequentialthinking
model: sonnet
---

# 以下是专家的正文内容
# 包含核心能力、信息传递机制、调度指令理解等
```

**要点**：
- `name` 格式：`code-vanguard-[expert-name]`
- `description` **必须使用双引号**
- `tools` 声明可用的工具（包括 MCP 工具）
- 正文包含信息传递机制和调度指令理解

---

## 📋 配置检查清单

安装完成后，请确认以下各项：

### 协调器检查

- [ ] 文件路径正确：`%USERPROFILE%\.claude\skills\code-vanguard-coordinator\skill.md`
- [ ] name 字段正确：`code-vanguard-coordinator`
- [ ] description 不使用双引号
- [ ] description 包含模式标识：`using both sequential and parallel execution`
- [ ] 核心原则完整（委托优先、自然语言触发、用户优先等）
- [ ] 执行流程清晰（5 步流程）
- [ ] MCP 授权机制完整
- [ ] 三种触发格式完整（串行/并行/混合）

### 专家检查

- [ ] 文件路径正确：`%USERPROFILE%\.claude\agents\code-vanguard-*.md`
- [ ] name 格式正确：`code-vanguard-[expert]`
- [ ] description 使用双引号
- [ ] description 长度在 200-350 字符
- [ ] description 使用 `<example>` 标签
- [ ] description 包含 `Uses Task tool to launch...`
- [ ] tools 字段包含 MCP 工具声明
- [ ] 正文包含信息传递机制
- [ ] 正文包含调度指令理解章节

### 团队一致性检查

- [ ] 专家数量 2-6 个（本团队 4 个）
- [ ] 专家名称带团队前缀 `code-vanguard-`
- [ ] 成员触发词不重叠
- [ ] MCP 能力与协调器速查表一致
- [ ] 信息传递机制符合混合型团队

---

## 🚨 常见问题

### Q1: 协调器无法触发专家？

**可能原因**：
- 专家配置文件未正确安装
- 专家 `name` 字段与协调器不一致

**解决方法**：
1. 检查 `C:\Users\Mr.Chen\.claude\agents\` 目录下是否有 `code-vanguard-*.md` 文件
2. 确认专家的 `name` 字段与协调器触发指令中的一致

---

### Q2: MCP 工具无法使用？

**可能原因**：
- 协调器未授权 MCP 工具
- MCP 工具未在专家的 `tools` 字段中声明

**解决方法**：
1. 确认专家的 `tools` 字段包含 MCP 工具
2. 协调器触发专家时需要明确授权 MCP 工具

---

### Q3: description 格式错误？

**可能原因**：
- Skill 的 description 使用了双引号
- Agent 的 description 未使用双引号

**解决方法**：
- **Skill（协调器）**：description 不使用双引号
- **Agent（专家）**：description 必须使用双引号

---

### Q4: 触发指令格式问题？

**协调器触发格式**：
```markdown
使用 code-vanguard-[expert] 子代理执行 [任务描述]
```

**错误格式**：
- ❌ 使用 code-vanguard-phoenix（缺少"子代理执行"）
- ❌ code-vanguard-phoenix 子代理执行（缺少"使用"）

**正确格式**：
- ✅ 使用 code-vanguard-phoenix 子代理执行设计架构

---

## 🔄 更新配置

如需更新现有配置：

1. **备份现有配置**
   ```bash
   # 备份协调器
   copy C:\Users\Mr.Chen\.claude\skills\code-vanguard-coordinator\skill.md backup_skill.md

   # 备份专家
   copy C:\Users\Mr.Chen\.claude\agents\code-vanguard-*.md backup_agents\
   ```

2. **复制新配置**
   - 将新配置文件复制到对应目录
   - 覆盖现有文件

3. **验证更新**
   - 触发协调器测试
   - 确认专家正常工作

---

## 📞 支持

如遇到问题，请检查：

1. **文件路径**是否正确
2. **配置格式**是否符合规范
3. **描述字段**是否正确（双引号/无双引号）
4. **tools 字段**是否包含所需工具

---

## ✅ 安装完成

安装完成后，Code Vanguard 团队即可使用。

**使用示例**：
```markdown
用户: 我需要一个完整的微服务架构设计
协调器: 我将协调 Code Vanguard 团队完成此任务...

=== 需求沟通 ===
[协调器与用户确认需求...]

=== 模式识别 ===
执行模式：混合模式

=== 任务规划 ===
阶段1（串行）：Phoenix 设计架构
阶段2（并行）：Viper 实现核心功能、Ghost 设计测试框架
阶段3（串行）：Ghost 完整测试

=== 触发专家 ===
使用 code-vanguard-phoenix 子代理执行架构设计...
```

---

**🎉 安装成功！祝使用愉快！**
