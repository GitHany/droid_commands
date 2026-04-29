# .factory 目录说明

本文档介绍 `F:\droid_commands\.factory` 目录的功能和自定义命令实现。

## 目录结构

```
.factory/
├── commands/          # 自定义命令配置
│   ├── hc1.md        # 苏格拉底式需求沟通命令
│   └── hc2.md        # TDD 实现执行命令
└── droids/           # 自定义子代理配置
    ├── bug-analyzer.md       # Bug 根因分析代理
    ├── code-reviewer.md      # 代码审查代理
    ├── codebase-explorer.md  # 代码库探索代理
    ├── implementation-worker.md  # TDD 实现工作代理
    └── task-planner.md       # 任务规划代理
```

---

## 自定义命令 (commands/)

### /hc1 — 苏格拉底式需求沟通

**文件**: `commands/hc1.md`

**功能**: 通过苏格拉底式提问和三维评分系统彻底理解用户需求，输出结构化需求文档。

**核心特性**:
- 一次一问原则
- 三维评分驱动（Goal Clarity 40%, Constraint Clarity 30%, Success Criteria 30%）
- 歧义度量化评估（需降至 20% 以下）
- 质疑假设和挑战环节
- 支持 Brownfield/Greenfield 两种项目类型

**使用方式**:
```
/hc1 <你的想法或需求描述>
```

**工作流程**:
1. Phase 0: 代理准备（Brownfield 项目检测和代码探索）
2. Phase 1: 初始化和访谈开始
3. Phase 2: 苏格拉底式访谈（循环提问和评分）
4. Phase 3: 确认与输出需求文档

**输出**: `.workbuddy/specs/hc1-{timestamp}.md`

---

### /hc2 — TDD 实现执行

**文件**: `commands/hc2.md`

**功能**: 基于需求文档执行完整的 TDD 实现、测试、调试和反馈流程。

**核心特性**:
- TDD 铁律：先写失败测试，再写最小实现
- 最小改动原则
- 四阶段调试法
- 变更蔓延检测
- 可选派发子代理执行并行任务

**使用方式**:
```
/hc2 <需求文档路径或直接描述>
```

**工作流程**:
1. Phase 0: 并行代理准备（codebase-explorer + task-planner）
2. Phase 1: 读取与分解
3. Phase 2: 逐项实现（TDD 串行模式）
4. Phase 3: 并行执行（Task tool 派发）
5. Phase 4: Bug 处理（四阶段调试）
6. Phase 5: 代码审查
7. Phase 6: 最终报告

---

## 自定义子代理 (droids/)

### bug-analyzer — Bug 根因分析代理

**文件**: `droids/bug-analyzer.md`

**功能**: 深入分析 Bug 根因，追踪数据流，对比正常代码模式，提出根因假设。

**工具权限**: read-only

**工作流程**:
1. 错误解析
2. 数据流追踪
3. 模式对比
4. 最近变更检查
5. 根因假设形成

---

### code-reviewer — 代码审查代理

**文件**: `droids/code-reviewer.md`

**功能**: 审查代码变更的正确性、安全性、可维护性和性能。

**工具权限**: read-only

**审查维度**:
- 正确性（逻辑、边界条件、错误处理）
- 安全性（输入校验、注入风险、敏感数据）
- 可维护性（命名、单一职责、DRY）
- 性能（N+1、内存泄漏、算法复杂度）
- 测试覆盖

**输出级别**:
- 🔴 阻塞项（必须修复）
- 🟡 建议项（应该修复）
- 💭 小改进（锦上添花）

---

### codebase-explorer — 代码库探索代理

**文件**: `droids/codebase-explorer.md`

**功能**: 探索代码库结构、依赖关系和相关代码，输出结构化分析报告。

**工具权限**: read-only

**工作流程**:
1. 项目概览（技术栈、目录结构、入口文件）
2. 深度分析（文件职责、依赖关系、数据流向）
3. 质量评估（测试覆盖、技术债务、代码风格）
4. 关联发现（相关文件、可能受影响的模块）

---

### implementation-worker — TDD 实现工作代理

**文件**: `droids/implementation-worker.md`

**功能**: 接收主 Agent 分发的独立任务，按 TDD 流程完成实现。

**工具权限**: read, write, search, execute

**执行流程**:
1. 理解任务
2. 写失败测试
3. 写最小实现
4. 验证（测试 + 类型 + 构建）
5. 报告完成状态

---

### task-planner — 任务规划代理

**文件**: `droids/task-planner.md`

**功能**: 将需求拆解为原子任务，分析依赖关系，规划并行执行策略。

**工具权限**: read-only

**工作流程**:
1. 需求分解（功能模块 → 原子任务）
2. 依赖分析（任务依赖图、并行批次）
3. 风险评估（技术风险、阻塞项）
4. 执行策略（提交粒度、回滚策略）

---

## 参考项目

本项目参考了以下开源项目的设计和理念：

| 项目 | 仓库 | 描述 |
|------|------|------|
| andrej-karpathy-skills | [forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills) | 基于 Karpathy 技能的 AI 编程辅助框架 |
| OpenSpec | [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec) | AI Agent 协作规范和协议 |
| agency-agents-zh | [jnMetaCode/agency-agents-zh](https://github.com/jnMetaCode/agency-agents-zh) | AI Agent 代理框架中文指南 |
| oh-my-claudecode | [Yeachan-Heo/oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode) | Claude Code 增强框架 |
| superpowers | [obra/superpowers](https://github.com/obra/superpowers) | AI 编程超级能力扩展 |

---

## 设计理念

1. **TDD 驱动**: 所有实现任务遵循测试先行的开发流程
2. **最小改动**: 不做需求之外的事情，避免过度设计
3. **代理协作**: 通过子代理实现并行处理和专业化分工
4. **量化评估**: 用歧义度等指标量化需求清晰度和代码质量
5. **无废话沟通**: 直接提问和报告，减少无效交流

---

## 版本

当前版本: v1.0.0
