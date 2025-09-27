# Claude Code CLI Cheatsheet
---

## Installation

### Install Options
```bash
# NPM (recommended)
npm install -g @anthropic-ai/claude-code

# Native Install (Beta) - macOS/Linux/WSL
curl -sL https://install.anthropic.com | sh

# Native Install (Beta) - Windows PowerShell
irm https://claude.ai/install.ps1 | iex

# Verify installation
claude --version

# Update to latest version
claude update
```

### System Requirements
- Node.js 18+ (latest LTS recommended)
- Windows, macOS (Apple Silicon and Intel), Linux (x86_64 and arm64)
- 4GB RAM minimum

---

## Authentication

### Authentication Methods
```bash
# Claude account login (recommended)
claude  # Then use /login in the session

# API Key method
export ANTHROPIC_API_KEY=your_api_key_here
claude

# CLI Help
claude --help
```

---

## Basic Commands

### Core Usage
```bash
# Start interactive session
claude

# Direct prompt execution
claude "explain this codebase"

# Continue last session
claude -c

# Resume specific session
claude -r session-id-here

# New session
claude --new

# Start with initial prompt
claude "summarize this project"
```

### Command Options
```bash
# Specify model
claude --model claude-sonnet-4-20250514 "complex refactor"

# Include additional directories
claude --add-dir /path/to/extra "update all components"

# View session history (interactive list)
claude --resume

# Set working directory
claude --dir /path/to/project
```

---

## Slash Commands

### Session Management
```
/new                 # Start fresh conversation
/clear              # Clear current context
/history            # Show command history
/save [name]        # Save current session
/load [name]        # Load saved session
/compact [instructions]   # Summarize conversation with optional instructions
/exit                     # Exit the REPL
/help                     # Show available commands
/config                   # Open configuration panel
/doctor                   # Check Claude Code installation health
/cos                      # Show cost and duration of current session
```

### File Operations
```
/read [file]        # Read and add file to context
/edit [file]        # Edit file with AI assistance
/create [file]      # Create new file
/search [pattern]   # Search files in project
/grep [term]        # Search content in files
/init               # Generate CLAUDE.md project guide
/memory             # Edit project memory files
```

### Git Integration
```
/git status         # Show git status
/git diff           # Show uncommitted changes
/git commit         # Create commit with AI message
/git branch         # Manage branches
/review             # Review staged changes
/git add -p         # Interactive staging
/git reset --soft   # Undo last commit
/git stash          # Save work temporarily
/git log --oneline  # View commit history
```

### Project Management
```
/todo               # Manage task list
/test               # Run tests
/build              # Run build command
/lint               # Run linter
/ide                # Manage IDE integrations
/terminal-setup     # Install Shift+Enter binding for multi-line input (iTerm2/VS Code)
```

### Model & Settings
```
/model [name]       # Switch model
/temperature [0-1]  # Set creativity level
/context            # Show current context size
/settings           # View/edit settings
/vim                # Enable vim-style editing mode
```

---

## Configuration

### Config Management
```bash
# Open config file
claude /config

# Config file locations
~/.claude/settings.json  # User-wide
.claude/settings.json    # Project-wide
.claude/settings.local.json  # Local overrides
```

### Configuration Options
```json
{
  "model": "claude-sonnet-4-20250514",
  "temperature": 0.7,
  "maxTokens": 4096,
  "autoSave": true,
  "gitIntegration": true,
  "lintOnSave": true,
  "testOnCommit": false,
  "projectFiles": ["AGENTS.md", "README.md"],
  "excludePatterns": ["node_modules", ".git", "dist"],
  "permissions": {
    "allowedTools": ["Read", "Write", "Bash(git *)"],
    "deny": ["Read(./.env)"]
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write(*.py)",
        "hooks": [{"type": "command", "command": "python -m black $file"}]
      }
    ]
  }
}
```

### Environment Variables
```bash
# Authentication
export ANTHROPIC_API_KEY=your_key

# Default model
export CLAUDE_MODEL=claude-sonnet-4-20250514

# Project root
export CLAUDE_PROJECT_ROOT=/path/to/project

# Debug mode
export CLAUDE_DEBUG=true
```

---

## Advanced Features

### Project Context
```bash
# Include AGENTS.md automatically
claude "implement auth system"

# Custom context file
claude --context ./project-context.md "build feature"

# Multiple context files
claude --context file1.md --context file2.md

# Initialize project guide
claude /init

# Edit memory
claude /memory
```

### Planning Mode
```bash
# Enter planning mode
claude --plan "e-commerce checkout flow"

# Review and approve plan
claude --execute-plan ./plan.md
```

### Test-Driven Development
```bash
# Generate tests first
claude --tdd "user authentication module"

# Run tests after changes
claude --auto-test "refactor database layer"

# Write tests before implementation
claude --test-first "payment processing"

# Coverage analysis
claude --coverage "identify untested code"
```

### Multi-file Operations
```bash
# Edit multiple files
claude --multi-edit "update all API endpoints"

# Batch refactoring
claude --refactor "extract common logic"

# Process multiple files
find . -name "*.js" -exec claude -p "analyze this file for bugs: {}" \; > bug_report.txt
```

### Tool Management
```bash
# Allow specific tools without prompting
claude --allowedTools "Bash(git log:*)" "Bash(git diff:*)" "Write"

# Disallow specific tools
claude --disallowedTools "Bash(rm:*)" "Bash(sudo:*)"

# Skip all permission prompts (dangerous)
claude --dangerously-skip-permissions
```

### Advanced Piping
```bash
# Complex piping operations
git log --oneline | claude -p "summarize these commits"
cat error.log | claude -p "find the root cause"
ls -la | claude -p "explain this directory structure"
```

---

## Working Modes

### Interactive Mode (Default)
```bash
# Full interactive experience
claude
# - File navigation
# - Real-time editing
# - Command execution
```

### Headless Mode
```bash
# No UI, direct execution
claude --headless "fix all linting errors"

# Output only mode
claude --quiet "generate documentation"

# Print mode (SDK) - execute and exit
claude -p "explain this function"
```

### Watch Mode
```bash
# Monitor file changes
claude --watch "maintain code quality"

# Auto-fix on save
claude --watch --auto-fix
```

---

## Model Context Protocol (MCP)

### MCP Servers
```bash
# List available MCP servers
claude mcp list

# Connect to MCP server
claude mcp connect github

# Configure MCP
claude mcp config

# MCP server management (via slash commands)
/mcp                      # Access MCP functionality
```

### Available MCP Integrations
- GitHub integration
- Browser automation (Chrome, Puppeteer)
- Database connections
- Cloud services (AWS, GCP, Azure)
- External APIs
- Google Drive, Figma, Slack

---

## Git Workflow Integration

### Safe Git Practices
```bash
# Create feature branch
claude "create branch for user dashboard"

# Stage changes interactively
claude "stage relevant changes only"

# Generate commit message
claude "commit with descriptive message"

# Create pull request
claude "create PR with summary"

# Git hooks integration
claude -p "create pre-commit hook for code quality" > .git/hooks/pre-commit

# Advanced Git operations
git log --oneline -10 | claude -p "create changelog from these commits"
git diff --name-only | claude -p "explain what changed in this commit"
```

### Git Commands via Claude
```
/git add -p         # Interactive staging
/git reset --soft   # Undo last commit
/git stash          # Save work temporarily
/git log --oneline  # View commit history
```

---

## Testing Integration

### Test Commands
```bash
# Run all tests
claude test

# Run specific test file
claude test ./src/auth.test.js

# Generate new tests
claude "add tests for edge cases"

# Fix failing tests
claude "fix test failures"
```

### Test-First Development
```bash
# Write tests before implementation
claude "write unit tests for payment processing"

# Coverage analysis
claude --coverage "identify untested code"
```

---

## Best Practices

### Effective Prompting
```bash
# Be specific about requirements
claude "add error handling with retry logic to API calls"

# Include constraints
claude "optimize performance without breaking changes"

# Reference patterns
claude "follow existing auth pattern for new endpoint"
```

### Context Management
```bash
# Start with minimal context
claude --minimal "quick fix"

# Add context as needed
/read ./src/config.js
/read ./src/database.js

# Clear unnecessary context
/clear
```

### Safety Practices
```bash
# Review mode for critical changes
claude --review-mode "update authentication"

# Dry run without applying changes
claude --dry-run "refactor database layer"

# Backup before major changes
claude --backup "major refactoring"

# Use `--disallowedTools` for dangerous commands
claude --disallowedTools "Bash(rm:*)" "Bash(sudo:*)"

# Avoid `--dangerously-skip-permissions`
```

### Performance Tips
- Keep context under 100k tokens
- Remove unnecessary files from context
- Use specific file patterns
- Use `/clear` frequently between tasks
- Limit context with `--max-turns`
- Use `/compact` for long conversations

### Workflow Tips
- Create custom slash commands in `.claude/commands/`
- Use `--output-format json` for automation
- Pipe commands for complex workflows
- Use session IDs for long-running tasks

---

## Troubleshooting

### Debug Commands
```bash
# Enable debug logging
claude --debug

# Verbose output
claude --verbose "complex task"

# Check API status
claude status

# Clear cache
claude cache clear

# Reset configuration
claude reset

# Performance diagnostics
/doctor --performance
```

### Common Issues
```bash
# Fix permission issues
sudo chown -R $(whoami) ~/.claude-code

# Update to latest version
npm update -g @anthropic-ai/claude-code

# Reinstall
npm uninstall -g @anthropic-ai/claude-code
npm install -g @anthropic-ai/claude-code
```

---

## Keyboard Shortcuts

### Navigation
```
Ctrl+P          # File picker
Ctrl+Shift+F    # Search in files
Ctrl+G          # Go to line
Ctrl+Tab        # Switch files
Up/Down         # Navigate command history
```

### Editing
```
Ctrl+/          # Toggle comment
Ctrl+D          # Multi-cursor
Ctrl+Shift+L    # Select all occurrences
Alt+Up/Down     # Move line
```

### Claude-specific
```
Ctrl+Enter      # Submit prompt
Ctrl+K          # Clear prompt
Ctrl+R          # Retry last command
Ctrl+Z          # Undo AI changes
Escape          # Cancel operation
Ctrl+C          # Cancel current operation
Ctrl+D          # Exit Claude Code
Tab             # Auto-complete
Up/Down         # Navigate command history
Esc Esc         # Edit previous message (double escape)
Shift+Tab       # Toggle permission modes (Auto-Accept, Plan Mode, normal)
Ctrl+L          # Clear terminal screen
Shift+Enter     # Insert new line (after /terminal-setup)
\ + Enter       # Quick multi-line escape (all terminals)
Option+Enter    # Insert new line (macOS default)
Ctrl+J          # Insert line feed for multi-line
```

---

## Performance Tips

### Optimize Context
- Keep context under max tokens via clear
- Use specific directories

### Model Selection
```bash
# Fast responses for simple tasks
claude --model claude-3-haiku "format code"

# Complex reasoning
claude --model claude-3-opus "architect system"

# Balanced performance
claude --model claude-3-sonnet "implement feature"
```

### Batch Operations
```bash
# Group similar tasks
claude "update all test files to use new assertions"

# Process multiple files efficiently
claude --batch "add TypeScript types"
```

---

## Integration Examples

### VS Code Integration
```bash
# Open in VS Code after changes
claude --open-in vscode "implement feature"

# Sync with VS Code settings
claude --sync-vscode

# Configure VS Code integration
/ide vscode
```

### CI/CD Integration
```bash
# Pre-commit hooks
claude --pre-commit "ensure code quality"

# GitHub Actions
claude --github-action "create deployment workflow"

# CI/CD pipeline integration
claude -p "analyze test coverage" --output-format json | jq '.coverage_percentage'
claude -p "generate release notes from commits" --max-turns 2 > RELEASE_NOTES.md
```

### Documentation
```bash
# Generate documentation
claude docs generate

# Update existing docs
claude docs update

# Create API documentation
claude docs api
```

### Third-Party Tool Connections
```bash
# Database integration
mysql -e "SHOW TABLES" | claude -p "analyze database structure"

# Docker integration
docker ps | claude -p "analyze running containers"
docker logs container_name | claude -p "find errors in logs"
```

---

## Security & Privacy

### Data Protection
```bash
# Local-only mode (no cloud)
claude --local-only

# Exclude sensitive files
claude --exclude "*.env,*.key"

# Redact secrets
claude --redact-secrets

# Use deny in permissions
```

### Audit & Compliance
```bash
# Log all changes
claude --audit-log

# Review mode for production
claude --production-safe

# Compliance check
claude --compliance-check

# Security-focused operations
claude --disallowedTools "Bash(rm:*)" "Bash(sudo:*)" "Bash(chmod:*)" \
       --audit-mode \
       --no-external-calls \
       "secure code review"
```

---

**Claude Code CLI Cheatsheet • Updated: 2025-09-26**
**Documentation**: [docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code)
**GitHub**: [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)