# Scouts Claude Code Plugin

This Claude Code plugin provides intelligent code investigation capabilities through semantic-first parallel exploration.

## 📦 Plugin Structure

```
.claude-plugin/
├── plugin.json           # Plugin metadata and configuration
├── marketplace.json      # Marketplace listing information
├── README.md            # This file
├── commands/            # Custom commands (../commands/)
│   └── withScout.md    # Main investigation command
└── agents/              # Sub-agents (../agents/)
    └── scout.md        # Scout investigation agent
```

## 🎯 Available Commands

### `/withScout`

Main command for code investigation. Coordinates multiple scout agents to explore codebase in parallel.

**Usage:**
```
/withScout [investigation goal]
```

**Example:**
```
/withScout Investigate the authentication flow and identify where to add JWT refresh functionality
```

## 🤖 Available Agents

### `scout`

Specialized investigation agent that performs semantic-first hybrid search across codebase, documentation, and version history.

**Capabilities:**
- Semantic code search (meaning-based retrieval)
- On-demand knowledge loading (index-guided)
- Iterative refinement (2-3 rounds)
- Structured report generation

## 📊 Output

All investigation results are saved to:
- **Scout Reports**: `.kilocode/sub-memory-bank/scout/yy-mm-dd-[topic].md`
- **Consolidated Reports**: `.kilocode/sub-memory-bank/report/yy-mm-dd-[topic].md`

## 🔧 Configuration

The plugin automatically detects and uses project knowledge ecosystem:
- `/.kilocode/rules/memory-bank/index.md` - Knowledge index
- `/.kilocode/ProjectWiki/` - Architecture documentation
- `/.kilocode/SvnLog/` - Version history

## 📚 Documentation

For detailed documentation, see:
- [README.md](../README.md) - System overview
- [commands/withScout.md](../commands/withScout.md) - Complete workflow
- [agents/scout.md](../agents/scout.md) - Scout behavior specification
- [scouts-system-design.md](../scouts-system-design.md) - Architecture design

## 🚀 Quick Start

1. Ensure your project has the `.kilocode/` structure
2. Run `/withScout [your investigation goal]`
3. Review generated reports in `.kilocode/sub-memory-bank/`

## 📄 License

MIT

