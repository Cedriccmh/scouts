# Scouts System

<div align="center">

**TokenRoll Claude Code Plugin: Best Practices for CC Coding**

[![GitHub](https://img.shields.io/badge/GitHub-TokenRollAI%2Fcc--plugin-blue?logo=github)](https://github.com/TokenRollAI/cc-plugin)

[English](README.md) | [简体中文](README.zh-CN.md)

</div>

---

## Installation

### Step 1: Install Plugin

```
# Add TokenRoll plugin marketplace
/plugin marketplace add https://github.com/TokenRollAI/cc-plugin

# Install tr plugin
/plugin install tr@cc-plugin
```

### Step 2: Use the Plugin

1. Add to your user-level CLAUDE.md
   ```
   - Always use scout agent to get knowledge and information for codebases, web, documentation
   - Always try use bg-worker and scout agent to help you finish work
   ```
   Done! Now you can use it normally.
2. Force using Scout Agent to enhance context efficiency
   ```
   /withScout xxx(your task)
   ```

### (Recommend!) Install CCR: Power SubAgent with GLM4.6

[Reference](https://github.com/musistudio/claude-code-router)

```
npm install -g @musistudio/claude-code-router
```

Fill in the configuration in `~/.claude-code-router/config.json`, reference as follows:

```
{
    "LOG": true,
    "LOG_LEVEL": "debug",
    "CLAUDE_PATH": "",
    "HOST": "127.0.0.1",
    "PORT": 3456,
    "APIKEY": "sk-apikey",
    "API_TIMEOUT_MS": "600000",
    "PROXY_URL": "http://127.0.0.1:7890",
    "transformers": [
        "Anthropic"
    ],
    "Providers": [
        {
            "name": "claude",
            "api_base_url": "https://<BASE>/v1/messages",
            "api_key": "XXX",
            "models": [
                "claude-sonnet-4-5-20250929"
            ],
            "transformer": {
                "use": [
                    "Anthropic"
                ]
            }
        },
        {
            "name": "glm",
            "api_base_url": "https://open.bigmodel.cn/api/anthropic/v1/messages",
            "api_key": "XXX",
            "models": [
                "glm-4.6"
            ],
            "transformer": {
                "use": [
                    "Anthropic"
                ]
            }
        }
    ],
    "Router": {
        "default": "claude,claude-sonnet-4-5-20250929",
        "background": "claude,claude-sonnet-4-5-20250929",
        "think": "claude,claude-sonnet-4-5-20250929",
        "longContext": "claude,claude-sonnet-4-5-20250929",
        "webSearch": "claude,claude-sonnet-4-5-20250929"
    }
}
```

## About

A powerful Claude Code plugin developed by **DJJ** and **Danniel** for the TokenRoll team. This plugin transforms your development workflow with intelligent Git automation, research-first development patterns, and creative ideation tools.

## Core Features

- **`/tr:commit`** - Intelligent commit message generator that learns from your Git history

- **`/tr:withScout`** - **Save significant main agent context through sub-agent architecture** (ideal for refactoring, bug fixing, feature planning, and documentation in medium to large projects)

- **Super-Idea Agent** - Transform a simple idea into a viral product concept

<div align="center">

Made with ❤️ by DJJ & Danniel

</div>
