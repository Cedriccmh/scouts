# Scouts - 代码库智能调查系统

> 基于语义检索的并行代码探索框架，用于快速理解复杂代码库

## 💡 核心理念

Scouts 通过**规划-探索-整合**的三层架构，帮助你系统化地调查和理解代码库：

```
Memory Bank Index (知识中枢)
        ↓ 指针引导
    withScout (规划者) ── 分解任务 → 提供导航提示
        ↓
    Scout × N (调查者) ── 语义检索 → 按需深度探索  
        ↓
    综合报告 (知识沉淀)
```

### 关键特性

- 🎯 **语义优先检索**：理解意图而非仅匹配关键词
- 🔄 **迭代式收敛**：通过多轮精炼逐步深入
- 🤝 **并行协作**：2-3 个 scout 同时探索不同区域
- 📚 **知识复用**：基于索引的按需加载，避免信息过载
- 📊 **结构化输出**：标准化报告格式，易于整合

## 🚀 快速开始

### 基础用法

```
/withScout 调查项目的认证流程，找出在哪里添加 JWT 刷新功能
```

系统会自动：
1. 检查 Memory Bank 索引，提取相关知识指针
2. 根据任务类型（Bug/Feature/Refactor）优化搜索策略
3. 并行部署 scouts 进行深度调查
4. 生成个体报告和综合报告

### 使用示例

#### 示例 1：Bug 调查（优先使用 SvnLog）
```
/withScout 用户登录后偶尔出现 session 失效，调查可能的原因
```

**预期输出**：
- Scout A 调查近期 session 相关代码变更
- Scout B 调查 session 管理和过期逻辑
- 综合报告定位问题代码和历史修改记录

#### 示例 2：功能开发（优先使用 ProjectWiki）
```
/withScout 调查现有的支付流程架构，为集成新支付网关做准备
```

**预期输出**：
- Scout A 分析支付模块接口和抽象层
- Scout B 研究现有支付网关集成模式
- 综合报告提供集成点建议和设计参考

#### 示例 3：代码重构（综合使用所有数据源）
```
/withScout 分析用户模块的耦合情况，评估拆分为微服务的可行性
```

**预期输出**：
- Scout A 扫描跨模块依赖和调用关系
- Scout B 分析历史演化和当前架构设计
- 综合报告提供耦合点分析和拆分建议

#### 示例 4：技术栈迁移
```
/withScout 调查项目中所有使用 jQuery 的地方，评估迁移到 React 的工作量
```

**预期输出**：
- Scout A 定位所有 jQuery 使用点
- Scout B 分析依赖和交互模式
- 综合报告估算迁移范围和风险点

#### 示例 5：性能优化
```
/withScout 调查数据库查询热点，找出 N+1 查询和慢查询的位置
```

**预期输出**：
- Scout A 分析 ORM 使用模式
- Scout B 追踪数据库调用链
- 综合报告列出优化建议和具体位置

### 报告位置

- **Scout 报告**：`.kilocode/sub-memory-bank/scout/yy-mm-dd-[topic].md`
- **综合报告**：`.kilocode/sub-memory-bank/report/yy-mm-dd-[topic].md`

## 📁 知识生态

```
.kilocode/
├── rules/memory-bank/index.md    # 知识索引（指针中枢）
├── ProjectWiki/                   # 架构文档、API 规范
├── SvnLog/                        # 版本历史、变更记录
└── sub-memory-bank/
    ├── report/                    # 综合调查报告
    ├── scout/                     # 单个 scout 报告
    └── [modules]/                 # 模块特定知识
```

### 职责分离

| 角色 | 职责 |
|------|------|
| **Memory Bank Index** | 知识中枢，提供导航指针 |
| **withScout** | 规划者：读索引 → 分解任务 → 整合报告 |
| **Scout** | 调查者：接收指引 → 深度探索 → 生成证据 |
| **Recorder** (未来) | 知识管理者：提炼发现 → 更新索引 |

## 🎓 核心原则

1. **按需加载**：根据 index 指针按需深度探索，避免上下文腐烂
2. **语义优先**：语义检索 → 符号精炼 → 精准读取
3. **职责清晰**：规划者提供导航，调查者执行探索
4. **索引中心**：知识通过 index 路由，而非全量扫描

## 📖 详细文档

- **[commands/withScout.md](commands/withScout.md)** - 完整工作流程、职责边界、模板
- **[agents/scout.md](agents/scout.md)** - Scout 代理的详细行为规范
- **[hybrid-search-workflow.md](hybrid-search-workflow.md)** - 语义优先检索指南
- **[scouts-system-design.md](scouts-system-design.md)** - 系统架构和设计原则

## ⚡ 适用场景

| 场景 | 推荐任务类型 | 优先数据源 |
|------|------------|-----------|
| 定位 Bug | Bug/Debug | Codebase + SvnLog (近期变更) |
| 开发新功能 | Feature Development | Codebase + ProjectWiki (设计文档) |
| 代码重构 | Refactoring | Codebase + ProjectWiki + SvnLog |

## 🔧 工作流程

```
Phase 0: Lightweight Pre-Check
  withScout 读 index → 提取指针

Phase 1: Task Decomposition  
  识别任务类型 → 分解为并行任务 → 准备 Known Information

Phase 2: Deep Investigation
  Scouts 接收导航提示 → 语义检索 → 按需加载 → 生成报告

Phase 3: Synthesis
  整合所有 scout 报告 → 建立跨区域连接 → 生成综合报告

Phase 4: Knowledge Update (由 recorder 处理)
  提炼发现 → 更新 index → 为未来提供导航
```

---

**开始使用**：直接运行 `/withScout [你的调查目标]` 即可启动智能代码调查！

