# OpenAI Codex CLI Cheatsheet
---

## Installation

### Install Options
```bash
# NPM (recommended)
npm i -g @openai/codex

# Homebrew
brew install codex

# Verify installation
codex --version
```

### System Requirements
- Node.js (latest recommended)
- macOS (Apple Silicon and x86_64)
- Linux (x86_64 and arm64)

---

## Authentication

### Authentication Methods
```bash
# ChatGPT account (recommended)
codex --login

# API Key method
export OPENAI_API_KEY=your_api_key_here
codex

# CLI Help
codex --help
```

---

## Basic Commands

### Core Usage
```bash
# Start interactive session
codex

# Direct query
codex "explain this function"

# Quiet mode (output only)
codex -q "fix this bug"

# Continue previous session
codex --restore
```

### Command Options
```bash
# Specify model
codex -m "gpt-4o" "complex task"

# Include images
codex -i ./screenshot.png "analyze this UI"

# Set provider
codex -p openai "generate component"

# View history
codex --history

# Free credits
codex --free
```

---

## Approval Modes

### Suggest Mode (Default)
```bash
# Prompts for all actions
codex "refactor this component"
# Will ask: "Apply these changes? [y/N]"

# Explicit suggest mode
codex -a suggest "make changes"
```

### Auto-Edit Mode
```bash
# Auto-approves file edits, prompts for commands
codex --auto-edit "update all components"

# Or using approval-mode flag
codex -a auto-edit "refactor codebase"
```

### Full-Auto Mode
```bash
# Auto-approves everything in sandbox
codex --full-auto "complete implementation"

# With writable root
codex --full-auto -w /safe/directory "build feature"

# Using approval-mode flag
codex -a full-auto "automated workflow"
```

### Dangerous Mode
```bash
# Skip ALL confirmations (use with extreme caution)
codex --dangerously-auto-approve-everything "emergency fix"
```

---

## Configuration

### Config Management
```bash
# Open config file
codex -c

# Config file location
~/.codex/config.toml
```

### Configuration Options
```toml
# ~/.codex/config.toml
[general]
model = "gpt-4o"
provider = "openai"
approval_mode = "suggest"

[sandbox]
writable_roots = ["/home/user/projects"]
enable_notifications = true

[project]
include_project_doc = true
project_doc_path = "AGENTS.md"
```

### Environment Variables
```bash
# Authentication
export OPENAI_API_KEY=your_key

# Default model
export CODEX_MODEL=gpt-4o

# Approval mode
export CODEX_APPROVAL_MODE=auto-edit

# Debug mode
export CODEX_DEBUG=true
```

---

## Advanced Features

### Project Documentation
```bash
# Include AGENTS.md automatically
codex "implement user auth"
# Reads AGENTS.md context

# Skip project docs
codex --no-project-doc "quick fix"

# Custom project doc
codex --project-doc ./custom-doc.md "complex feature"
```

### Sandbox Mode
```bash
# Set writable directories
codex -w /path/to/safe/dir --full-auto "experimental changes"

# Multiple writable roots
codex -w /dir1 -w /dir2 "cross-directory changes"
```

### Model Context Protocol (MCP)
- Configure MCP in config file
- Enables extended tool capabilities
- Integrates with external services

### Image Analysis
```bash
# Single image
codex -i ./mockup.png "implement this design"

# Multiple images
codex -i ./before.png -i ./after.png "show differences"

# Image with context
codex -i ./error.png "debug this issue"
```

### Rollout Management

#### Session History
```bash
# Browse previous sessions
codex --history

# View specific rollout
codex -v rollout_id_123

# Inspect saved rollout
codex -v "previous debugging session"
```

---

## Shell Completion Setup

### Completions
```bash
# Bash
codex completion bash > ~/.bash_completion.d/codex

# Zsh
codex completion zsh > ~/.zsh/completions/_codex

# Fish
codex completion fish > ~/.config/fish/completions/codex.fish
```

---

## Best Practices

### Safe Development Workflow
```bash
# Start with suggest mode
codex -a suggest "analyze this codebase"

# Use auto-edit for trusted changes
codex --auto-edit "update dependencies"

# Reserve full-auto for sandboxed environments
codex --full-auto -w /tmp/sandbox "experimental features"
```

### Effective Prompting
```bash
# Be specific about scope
codex "add error handling to the authentication module"

# Include context
codex "using our established patterns, create a new API endpoint"

# Specify desired outcome
codex "refactor for performance while maintaining the current API"
```

---

## Security Considerations
```bash
# Review before applying
codex -q "generate code" | review-tool
```

- Use appropriate approval modes:
  - suggest: Production environments
  - auto-edit: Trusted file changes
  - full-auto: Sandboxed only
- Regular config review
```bash
codex -c
```
- Review settings periodically

---

## Workflow Integration
```bash
# Git integration
codex "create feature branch and implement login system"

# Testing workflows
codex "add comprehensive tests for this module"

# Documentation generation
codex "update README with new API endpoints"

# CI/CD preparation
codex "create deployment configuration for this service"
```

---

## Performance Optimization
```bash
# Use appropriate models
codex -m "gpt-4o-mini" "simple questions"
codex -m "gpt-4o" "complex architecture"
```

- Leverage project documentation
- Maintain good AGENTS.md files
- Use context-aware prompts
- Batch similar operations
```bash
codex "update all components to use new design system"
```

---

## Troubleshooting
```bash
# Enable verbose logging
codex --full-stdout "detailed task"

# Check authentication
codex --login

# Clear history
rm -rf ~/.codex/history/

# Reset configuration
rm ~/.codex/config.toml
codex -c
```

---
**OpenAI Codex CLI Cheatsheet • Updated: 2025-09-01**  
