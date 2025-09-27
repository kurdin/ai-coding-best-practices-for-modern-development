# Code with AI
## AI Coding Best Practices for Modern Development

**Presenter:** Sergey Kurdin  
Senior Developer at Charles River Labs (Apollo SA project)  
30+ years building software  
Built and shipped products at Marriott.com, Ski.com, It.com, Amazon, NIH, and multiple startups  
[PasteBar App](https://github.com/PasteBar/PasteBarApp) Maintainer - Free, Open Source Clipboard Manager for Mac & Windows (1.7k★ on GitHub)

---

## Agenda

- **Foundation:** Why AI coding now & mindset shift
- **Understanding AI:** How LLMs work & context windows
- **Best Practices:** Prompting patterns & planning-first approach
- **Git Workflow:** Safe version control & incremental commits
- **CLI-first Agents:** Common commands & workflow (tool-agnostic)
- **Quality Control:** Testing, reviews & catching bad patterns
- **Limits & Safety:** AI security guardrails
- **Human Skills:** What matters MORE with AI
- **Key Takeaways:** Start small, verify everything

---

## Evolution of AI-Assisted Coding

### Early Tools
- Syntax highlighting → Better readability
- Linting & type checking → Fewer mistakes

### AI Breakthrough
- ChatGPT 3.5 → Natural language Q&A
- GitHub Copilot → Inline autocomplete

### Modern Coding Agents
- Claude Code, Codex CLI, Cursor, Windsurf, Gemini Code Assist
- Understand repo structure & context
- Planning first, then implementation
- Plan → apply small step → test → iterate (repo-aware, reviewable edits)

---

## Why AI for Developers — Now

- **Less typing, more steering**
- Fast refactors and unit tests in minutes; iterate on implementation variants
- Faster documentation and code reviews
- Learns and follows your repo's patterns
- Produces code aligned with project style

✓ You guide, review, and accept  
✓ AI accelerates mechanics  
✓ You own design and code quality

💡 **Pro Tip:** Generate and reuse AGENTS.md file with repo-specific instructions

---

## Current Tooling Landscape

### Autocomplete Copilots
- GitHub Copilot, Codeium, TabNine
- Inline suggestions while typing

### Chat Assistants
- ChatGPT, Claude, Gemini
- Architecture and design decisions
- Q&A and code generation via chat

### CLI-first Coding Agents **Most Powerful**
- Claude Code, Codex CLI, Cursor, Windsurf, Gemini Code Assist
- Understand entire repository structure
- Plan → Review → Implement workflow
- Direct file editing with reviewable changes

✓ Focus on patterns, not brands — most agents support similar flows

---

## The Mindset Shift

- Build **systems that solve problems**
- Shift from **coder → architect**
- AI learns from your repo and suggests solutions; you guide and control
- **Your new responsibilities:**
  - Define the problem clearly
  - Curate context carefully
  - Review changes thoroughly
  - Enforce quality gates
- Result: **Fewer keystrokes, more impact** and **fewer typing mistakes**

---

## What is AI? (LLMs in 2 Minutes)

- **AI = Large Language Models** trained on text/code patterns
- They're **NOT databases** or compilers
- They **predict the next token** given prior tokens

### Strengths:
- Pattern recall & style mimicry
- Fast scaffolding
- Broad knowledge base

### Weaknesses:
- Hallucinations (confident but wrong)
- No true runtime awareness

⚠️ "Autocomplete on steroids" - not a truth engine

---

## How LLMs Generate Code

- **Tokenization → Probabilities → Decoding**
- Output quality depends on:
  - Prompt clarity
  - Curated context
  - Explicit constraints
- **Temperature** controls creativity vs safety
- Outputs can vary—build, run, and test to validate

✓ Best Practice: Ask for plans first, then for implementation  
✓ Keep changes smaller and under control  
✓ Compile, run, manual test, unit tests

---

## Understanding Models and Context Windows

### Model Context Limits:
- Model context windows vary by provider (hundreds of thousands of tokens)
- Effective usable window is always smaller than advertised

### What Makes Models Different:
- Training data: General text vs code repositories
- Architecture: Base vs instruction-tuned vs code-specialized, fine tuning
- Optimization: Next-token prediction; instruction-tuning and tool use enable task completion

### Why Specialization Matters:
- General models: Great explanations, weaker syntax
- Code models: Strong patterns, weaker natural language

✓ Code models trained on millions of patterns  
✓ Choose model based on task: coding vs explaining

---

## Why Context Matters

- Models only see a **limited window**
- Too much context → **truncation** of critical code
- Provide only minimal relevant files plus explicit acceptance criteria and constraints

### Context priority order (what to include):
1. Current error messages & stack traces
2. Files you're editing & their imports
3. Related type definitions & interfaces
4. Relevant test files
5. Project config (package.json, tsconfig)

✓ Mantra: Curate → Confirm → Constrain → Verify

---

## The Confidence Calibration Problem

- LLMs are **always confident**, even when wrong
- No built-in "I don't know" mechanism

### Red flags to watch:
- Inventing APIs that don't exist
- Using deprecated methods confidently
- Creating strange-sounding features

### Mitigation strategies:
- Cross-check with your knowledge and official docs; assume unfamiliar APIs are suspect
- Extra caution with new libraries, new APIs
- Track hallucination patterns and ask for clarification or start over

⚠️ Example: useState2(), Array.prototype.contains() (non-existent)

---

## Mental Model: Architecting with AI

- Decompose tasks → Write acceptance criteria
- Constrain scope → Request **small changes**
- Iterate quickly → Run, test, review each step
- Treat AI like a **junior developer**
  - Ask to plan first
  - Ask why you need to change
  - Request alternatives
  - Trust, but verify: compile → run → test before commit

⚠️ Visually review all changes, not just trust end results

---

## General Best Practices

### Before Code
- Clarify your intent, better understand the problem
- Define constraints
- Provide relevant context only: files, imports, components, types, etc.

### During Code
- Ask for plans first, review then implement
- Request smaller changes
- Review small changes, revert early, and iterate

### After Code
- Review all changes, ask AI to explain
- Use lint, typecheck, build and test
- Manual test, unit tests
- Security review
- Performance check

✓ Workflow: Plan → Implement → Test → Review

---

## Prompt Patterns That Work (for CLI agents)

- **Structure:** Role • Context • Task • Constraints • Verification
- Be explicit about files/scope, runtime/versions, and safety expectations
- Prefer plan → apply for multi-step work; keep each step small and reviewable
- Keep outputs focused and actionable; prefer commands or concise status summaries

```
Example Prompt (Refactor, File Edits Applied):
Role: Senior TypeScript engineer.
Context: Node 20, Jest; repo uses src/ and test/.
Target: src/auth/token.ts#getUserToken duplicates retry/backoff logic.
Task: Extract retry/backoff into src/utils/retry.ts and reuse it in getUserToken
without changing external behavior.
Constraints:
• Keep public signatures stable
• Do not change unrelated modules
• Update test/auth/token.spec.ts to cover 429/503 with exponential backoff (max 3 attempts)
Verification:
• build passes (Node 20)
• npm run typecheck
• npm test -- test/auth/token.spec.ts
Out of scope:
• Do not modify unrelated modules or configuration files
```

---

## Version Control & AI Patterns

### The Incremental Staging Pattern

1. Start new branch: `git checkout -b feature/ai-refactor`
2. Ensure clean directory: `git status` shows no changes
3. Request AI to create a plan, review it, approve or request improvements, do small, focused, reviewable changes
4. Stage incrementally: `git add -p` (review each hunk)
5. Test locally: manual test, lint, type check, compile, unit tests
6. Good → commit: `git commit -m "[AI]: Extract retry logic"`
7. Bad → revert: `git restore` or `git revert` and retry prompt
8. Move to next task; repeat for multi-step work

```bash
git checkout -b feature/ai-refactor
git add -p  # Review hunks interactively
git commit -m "[AI]: Extract retry logic"
git restore --staged .  # Unstage if needed (avoid reset --hard)
```

---

## Planning-First for Big Features

**Use AI to plan large features upfront → Break into manageable subtasks → Reduce risk**

### Step 1: Describe the Feature
- Current state, requirements, constraints. Include UI screenshots, wireframes, diagrams, etc.
- `"As a product architect, summarize this feature spec: [details]"`

### Step 2: Request Implementation Plan
- Break into smaller subtasks
- `"Create plan for [feature]: subtasks, dependencies, save as Markdown [feature-name]-plan.md"`

### Step 3: Review & Approve
- Get your approval before implementation or request changes
- `"Start implementation of subtask 1 from [feature-name]-plan.md"`

---

## Essential Git Commands for AI Work

- `git switch -c ai/<feature>` — Create dedicated AI branch
- `git add -p` — Stage specific hunks
- `git restore --staged .` — Unstage to retry
- `git diff --staged` — Verify changes
- `git commit -m "[AI] checkpoint: desc"`
- `git revert HEAD` — Safe undo
- `git log --grep="[AI]"` — Track AI commits
- `git rebase -i` — Clean before PR
- pre-commit hooks — Auto-lint/format before commit

⚠️ Avoid `reset --hard`

---

## Testing AI-Generated Code

**AI code needs extra testing — it makes creative mistakes**

### Property-Based Testing
- Define invariants, auto-generate diverse inputs
- AI often misses edge cases — good unit tests help to expose them

### Mutation Testing
- Verify test quality by introducing small bugs
- If tests don't catch the bugs, they need improvement
- Especially important for AI-generated code

### Weakness Detection
- Use AI against itself
- `"Find 3 ways to break this function, including edge cases"`
- AI suggests: huge inputs, duplicates, non-comparable types

### Browser Testing with MCP
- Model Context Protocol (MCP) enables AI to interact with Chrome
- AI can navigate, click, fill forms, verify UI behavior, check console logs and errors
- Example: `github.com/hangwin/mcp-chrome`

### Golden Rule
**AI code → Human tests | Human reviews → AI tests**
- Balance automation with human judgment in the middle to avoid false positives
- Always run existing tests before committing AI changes
- If AI wrote it, add at least one property-based test or mutation-killing assertion

---

## Performance Awareness & AI-Assisted Reviews

**AI code often needs optimization — combine performance checks with AI reviews**

### Performance Issues to Watch
- Inefficient database queries
- Too many nested loops
- Blocking I/O operations
- Memory leaks in handlers

### AI Double-Loop Reviews
- Ask for risk analysis and efficiency
- Request missing test cases
- Generate PR descriptions
- Review for security, performance, edge cases
- `"Find 3 issues with this code and suggest fixes"`

⚠️ Never skip human review—assume AI is wrong until tests and profiling say otherwise

✓ When creating a PR, ask: "Write a concise PR description from these changes: [summary]"

---

## Data & Safety Guardrails

**Protect customer data, secrets, and IP while integrating AI safely**

### Never Paste Secrets or Tokens
- Use placeholders like `[API_KEY]` and replace post-generation
- Configure AI tools to auto-redact sensitive patterns

### Mask Customer Data
- Use synthetic data: `user_1@example.com` instead of real emails

### Tag AI Commits
- Use `[AI]` prefix for transparency

### Use Secrets Managers
- Never paste tokens into prompts
- Use environment variables or secret management tools

### Review License Obligations
- Verify licenses for generated code and suggested dependencies
- Ensure compliance with your organization's policies

### Use Enterprise Models for Private Code
- Use only enterprise or on-prem models for private repos; avoid public AI services for proprietary code

---

## CLI-first AI Workflow (Tool-Agnostic)

**Automation, consistency, CI/CD-friendly**

### Why CLI?
- **Scriptable:** Wrap prompts in bash/python scripts
- **Portable:** Works in terminals, servers, remote
- **Standardize:** Share configs & aliases team-wide

### Common Agent Capabilities
- Plan / Review / Diff / Apply
- Mention files or folders
- Search or fuzzy-find files
- Resume sessions, compact/summarize

✓ Flow: Plan → Diff preview → Apply small step → Test → Commit

---

## Common CLI Agent Commands (Generic)

### Session & Config
- `/init` — Generate `AGENTS.md` / set context
- `/status` — Show settings
- `/model` — Pick model/effort level
- `/new` or `/resume` — Session control

### Workflow
- `/plan` — Propose steps
- `/diff` — Preview changes
- `/apply` — Apply edits
- `/review` — Critique changes
- `/mention` — Add files to context
- `@` — Fuzzy file search

### About AGENTS.md Files
- CLI agents automatically detect and use `AGENTS.md` files for context
- Use **multiple AGENTS.md files** for different repo areas:
  - `backend/AGENTS.md` — API-specific patterns & rules
  - `frontend/AGENTS.md` — UI conventions & components
  - `libs/AGENTS.md` — Component library guidelines
- Each file provides domain-specific context to guide AI behavior

📚 **CLI-Specific References:**
- [Claude Code CLI Cheatsheet](Claude%20Code%20CLI%20Cheatsheet.md)
- [OpenAI Codex CLI Cheatsheet](OpenAI%20Codex%20CLI%20Cheatsheet.md)

---

## CLI Agent Workflow Example (Generic)

### 1. Start & Create Plan
```
$ claude | codex
→ Plan retry logic with exponential backoff; save to retry-plan.md
```

### 2. Review Plan
```
$ cat retry-plan.md
```
← Approve before applying

### 3. Execute Approved Step
```
$ claude | codex
→ Implement step 1 from retry-plan.md; run tests after changes
```

### 4. Stage & Commit
```
$ git add -p
$ git commit -m "[AI]: Implement retry logic step 1"
```

### 5. Test & Push
```
$ npm test
$ git push -u origin ai/retry-logic
```
→ Open PR for review

---

## The Context Switching Cost

- **Batch similar tasks**
  - All tests, then all refactors
- **Save successful prompts in team knowledge base**
- **Build context once**, use many times
- **When AI gets stuck:** Clear context, simplify request, provide working example
- **15-minute rule:**
  - If stuck → change approach or better start over

💡 **Tip:** Provide a minimal snippet instead of the entire file when requesting a specific change

⚠️ If the session gets long/noisy, summarize or start a fresh session

---

## Bad Patterns in AI Code

### Generic variable names
- `data`, `item`, `result`

### Code structure issues
- Deeply nested ifs or loops
- Overly "clever" one-liners
- Unnecessary layers of indirection that obscure control flow

### Missing safeguards
- No error boundaries
- Hardcoded values
- Catching and swallowing errors without logging or remediation

### Debug artifacts
- Too many console.logs and comments
- Unnecessary type assertions
- Unused or redundant imports

⚠️ You should catch those issues and fix before creating PR

---

## Human Skills That Matter More

- **System design** (AI can't architect)
- **Code review** (3x more important)
- **Specification writing** = new programming
- **Domain expertise** = your differentiator
- **Debugging intuition**

💡 Strong fundamentals matter MORE, not less

⚠️ AI amplifies both good and bad practices

---

## Key Takeaways

- AI is a **tool, not a replacement** for developers
- Small, verifiable changes win
- Context is everything, use it wisely
- Don't trust—verify
- Your skills become **MORE valuable**, focus on patterns
- Plan, guide, review, and accept—you stay in control
- Start small. Ship safely. Measure impact.

---

## Practical AI Workflow

### Effective Prompts

**Planning:**
```
"Create plan for [feature]. Save to [feature].md for review"
```

**Bugfix:**
```
"Fix [bug] in [file]. Include test."
```

**Refactor:**
```
"Extract [logic] to [target dir]."
```

**Testing:**
```
"Add tests for [file] edge cases."
```

**Docs:**
```
"Document [API] with examples."
```

### Git Safety Flow

1. Start with **clean dir**
2. Have AI make **one small change**
3. `git add -p` → review
4. **Test locally** first
5. Pass? → **commit**
6. Fail? → `git restore --staged`
7. **Iterate** with better prompt

**Golden Rule:** Smaller changes = Easy rollbacks

---

## Thank You!

**AI Coding Best Practices & Patterns for Modern Development**

**Sergey Kurdin**  
CRL: sergey.kurdin@crl.com  

LinkedIn: [linkedin.com/in/kurdin](https://www.linkedin.com/in/kurdin/)  
GitHub: @sergeykurdin  
Project: [PasteBar](https://github.com/PasteBar/PasteBarApp) - Free Clipboard Manager for Mac & Windows

## Contact

- **Email**: sergey.kurdin@crl.com
- **LinkedIn**: [linkedin.com/in/kurdin](https://www.linkedin.com/in/kurdin/)
- **GitHub**: @sergeykurdin
- **Project**: PasteBar - Free Clipboard Manager for Mac & Windows

## License

This presentation material is for educational purposes. Please contact the author for usage rights.
