## 一、系统架构概览

### 整体架构

```
┌──────────────────────────────────────────────────────┐
│  Knowledge Ecosystem (.kilocode/)                    │
│  ├── rules/memory-bank/index.md (中心索引)          │
│  │   └── 指向: ProjectWiki, SvnLog, past reports   │
│  ├── ProjectWiki/ (架构文档、API规范、设计决策)     │
│  ├── SvnLog/ (版本历史、提交记录、变更模式)         │
│  └── sub-memory-bank/                               │
│      ├── report/ (综合调查报告)                     │
│      ├── scout/ (单个scout报告)                    │
│      └── [modules]/ (模块特定知识)                 │
└──────────────────────────────────────────────────────┘
                    ↓ index pointers
        ┌───────────────────────┐
        │   withScout           │  ← 协调层 (Planner)
        │   - 读index获取指针   │
        │   - 任务分解          │
        │   - 准备导航提示      │
        │   - 报告整合          │
        └───────────────────────┘
                    ↓ navigation hints
        ┌───────────────────────┐
        │   scout × N           │  ← 执行层 (Investigators)
        │   - 接收Known Info    │
        │   - 按需深度加载      │
        │   - 语义优先检索      │
        │   - 生成个体报告      │
        └───────────────────────┘
```

### 职责边界

| 活动 | withScout | Scout |
|------|-----------|-------|
| **读 Memory Bank Index** | ✅ 轻量级读取，提取指针 | ⚠️ 仅当 Known Info 不足 |
| **浏览 ProjectWiki** | ❌ 不直接浏览 | ✅ 按需加载（index/任务指引） |
| **浏览 SvnLog** | ❌ 不直接浏览 | ✅ 按需加载（index/任务指引） |
| **语义代码检索** | ❌ 不直接检索 | ✅ 核心职责 |
| **报告整合** | ✅ 整合所有scout报告 | ❌ 只生成单个报告 |

### 信息流

```
Phase 0: Lightweight Pre-Check
  withScout 读 index → 提取指针和已知发现
    ↓
Phase 1: Task Decomposition
  withScout 分解任务 → 准备结构化 Known Information
    ↓
Phase 2: Deep Investigation
  Scouts 接收导航提示 → 按需深度加载 → 语义检索 → 生成报告
    ↓
Phase 3: Synthesis
  withScout 整合所有scout报告 → 生成综合报告
    ↓
Phase 4: Knowledge Update (由专门的 recorder 处理)
  更新 index.md → 创建新的指针 → 为未来调查提供导航
```

---

## 二、检索策略配置

### 任务类型与策略

| 任务类型 | 检索重点 | 数据源优先级 |
| --- | --- | --- |
| **Bug 定位类** | 调用关系、最近提交记录 | Codebase (调用链) + SvnLog (近期变更) |
| **功能开发类** | 文档、接口定义 | Codebase (接口) + ProjectWiki (设计文档) |
| **重构类** | 跨模块依赖扫描 | Codebase (依赖) + ProjectWiki (原始意图) + SvnLog (演化历史) |

系统根据任务类型自动优化检索策略和数据源选择。

---

## 三、检索流程

### 1. 并行语义检索（Semantic-First Hybrid Search）

检索范围包括：

- **代码库（Codebase）**：源代码文件和配置
- **项目文档（ProjectWiki）**：`.kilocode/ProjectWiki/` - 架构文档、API规范、设计决策
- **版本历史（SvnLog）**：`.kilocode/SvnLog/` - SVN提交记录、变更模式、历史修复
- **记忆库（Memory Bank）**：`.kilocode/rules/memory-bank/` - 已发现的模块关系和模式
- **过往调查（Sub-Memory-Bank）**：`.kilocode/sub-memory-bank/` - 之前的报告和发现
- 明确检索文件类型范围（文件夹、文件扩展名）

**检索策略**：语义检索（意图理解）→ 符号精炼（关键词匹配）→ 精准读取（特定行范围）

### 2. 语义聚类与摘要生成

对检索结果进行语义聚类，自动生成摘要（Summary），帮助快速理解上下文。

### 3. 关键词与正则匹配

在语义检索基础上，辅以高精度关键词与正则匹配机制，确保细粒度命中。

### 4. 迭代式搜索

根据初次搜索结果自动展开迭代检索：

- 发现新依赖/重要关键字或遗漏的上下文
- 动态更新查询范围与权重

### 5. Human-in-the-loop #顶层，不涉及scouts

在遇到无法确定某段内容是否相关的情况时，系统主动提问用户，以人类反馈为信号，优化检索方向。

### 6. 日志与指标记录（可观测）#暂不实现

每次检索都记录性能指标：

- 检索延迟（Latency）
- 准确率 (Precise)
- 迭代次数（Iteration Count）

这些数据用于持续优化模型与策略。

### 7. 报告生成与知识沉淀

**调查报告保存**（由 withScout 和 scouts 负责）：

- **个体 Scout 报告**：`.kilocode/sub-memory-bank/scout/yy-mm-dd-[topic].md`
  - 包含元数据、代码段、结论、关系、结果、注意事项
  - 新发现的函数、类、模块关系
  - 依赖边与调用路径
  - 由各个 scout 生成
  
- **综合调查报告**：`.kilocode/sub-memory-bank/report/yy-mm-dd-[topic].md`
  - 整合所有 scout 发现
  - 跨区域连接和可操作建议
  - 部署历史和证据轨迹
  - 由 withScout 整合生成

**Knowledge Bank 更新**（由专门的 recorder 处理，非本系统职责）：
  - 将重要发现提炼到 `.kilocode/rules/memory-bank/index.md`
  - 创建指向新报告的指针
  - 更新架构图和模块关系图
  - 为未来调查提供导航提示

---

## 四、核心设计原则

### 1. 按需加载，避免上下文腐烂
- withScout 只读 index，不直接浏览 ProjectWiki/SvnLog
- Scouts 根据 index 指针和任务需求，按需深度加载
- 避免每次都加载大量可能无关的历史信息

### 2. 职责分离，清晰边界
- **withScout = 规划者**：读索引、分解任务、整合报告
- **Scout = 调查者**：接收指引、深度探索、生成证据
- **Recorder = 知识管理者**：提炼发现、更新索引、维护知识库（未来实现）

### 3. 索引中心化，智能路由
- Memory Bank Index 作为知识中枢
- 提供指针而非全量内容
- 引导而非限制探索路径

### 4. 语义优先，混合检索
- 语义检索（意图理解）→ 符号精炼（关键词）→ 精准读取（行范围）
- 避免纯关键词搜索的局限性
- 保留符号搜索的精确性

---

## 五、相关文档

- **命令配置**：`commands/withScout.md` - 完整的工作流程、职责边界、模板
- **Agent 提示词**：`agents/scout.md` - Scout 代理的详细行为规范和搜索策略
- **混合检索策略**：`hybrid-search-workflow.md` - 语义优先检索指南