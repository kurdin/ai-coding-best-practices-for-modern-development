# Code with AI: AI Coding Best Practices for Modern Development

## About This Presentation

This is an interactive HTML presentation on AI coding best practices and patterns for modern development. The presentation covers essential topics for developers looking to integrate AI tools effectively into their workflow.

## Presenter

**Sergey Kurdin**
- Senior Developer at Charles River Labs (Apollo SA project)
- 30+ years building software
- Built and shipped products at Marriott.com, Ski.com, It.com, Amazon, NIH, and multiple startups
- PasteBar App Maintainer - Free, Open Source Clipboard Manager for Mac & Windows (1.7k★ on GitHub)

## Topics Covered

### 1. Foundation
- Why AI coding now & mindset shift
- Evolution of AI-assisted coding
- Current tooling landscape

### 2. Understanding AI
- How LLMs work & context windows
- Model differences and specialization
- The confidence calibration problem

### 3. Best Practices
- Prompting patterns & planning-first approach
- Mental model for architecting with AI
- General workflow: Plan → Implement → Test → Review

### 4. Git Workflow
- Safe version control & incremental commits
- The incremental staging pattern
- Essential Git commands for AI work

### 5. CLI-first Agents
- Codex CLI essential commands & workflow
- Why CLI-first approach matters
- Practical workflow examples

### 6. Quality Control
- Testing AI-generated code
- Property-based and mutation testing
- Performance awareness & AI-assisted reviews

### 7. Limits & Safety
- Data & safety guardrails
- When NOT to use AI
- Security considerations

### 8. Human Skills
- What matters MORE with AI
- System design and code review importance
- Domain expertise as differentiator

## Key Takeaways

- AI is a **tool, not a replacement** for developers
- Small, verifiable changes win
- Context is everything, use it wisely
- Don't trust—verify
- Your skills become **MORE valuable**, focus on patterns
- Plan, guide, review, and accept—you stay in control
- Start small. Ship safely. Measure impact.

## Core Principles

### The Mindset Shift
- Build **systems that solve problems**
- Shift from **coder → architect**
- AI learns from your repo and suggests solutions; you guide and control

### Workflow Pattern
1. **Before Code**: Clarify intent, define constraints, provide relevant context
2. **During Code**: Ask for plans first, request smaller changes, review and iterate
3. **After Code**: Review all changes, lint/typecheck/build/test, security review

### Git Safety Flow
1. Start with clean directory
2. Have AI make one small change
3. `git add -p` → review hunks
4. Test locally first
5. Pass? → commit with `[AI]` prefix
6. Fail? → `git restore --staged` and retry

## Practical Tips

### Effective Prompting Structure
**Role • Context • Task • Constraints • Verification**

Example:
```
Role: Senior TypeScript engineer.
Context: Node 20, Jest; repo uses src/ and test/.
Target: src/auth/token.ts#getUserToken duplicates retry/backoff logic.
Task: Extract retry/backoff into src/utils/retry.ts
Constraints:
• Keep public signatures stable
• Do not change unrelated modules
• Update tests to cover edge cases
Verification:
• npm run typecheck
• npm test
```

### Common AI Code Smells to Watch For
- Generic variable names (`data`, `item`, `result`)
- Deeply nested ifs or loops
- Missing error boundaries
- Hardcoded values
- Too many console.logs
- Unused imports

### Security Best Practices
- Never paste secrets or tokens
- Use placeholders like `[API_KEY]`
- Mask customer data
- Tag AI commits with `[AI]` prefix
- Use enterprise models for private code

## Tools Mentioned

### Autocomplete Copilots
- GitHub Copilot, Codeium, TabNine

### Chat Assistants
- ChatGPT, Claude, Gemini

### CLI-first Coding Agents
- Codex CLI, Claude Code, Cursor, Windsurf

## Pro Tips

- Generate and reuse AGENTS.md file with repo-specific instructions
- Use Full Access mode in Codex so it can read files and make edits without approval
- Use git to control flow/changes
- Provide minimal snippet instead of entire file when requesting specific changes
- If session gets long/noisy, summarize or start fresh
- 15-minute rule: If stuck → change approach or start over

## How to Use This Presentation

1. Open `ai-coding-best-practices.html` in a web browser
2. Navigate using:
   - Arrow keys (← →) or Space bar
   - Home/End keys to jump to first/last slide
   - Mouse/touch swipe on mobile devices
3. Controls appear when hovering near bottom of screen
4. Direct link to specific slides using URL hash: `#slide-N`

## Contact

- **Email**: sergey.kurdin@crl.com
- **LinkedIn**: [linkedin.com/in/kurdin](https://www.linkedin.com/in/kurdin/)
- **GitHub**: @sergeykurdin
- **Project**: PasteBar - Free Clipboard Manager for Mac & Windows

## License

This presentation material is for educational purposes. Please contact the author for usage rights.