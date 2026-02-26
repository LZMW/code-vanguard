# 协作模式示例

> 这些是参考示例，协调器可根据实际情况自由组合或创新

> ⚠️ **重要**：必须使用自然语言触发专家 agent

## 示例1：单专家模式

**适用场景**：简单任务，单一专家可独立完成

**触发方式**：
```
使用 code-vanguard-phoenix 子代理设计系统架构
使用 code-vanguard-viper 子代理实现用户登录功能
使用 code-vanguard-ghost 子代理测试代码质量
使用 code-vanguard-oracle 子代理调研技术方案
```

## 示例2：链式协作（设计→实现→测试）

**适用场景**：完整项目开发，需要多阶段协作

**触发方式**：
```
步骤1: 使用 code-vanguard-phoenix 子代理设计系统架构...
       ↓ 获取架构设计文档

步骤2: 使用 code-vanguard-viper 子代理基于架构设计实现代码...
       ↓ 获取实现代码

步骤3: 使用 code-vanguard-ghost 子代理测试实现代码...
       ↓ 获取测试报告
```

## 示例3：并行协作

**适用场景**：多个独立模块同时开发

**触发方式**：
```
同时触发多个 Viper 子代理：
- 使用 code-vanguard-viper 子代理实现用户模块...
- 使用 code-vanguard-viper 子代理实现订单模块...
- 使用 code-vanguard-viper 子代理实现支付模块...

注意：并行触发时，每个任务描述要明确独立
```

## 示例4：顾问式协作

**适用场景**：主专家执行 + 顾问专家复核

**触发方式**：
```
步骤1: 使用 code-vanguard-viper 子代理实现算法...
步骤2: 使用 code-vanguard-oracle 子代理复核算法方案...
步骤3: 如有问题，再次触发 Viper 修正
```

## 示例5：动态调整

**场景**：执行中发现新问题

**应对**：
- 原计划单专家，发现需要架构设计 → 先触发 Phoenix
- 原计划链式，某环节简单 → 跳过或合并
- 发现技术难点 → 引入 Oracle 顾问
- 遇到复杂问题 → 使用 AskUserQuestion 与用户确认

## 示例6：通过 description 自动匹配

专家 agent 的 description 会自动匹配任务：

```
协调器输出任务描述：
"设计一个用户认证系统的架构"

系统自动匹配到 phoenix 的 description：
"System architecture designer expert. Use proactively when designing architecture..."
```

---

**关键**：
1. 必须使用自然语言触发
2. 每次触发后等待结果再进行下一步
3. 以上都是示例，协调器应保持灵活性
