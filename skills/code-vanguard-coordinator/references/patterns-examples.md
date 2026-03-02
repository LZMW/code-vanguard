# 协作模式参考示例

本文档提供 Code Vanguard 团队的详细协作模式示例，供协调器在执行任务时参考。

---

## 模式1：单专家独立完成

### 适用场景
- 简单任务，单一职责
- 任务复杂度低（< 100行代码）
- 不需要跨领域协作

### 示例

**用户需求**：
```
写一个 Python 快速排序函数
```

**协调器分析**：
- 任务类型：简单编码
- 复杂度：低
- 涉及领域：单一（编码）
- 协作模式：单专家

**执行流程**：
```
1. 协调器识别需求 → 简单编码任务
2. 选择专家：Viper（开发者）
3. 触发 Viper 执行编码任务
4. Viper 输出可运行代码 + 使用示例
5. 协调器汇总交付
```

**触发指令**：
```yaml
subagent_type: "code-vanguard-viper"
description: "实现快速排序函数"
prompt: |
  任务：实现一个 Python 快速排序函数

  **📋 输出要求**:
  - 可运行的 Python 代码
  - 函数文档字符串
  - 使用示例
```

---

## 模式2：链式协作（串行）

### 适用场景
- 任务有强依赖关系
- 需要顺序执行（设计→实现→测试）
- 后续步骤依赖前置步骤产出

### 示例

**用户需求**：
```
帮我设计并实现一个用户登录 API，包含测试用例
```

**协调器分析**：
- 任务类型：完整项目
- 复杂度：中
- 涉及领域：架构 + 编码 + 测试
- 协作模式：链式协作

**执行流程**：
```
=== 链式协作模式 ===

# 阶段1：架构设计
Phoenix 设计 API 架构
  输出：.codevanguard/phases/01_architecture/INDEX.md

# 阶段2：功能实现（依赖阶段1）
Viper 实现登录 API
  输入：读取 01_architecture/INDEX.md
  输出：.codevanguard/phases/02_implementation/INDEX.md

# 阶段3：质量测试（依赖阶段2）
Ghost 编写测试用例
  输入：读取 02_implementation/INDEX.md
  输出：.codevanguard/phases/03_testing/INDEX.md

# 汇总交付
协调器整合所有产出，交付用户
```

**触发指令序列**：

```yaml
# 阶段1
subagent_type: "code-vanguard-phoenix"
description: "设计用户登录API架构"
prompt: |
  **📂 阶段路径**:
  - 阶段目录: .codevanguard/phases/01_architecture/
  - 消息文件: .codevanguard/inbox.md

  **📋 输出要求**:
  - INDEX.md: 必须创建（概要+架构图+技术选型）

---
# 阶段2
subagent_type: "code-vanguard-viper"
description: "实现用户登录API"
prompt: |
  **📂 阶段路径**:
  - 阶段目录: .codevanguard/phases/02_implementation/
  - 前序索引: .codevanguard/phases/01_architecture/INDEX.md（请先读取！）
  - 消息文件: .codevanguard/inbox.md

  **📋 输出要求**:
  - INDEX.md: 必须创建（概要+代码文件清单）

---
# 阶段3
subagent_type: "code-vanguard-ghost"
description: "编写测试用例"
prompt: |
  **📂 阶段路径**:
  - 阶段目录: .codevanguard/phases/03_testing/
  - 前序索引: .codevanguard/phases/02_implementation/INDEX.md（请先读取！）
  - 消息文件: .codevanguard/inbox.md

  **📋 输出要求**:
  - INDEX.md: 必须创建（概要+测试用例清单+覆盖率）
```

---

## 模式3：并行协作

### 适用场景
- 任务相互独立，无依赖关系
- 需要多视角同时分析
- 可以同时执行多个子任务

### 示例

**用户需求**：
```
同时实现用户模块、订单模块和支付模块
```

**协调器分析**：
- 任务类型：多模块并行开发
- 复杂度：中
- 涉及领域：编码（多个独立模块）
- 协作模式：并行协作

**执行流程**：
```
=== 并行协作模式 ===

同时触发以下专家，独立完成各自任务：

# 专家1：Viper - 用户模块
Viper 实现用户模块
  输出：.codevanguard/outputs/viper-user/output.md

# 专家2：Viper - 订单模块
Viper 实现订单模块
  输出：.codevanguard/outputs/viper-order/output.md

# 专家3：Viper - 支付模块
Viper 实现支付模块
  输出：.codevanguard/outputs/viper-payment/output.md

等待所有专家完成后...
协调器汇总所有产出，交付用户
```

**触发指令**：
```yaml
# 同时触发（在一次消息中发送多个 Task 调用）

# 专家1
subagent_type: "code-vanguard-viper"
description: "实现用户模块"
prompt: |
  **📂 产出路径**:
  - 产出目录: .codevanguard/outputs/viper-user/
  - 消息文件: .codevanguard/inbox.md

  **📋 输出要求**:
  - output.md: 完成文档
  - COMPLETE 消息: 发送到 inbox.md

---
# 专家2
subagent_type: "code-vanguard-viper"
description: "实现订单模块"
prompt: |
  **📂 产出路径**:
  - 产出目录: .codevanguard/outputs/viper-order/
  - 消息文件: .codevanguard/inbox.md

  **📋 输出要求**:
  - output.md: 完成文档
  - COMPLETE 消息: 发送到 inbox.md

---
# 专家3
subagent_type: "code-vanguard-viper"
description: "实现支付模块"
prompt: |
  **📂 产出路径**:
  - 产出目录: .codevanguard/outputs/viper-payment/
  - 消息文件: .codevanguard/inbox.md

  **📋 输出要求**:
  - output.md: 完成文档
  - COMPLETE 消息: 发送到 inbox.md
```

---

## 模式4：顾问式协作

### 适用场景
- 需要先调研再实现
- 技术选型不确定
- 需要专家咨询支持

### 示例

**用户需求**：
```
实现一个高性能缓存系统，不确定用什么技术方案
```

**协调器分析**：
- 任务类型：调研 + 实现
- 复杂度：中
- 涉及领域：调研 + 编码
- 协作模式：顾问式协作

**执行流程**：
```
=== 顾问式协作模式 ===

# 阶段1：技术调研
Oracle 调研缓存技术方案
  输出：.codevanguard/outputs/oracle/output.md（技术选型建议）

# 阶段2：基于调研实现
Viper 实现缓存系统
  输入：读取 oracle/output.md
  输出：.codevanguard/phases/02_implementation/INDEX.md

# 汇总交付
协调器整合调研结果和实现代码，交付用户
```

---

## 模式5：混合协作

### 适用场景
- 部分串行、部分并行
- 复杂项目需要灵活调整
- 某些步骤依赖前置步骤，但后续可并行

### 示例

**用户需求**：
```
设计并实现一个完整的用户认证系统，需要调研OAuth方案，同时要有测试用例
```

**协调器分析**：
- 任务类型：完整项目 + 技术调研
- 复杂度：高
- 涉及领域：架构 + 调研 + 编码 + 测试
- 协作模式：混合协作

**执行流程**：
```
=== 混合协作模式 ===

# 阶段1：串行准备（架构设计）
Phoenix 设计认证系统架构
  输出：.codevanguard/phases/01_architecture/INDEX.md

等待完成...

# 阶段2：并行执行（基于架构设计）
同时触发以下专家：

## 专家2：Viper - 核心模块实现
  输入：读取 01_architecture/INDEX.md
  输出：.codevanguard/phases/02_implementation/INDEX.md

## 专家3：Oracle - OAuth方案调研
  输入：读取 01_architecture/INDEX.md
  输出：.codevanguard/outputs/oracle/output.md

等待所有专家完成...

# 阶段3：串行汇总（质量测试）
Ghost 测试和安全审计
  输入：读取 02_implementation/INDEX.md 和 oracle/output.md
  输出：.codevanguard/phases/03_testing/INDEX.md

# 汇总交付
协调器整合所有产出，交付用户
```

---

## MCP授权示例

### 示例1：架构设计任务（需要深度思考）

```markdown
🔓 MCP 授权（用户已同意）：

🔴 必要工具（请**优先使用**）：
- mcp__sequential-thinking__sequentialThinking: 深度思考推导架构决策
💡 使用建议：遇到复杂架构决策时请调用此工具，使用第一性原理分析

🟡 推荐工具（**建议主动使用**）：
- mcp__context7__query-docs: 查询技术文档
💡 使用建议：需要了解新技术栈的最佳实践时使用此工具
```

### 示例2：技术调研任务（需要网络搜索）

```markdown
🔓 MCP 授权（用户已同意）：

🔴 必要工具（请**优先使用**）：
- mcp__web-search-prime__webSearchPrime: 网络搜索技术方案
- mcp__web-reader__webReader: 读取技术文章
💡 使用建议：调研新技术时请调用这些工具，获取最新信息

🟡 推荐工具（**建议主动使用**）：
- mcp__context7__query-docs: 查询技术文档
- mcp__sequential-thinking__sequentialThinking: 深度思考推导
💡 使用建议：需要深入分析时使用

🟢 可选工具（如有需要可使用）：
- mcp__zread__search_doc: 搜索 GitHub 仓库文档
💡 使用建议：如果需要参考开源项目实现，可以使用此工具
```

---

## 消息格式参考

### inbox.md 消息格式

```markdown
# 代码先锋 消息收件箱

## 2026-03-02 10:30:00
[10:30:00] phoenix STATUS: 架构设计完成
产出文件：.codevanguard/phases/01_architecture/INDEX.md
摘要：完成微服务架构设计，采用事件驱动模式

## 2026-03-02 10:35:00
[10:35:00] viper COMPLETE: 核心模块实现完成
产出文件：.codevanguard/phases/02_implementation/INDEX.md

## 2026-03-02 10:40:00
[10:40:00] oracle DISCOVERY: 发现更优的缓存方案
内容：Redis Cluster 比 Sentinel 更适合当前场景
影响：建议调整架构设计中的缓存方案

## 2026-03-02 10:45:00
[10:45:00] ghost WARNING: 发现潜在安全风险
内容：认证接口缺少速率限制
影响：建议在实现阶段添加限流机制
```

---

## 决策树总结

```
用户任务
    │
    ├─ 简单任务（单一职责）─────────────────→ 单专家
    │
    ├─ 有强依赖关系
    │   ├─ 设计→实现→测试 ─────────────────→ 链式协作
    │   └─ 调研→实现 ──────────────────────→ 顾问式
    │
    ├─ 完全独立任务
    │   └─ 多模块同时开发 ─────────────────→ 并行协作
    │
    └─ 部分串行+部分并行
        └─ 复杂项目 ───────────────────────→ 混合协作
```
