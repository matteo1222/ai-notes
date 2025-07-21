# Effective Agentic Coding Patterns: A Beginner's Guide

*A comprehensive guide to patterns and best practices for working effectively with AI coding assistants*

## Sources
- [Agentic Coding - Armin Ronacher](https://lucumr.pocoo.org/2025/6/12/agentic-coding/) **(Ronacher 2025)**
- [Master Claude Code - YouTube](https://www.youtube.com/watch?v=6eBSHbLKuN0) **(Master Claude Code)**
- [The Perfect Commit - Simon Willison](https://simonwillison.net/2022/Oct/29/the-perfect-commit/) **(Willison 2022)**
- [Two Engineers Ship Like a Team of 15 - YouTube](https://www.youtube.com/watch?v=Lh_X32t9_po) **(Two Engineers 2025)**

## Table of Contents
1. [Quick Reference: When to Use Which Pattern](#quick-reference-when-to-use-which-pattern)
2. [Environment Setup & Tool Selection](#environment-setup--tool-selection)
3. [Workflow Patterns](#workflow-patterns)
4. [Code Quality & Architecture](#code-quality--architecture)
5. [Communication & Context Management](#communication--context-management)
6. [Testing & Deployment](#testing--deployment)
7. [Parallelization & Scaling](#parallelization--scaling)
8. [Performance Optimization](#performance-optimization)

---

## Quick Reference: When to Use Which Pattern

### Collaboration Intensity Framework

| **Approach** | **When to Use** | **Task Characteristics** | **Example Scenarios** | **Time Investment** |
|--------------|-----------------|---------------------------|------------------------|-------------------|
| **Full Autonomous** | Small, well-defined specs | - Clear requirements<br>- Known problem domain<br>- Low risk of errors | - Bug fixes<br>- Adding simple features<br>- Code refactoring | Low supervision |
| **One-Shot Guided** | Medium complexity, familiar domain | - Moderately complex<br>- Some ambiguity<br>- Standard patterns | - API endpoint creation<br>- Database migrations<br>- Component development | Single planning session |
| **Synchronous Collaboration** | High complexity or uncertainty | - Complex requirements<br>- Novel problems<br>- High business impact<br>- Learning new domain | - Architecture decisions<br>- Complex algorithms<br>- Critical system changes | Continuous collaboration |
| **Parallel Brainstorming** | Creative/exploratory work | - Multiple valid approaches<br>- Need diverse perspectives<br>- Innovation required | - New feature design<br>- Performance optimization<br>- Technical research | Medium setup, parallel execution |
| **Hybrid Hand-holding → Fan-out** | Large, multi-part projects | - Complex but decomposable<br>- Team learning involved<br>- Quality consistency needed | - Full feature development<br>- System integrations<br>- Team onboarding | High initial, then scalable |

### Task Complexity Decision Tree

```
Is the task well-defined and small?
├─ Yes → **Full Autonomous**
└─ No → Is it familiar domain with moderate complexity?
    ├─ Yes → **One-Shot Guided**
    └─ No → Is it a novel/high-impact problem?
        ├─ Yes → **Synchronous Collaboration**
        └─ No → Do you need multiple approaches?
            ├─ Yes → **Parallel Brainstorming**
            └─ No → Is it large and decomposable?
                └─ Yes → **Hybrid Hand-holding → Fan-out**
```

### Pattern Selection by Risk & Complexity

| **Risk Level** | **Low Complexity** | **Medium Complexity** | **High Complexity** |
|----------------|-------------------|----------------------|-------------------|
| **Low Risk** | Full Autonomous | One-Shot Guided | Parallel Brainstorming |
| **Medium Risk** | One-Shot Guided | Synchronous Collaboration | Hybrid Hand-holding |
| **High Risk** | Synchronous Collaboration | Synchronous Collaboration | Synchronous Collaboration |

### Time vs. Quality Trade-offs

| **Priority** | **Fast Delivery** | **Balanced** | **Highest Quality** |
|--------------|------------------|--------------|-------------------|
| **Approach** | Full Autonomous → One-Shot | Hybrid Hand-holding | Synchronous Collaboration |
| **Best For** | Prototypes, quick fixes | Production features | Critical systems |

---

## Environment Setup & Tool Selection

### Language & Framework Preferences
- **Choose stable, agent-friendly languages**: Go is recommended for backend projects due to its explicit context system, simple test caching, and low ecosystem churn *(Ronacher 2025)*
- **Avoid rapidly changing ecosystems**: JavaScript/Node.js ecosystems can be challenging due to frequent changes *(Ronacher 2025)*
- **Prioritize simplicity**: Languages with clear, straightforward syntax work better with AI assistants *(Ronacher 2025)*

### Tool Design Principles
- **Speed is critical**: Fast compilation and execution boost agent productivity *(Ronacher 2025)*
- **User-friendly design**: Tools should not hang, provide good error messages, and offer debuggability *(Ronacher 2025)*
- **Observability**: Log to files (not just terminal) so agents can investigate issues *(Ronacher 2025)*
- **Protection**: Use containerization (like Docker) for risk management when using autonomous modes *(Raw Notes)*
- **Avoid service conflicts**: Use tools that prevent duplicate service spawning (e.g., pidfiles) *(Raw Notes)*
- **Hot-reload patterns**: For slow applications, create daemon processes that can dynamically load code *(Raw Notes)*

### Autonomous Mode Settings
- **YOLO mode**: Use `--dangerously-skip-permissions` for fully autonomous workflows *(Raw Notes)*
- **Safe autonomy**: Always run autonomous mode inside Docker containers for protection *(Raw Notes)*
- **MCP usage**: Avoid MCP unless essential (e.g., Playwright MCP for browser automation) *(Raw Notes)*

### Development Environment
- **Terminal-based tools**: Enable scriptability and parallel execution *(Master Claude Code)*
- **SSH/tmux support**: Allows running multiple sessions simultaneously *(Master Claude Code)*
- **Dictation setup**: Voice input can speed up communication with AI assistants *(Master Claude Code)*
- **Workspace organization**: Use allowed-tools configurations and terminal setups *(Master Claude Code)*
- **Multi-modal support**: Drag and drop images, use file paths, or copy-paste images directly *(Master Claude Code)*
- **No indexing required**: Code stays local, no remote databases, no training on your code *(Master Claude Code)*

### Onboarding & Team Setup
- **Start with Q&A, not coding**: For team onboarding, begin with codebase questions before editing *(Master Claude Code)*
- **Accelerated onboarding**: Can reduce technical onboarding from weeks to days *(Master Claude Code)*
- **Permission boundaries**: Learn what can be "one-shotted" vs. needs hand-holding *(Master Claude Code)*

---

## Workflow Patterns

### Core Workflow: Explore → Plan → Confirm → Code → Commit *(Master Claude Code)*
1. **Explore**: Understand the codebase using @ tags, Q&A, and onboarding *(Master Claude Code)*
2. **Plan**: Have AI brainstorm or create detailed plans before coding *(Master Claude Code)*
3. **Confirm**: Review and approve plans before implementation *(Master Claude Code)*
4. **Code**: Implement the solution *(Master Claude Code)*
5. **Commit**: Create atomic, well-documented commits *(Master Claude Code)*

### Alternative Workflows
- **Test-Driven Development**: Write tests → commit → code → iterate → commit *(Master Claude Code)*
- **AI-Assisted TDD**: AI writes tests (review carefully) → AI implements → refactor until tests pass *(Raw Notes)*
- **Visual Development**: Write code → screenshot (using Playwright/Puppeteer) → iterate *(Master Claude Code)*
- **Mock-driven development**: Drag/drop UI mocks → AI implements → iterate with screenshots *(Master Claude Code)*
- **Parallel Brainstorming**: Use 3 parallel agents to brainstorm ideas before implementation *(Master Claude Code)*
- **CLI/SDK integration**: Use Claude Code as Unix utility - pipe input/output, JSON formatting *(Master Claude Code)*

### Planning Strategies
- **Break down complex tasks**: Use todo.md files for project planning *(Raw Notes)*
- **Question-driven planning**: Ask "What would a good PM ask about this?" *(Two Engineers 2025)*
- **Focus on user stories**: Center planning around user needs *(Two Engineers 2025)*
- **Look for red flags**: Identify potential issues early in the planning phase *(Two Engineers 2025)*
- **Interview mode**: Ask users for more context before generating solutions *(Two Engineers 2025)*
- **Make plans engaging**: Ask questions and focus on user stories to make plans more readable *(Two Engineers 2025)*

### Beyond Just Coding *(Two Engineers 2025)*
- **Feature research workflow**: Grounding → research current codebase → research best practices → plan → get approval → create GitHub issue
- **Development lifecycle integration**: Use AI for all development-related tasks, not just coding
- **Early intervention**: Fix issues in the planning phase rather than after deployment

---

## Code Quality & Architecture

### Code Style & Patterns
- **Write simple, straightforward code**: Prefer functions over complex classes *(Ronacher 2025, Raw Notes)*
- **Use plain SQL**: Avoid complex ORMs when possible *(Ronacher 2025, Raw Notes)*
- **Keep important checks local**: Permissions and critical logic should be visible and local *(Ronacher 2025)*
- **Favor code generation over dependencies**: Reduces dependency management overhead *(Ronacher 2025)*
- **Minimal dependencies**: Write your own code when possible to avoid upgrade/patch issues *(Raw Notes)*

### Architecture Principles
- **Make things parallelizable**: Design for concurrent execution *(Raw Notes)*
- **Enable easy refactoring**: Plan for code evolution and complexity management *(Raw Notes)*
- **Focus on maintainability**: Write code that's easy for both humans and AI to understand *(Ronacher 2025)*
- **Use structural interfaces**: Clear, explicit interfaces improve AI comprehension *(Ronacher 2025)*

---

## Communication & Context Management

### Context Management with CLAUDE.md *(Master Claude Code)*
Create context files at different levels:
- **Enterprise level**: Organization-wide patterns and standards *(Master Claude Code)*
- **Global level** (`~/.claude/CLAUDE.md`): Personal preferences and tools *(Master Claude Code)*
- **Project level** (checked in): Shared team context *(Master Claude Code)*
- **Project level** (local): Personal project-specific notes *(Master Claude Code)*

Include:
- Bash commands for common tasks *(Master Claude Code)*
- Architecture decisions *(Master Claude Code)*
- Important file locations *(Master Claude Code)*
- Team tools and MCP configurations *(Master Claude Code)*

### Effective Communication
- **Tell Claude to brainstorm first**: Get multiple approaches before implementation *(Master Claude Code)*
- **Provide clear context**: Use @ tags to reference specific files *(Master Claude Code)*
- **Be specific about requirements**: Clear requirements lead to better results *(Master Claude Code)*
- **Ask for explanations**: Have AI explain its approach for complex tasks *(Master Claude Code)*
- **Use specific prompts**: "Before you write code, make a plan" or "Make a plan, run it by me, ask for approval" *(Master Claude Code)*
- **Git integration**: Ask about Git history, commit formats, who introduced changes *(Master Claude Code)*
- **Weekly standups**: "What did I ship this week?" for automated status reports *(Master Claude Code)*

### Interactive Session Management *(Master Claude Code)*
- **Escape to interrupt**: Hit escape to give mid-task feedback or corrections
- **Session resumption**: Use `--resume` or `--continue` to resume previous sessions
- **History navigation**: Escape twice to jump back in session history

---

## Testing & Deployment

### Testing Strategies
- **Comprehensive testing**: Include implementation tests and documentation *(Willison 2022)*
- **Smoke tests**: Quick validation that core functionality works *(Two Engineers 2025)*
- **Visual testing**: Use Figma → Puppeteer → screenshot → code update workflows *(Two Engineers 2025)*
- **Prompt evaluation**: Treat prompts like code - test them, measure success rates, iterate *(Two Engineers 2025)*
- **Iterative self-correction**: Make AI systems fix their own issues through testing feedback *(Two Engineers 2025)*

### Perfect Commit Pattern *(Willison 2022)*
Each commit should include:
1. **Single, focused change**: One atomic improvement *(Willison 2022)*
2. **Tests demonstrating the change works**: Comprehensive test coverage *(Willison 2022)*
3. **Updated documentation**: Reflecting the change *(Willison 2022)*
4. **Link to issue/context**: Providing further background *(Willison 2022)*

### Deployment Practices
- **Keep main branch deployable**: Ensure commits don't break the build *(Willison 2022)*
- **Atomic commits**: Each commit should be self-contained and reviewable *(Willison 2022)*
- **Clear commit messages**: Focus on "why" rather than "what" *(Willison 2022)*
- **Use branches for experiments**: Keep experimental work separate from main *(Willison 2022)*

---

## Parallelization & Scaling

### Parallel Development Approaches
- **Multiple Claude instances**: Run different work streams in parallel *(Master Claude Code)*
- **Git worktrees**: Work on multiple branches simultaneously *(Master Claude Code)*
- **GitHub Actions**: Automate parallel workflows *(Master Claude Code)*
- **Claude Squad management**: Coordinate multiple AI assistants from a central location *(Raw Notes)*

### Task Distribution
- **Do different work in parallel**: Assign different features to different instances *(Raw Notes)*
- **Parallel problem-solving**: Have multiple instances solve the same problem and pick the best approach *(Raw Notes)*
- **Research parallelization**: Run research tasks concurrently to speed up information gathering *(Two Engineers 2025)*

### Hybrid Approach *(Raw Notes)*
- **Discuss plans with AI**: Question and validate understanding *(Raw Notes)*
- **Try one instance**: Test the approach with a single case *(Raw Notes)*
- **Provide feedback**: Give input on the approach *(Raw Notes)*
- **Scale with multiple agents**: Fan out to multiple sub-agents for parallel execution *(Raw Notes)*

---

## Performance Optimization

### Speed Optimization
- **Fast tool responses**: Minimize latency in tool interactions *(Ronacher 2025)*
- **Quick compilation**: Choose languages and tools that compile/execute quickly *(Ronacher 2025)*
- **Efficient token usage**: Optimize for token efficiency to reduce costs *(Ronacher 2025)*
- **Minimize interruptions**: Allow agents to complete tasks with minimal intervention *(Ronacher 2025)*

### Resource Management
- **Use cheaper models**: Claude Sonnet for many tasks instead of more expensive models *(Ronacher 2025)*
- **Cache effectively**: Implement caching for repeated operations *(Ronacher 2025)*
- **Batch operations**: Group related tasks to reduce overhead *(Ronacher 2025)*
- **Optimize for inference cost**: Design workflows to minimize API calls *(Ronacher 2025)*

### Workflow Efficiency
- **Containerization**: Use Docker for safe autonomous execution *(Raw Notes)*
- **Daemon patterns**: Create long-running processes for frequently used tools *(Ronacher 2025)*
- **File system watching**: Implement hot-reload patterns for rapid iteration *(Ronacher 2025)*
- **Logging strategies**: Structured logging for better debugging and monitoring *(Ronacher 2025)*
- **Tiered permission system**: Complex allow/block lists for safe bash command execution *(Master Claude Code)*
- **Static analysis**: Automatic detection of safe command combinations *(Master Claude Code)*

---

## Advanced Patterns

### Compounding Engineer Approach *(Two Engineers 2025)*
- **Prompt-generating prompts**: Create AI that can create better prompts *(Two Engineers 2025)*
- **Self-improving workflows**: Build systems that enhance their own processes *(Two Engineers 2025)*
- **Knowledge accumulation**: Build on previous work to compound effectiveness *(Two Engineers 2025)*

### Meta-Development Patterns
- **Full lifecycle integration**: Use AI beyond coding - for research, planning, issue creation *(Two Engineers 2025)*
- **Self-healing systems**: Create systems where AI can investigate and fix its own errors *(Raw Notes)*
- **Dynamic code loading**: For slow applications, create hot-reload systems for rapid iteration *(Raw Notes)*

### Quality Assurance
- **Fix early in the cycle**: Address issues in planning rather than after deployment *(Two Engineers 2025)*
- **Multiple validation layers**: Use different approaches to verify correctness *(Two Engineers 2025)*
- **Continuous evaluation**: Regular assessment of AI system performance *(Two Engineers 2025)*
- **Feedback loops**: Learn from mistakes to improve future performance *(Two Engineers 2025)*

### Research & Development
- **Grounding research**: Understand current codebase before proposing changes *(Two Engineers 2025)*
- **Best practice research**: Study industry standards and patterns *(Two Engineers 2025)*
- **Plan validation**: Check plans with stakeholders before implementation *(Two Engineers 2025)*
- **Issue tracking**: Create GitHub issues for feature requests and bugs *(Two Engineers 2025)*

---

## Getting Started Checklist

For beginners starting with agentic coding:

1. **Set up your environment**
   - [ ] Install Claude Code or similar AI coding assistant
   - [ ] Configure terminal and shell for optimal workflow
   - [ ] Set up allowed-tools and permissions

2. **Create your CLAUDE.md files**
   - [ ] Global configuration at `~/.claude/CLAUDE.md`
   - [ ] Project-specific context files
   - [ ] Document common commands and architecture decisions

3. **Establish workflows**
   - [ ] Practice the Explore → Plan → Confirm → Code → Commit pattern
   - [ ] Try test-driven development with AI assistance
   - [ ] Experiment with parallel brainstorming

4. **Focus on code quality**
   - [ ] Write simple, readable code
   - [ ] Minimize dependencies
   - [ ] Plan for refactoring and evolution

5. **Experiment and iterate**
   - [ ] Try different approaches to find what works for your team
   - [ ] Adapt patterns to your specific domain and requirements
   - [ ] Keep experimenting as the field evolves rapidly

Remember: The "good" approach for agentic coding is changing rapidly. Stay adaptable and keep experimenting with new tools and techniques as they emerge. *(Ronacher 2025)*


