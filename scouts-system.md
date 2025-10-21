# Scouts Search System

## Overview

Scouts is a parallel hybrid search engine optimized for large codebase understanding and analysis.

**Architecture:**

- Scouts operates with multiple "Intent Workers" (scout agents), each handling an independent search objective
- Each scout uses **semantic-first hybrid search** combining meaning-based and keyword-based retrieval
- Scouts can search across different domains in parallel:
  - **Codebase**: Source code and configuration files
  - **ProjectWiki**: `.kilocode/ProjectWiki/` - Architecture docs, API specs, design decisions
  - **SvnLog**: `.kilocode/SvnLog/` - Version control history, commit patterns
  - **Documentation**: All available documentation
- Results are consolidated into:
  - Individual scout reports: `.kilocode/sub-memory-bank/scout/yy-mm-dd-[topic].md`
  - Final comprehensive report: `.kilocode/sub-memory-bank/report/yy-mm-dd-[topic].md`

## When to Use Scouts

| Scenario | Use Case | Recommended Domains |
| --- | --- | --- |
| **Feature Design** | Understand current architecture and interfaces for better integration | Codebase (module interfaces) + ProjectWiki (design docs) |
| **Debugging** | Understand code execution flow to pinpoint issues | Codebase (call chains) + SvnLog (recent changes) |
| **Refactoring** | Understand runtime logic to design modification strategy | Codebase (dependencies) + ProjectWiki (original intent) + SvnLog (evolution) |

## Workflow

### 1. Create Search Task

Use the `/withScout` command with your investigation request. The system will:
- Analyze your goal and identify the task type (Bug/Feature/Refactor)
- Check existing knowledge in Memory Bank, ProjectWiki, and SvnLog
- Break down the task into parallel scout assignments
- Generate individual scout reports in `.kilocode/sub-memory-bank/scout/`
- Consolidate findings into a comprehensive report in `.kilocode/sub-memory-bank/report/`

**Example invocation**:
```
/withScout Investigate the authentication flow and identify where to add JWT refresh functionality
```

### 2. Scout Execution

The system automatically:
- Deploys 2-3 scout agents in parallel, each with a specific area of responsibility
- Each scout uses semantic-first hybrid search (meaning-based + keyword-based)
- Scouts search across specified domains (codebase, ProjectWiki, SvnLog, documentation)
- Each scout performs iterative refinement (up to 2-3 rounds) to fill knowledge gaps
- Scouts save individual reports with metadata, code sections, findings, and relationships

### 3. Read Results

Access the results:
- **Individual Scout Reports**: `.kilocode/sub-memory-bank/scout/yy-mm-dd-[scout-topic].md`
  - Detailed findings from each scout's investigation
  - Includes metadata, code sections, relations, and attention items
- **Consolidated Report**: `.kilocode/sub-memory-bank/report/yy-mm-dd-[topic].md`
  - Comprehensive summary integrating all scout findings
  - Cross-area connections and actionable recommendations
  - Appendix with deployment history and evidence trail

## Best Practices

- **Task Decomposition**: Let the system identify task type (Bug/Feature/Refactor) to optimize search strategy
- **Leverage Knowledge**: Check Memory Bank, ProjectWiki, and SvnLog before starting new investigations
- **Parallel Efficiency**: System deploys 2-3 scouts in parallel for optimal performance
- **Domain Selection**: Choose appropriate domains based on task type:
  - Bug/Debug → Codebase + SvnLog (recent changes)
  - Feature → Codebase + ProjectWiki (design docs)
  - Refactoring → All three (code + history + intent)
- **Iterative Approach**: Allow scouts to iterate 2-3 rounds to progressively fill knowledge gaps
- **Report Review**: Check individual scout reports for details, consolidated report for overall picture

> 💡 **Tip**: Use `/withScout` before any major design, debug, or refactor to quickly gain a structured, evidence-based understanding of your system.