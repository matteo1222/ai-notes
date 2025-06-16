https://lucumr.pocoo.org/2025/6/12/agentic-coding/

- use yolo mode --dangerously-skip-permissions for autonomous workflow
  - but do it in docker for some protection
- dont use mcp unless other tools are too hard to use like playwright mcp
- use Golang, it is easy for agent to use
- tools should be designed to be very user friendly - should not hang - inform good error - debuggability and observability
  > I use a [fork of shoreman](https://gist.github.com/mitsuhiko/8ca80fda0bf48045d54bcd34d76ad887) which writes a pidfile. When spanwed a second time it errors and logs “services already running”. Why does that matter? Because the agent sometimes does not know if the server is already running and otherwise happily spawns it a second time resulting in two version of the service bound to the same port.
- dont just log in terminal, log it into file for agent to investigate
- speed is important, compilation speed and execuetion speed boost agent productivity, becasue it can try things see result

  > If your stuff is indeed slow, then consider vibe-coding a demon that you can dynamically load stuff into. As an example Sentry takes too long to reload code and it takes too long to restart. To trial some agentic coding there my workaround was a module that watches a file system location and just imports and executes all python modules placed there, then writes the outputs into a log it can cat. That's not perfect, but it was a significant help for the agent to evaluate some basic code in the context of the application.
  > what this mean?

- avoid dependency, use agent to write your own code
  - no need to manage for dpeendenedy upgrade/patch
  - can fix bug easily yourself/with agent
- write simple code

  - function
  - plain sql

- make things parallelizable
- learn to refactor
- keep experiementing, the "good" approach for agentic coding is changing rapidly

---

Master Claude Code
https://www.youtube.com/watch?v=6eBSHbLKuN0

- terminal based, meaning it's scriptable
- can run in parallel, ssh/tmux
- recommend setup
  - /allowed-tools
  - /terminal-setup
  - Turn on MacOS Dictation
- understand codebase
  - Q & A, onboarding
  - use @ tag file
- editing code
  - tell claude to brainstorm or plan first
  - 3 parallel agent to brainstorm ideas before you write code
- tell claude about your team's tools/mcp
- common workflow
  - explore -> plan -> confirm -> code -> commit
  - write test -> commit -> code -> iterate -> commit
  - write code -> screenshot (playwright mcp/ puppeteer mcp)-> iterate
- give context

  - CLAUDE.md
    - project level
    - user level
      ~/.claude/CLAUDE.md
    - bash commands, architecture decision, important file, keep it short
  - different level
    - enterprise -> global (just me) -> project (checked in) -> project (just me)

- run it in parallel
  - tmux/worktree
  - github actions

---

MCP are boring
https://www.youtube.com/watch?v=J3oJqan2Gv8&t=1579s

---

- make todo.md for project planning

---

TDD - ai write test (review carefully), ai implement, refactor until all test pass

---

autonomus vs hand holding
hybrid approach

- discuss about the plan, question agent if it understand it, try one instance, give feedback, try 2 more, fan out to multiple subagent to do it all

---

https://simonwillison.net/2022/Oct/29/the-perfect-commit/
perfect commit

> The implementation: a single, focused change
> Tests that demonstrate the implementation works
> Updated documentation reflecting the change
> A link to an issue thread providing further context

---

## claude squad, manage claude code in a central place

- parallism, do different work in parallel
- do single work in parallel and pick the best approach


--- 
two engineer ship like a team of 15
https://www.youtube.com/watch?v=Lh_X32t9_po

- use claude code to not just do coding, do all the other things related to deveopement
- do research on a feature request
	- grounding, research current code base find out what we have
	- research best practice
	- make a plan, check in with user for approval
	- create github issue
- compounding engineer
	- make a prompt that can make prompts
- fix in the earliest part of things
	- meaning in the development cycle
		- plan -> write code -> commit -> push -> production
		- in plan phrase just fix things already steer the direction
- plans, make plan more fun to read
	- ask question
		- "What would good PM ask about this"
	- focus on user stories
	- look for red flags
- interview mode -> ask user about more context what they want, then generate output
- tests, evals is important
	- smoke test
	- make it iterate and fix things itself
	- figma -> puppeteer -> screenshot -> code update
	- eval is test for prompt
		- use a prompt, succeed 4 out of 10 times
		- iterate prompt
 

---
Reddit: I discovered a powerful way to continuously improve my CLAUDE\.md instructions for Claude Code
https://www.reddit.com/r/ClaudeAI/comments/1laby6h/i_discovered_a_powerful_way_to_continuously/

> I created a project reflection command specifically for optimizing the CLAUDE.md file itself. Now I can run /project:reflection anytime, and Claude Code analyzes my current instructions and suggests improvements. This creates a feedback loop where my coding agent gets progressively better.

custom command: /project:reflection

prompt
```
You are an expert in prompt engineering, specializing in optimizing AI code assistant instructions. Your task is to analyze and improve the instructions for Claude Code found in u/CLAUDE.md. Follow these steps carefully:

1. Analysis Phase:
Review the chat history in your context window.

Then, examine the current Claude instructions:
<claude_instructions>
u/CLAUDE.md
</claude_instructions>

Analyze the chat history and instructions to identify areas that could be improved. Look for:
- Inconsistencies in Claude's responses
- Misunderstandings of user requests
- Areas where Claude could provide more detailed or accurate information
- Opportunities to enhance Claude's ability to handle specific types of queries or tasks

2. Interaction Phase:
Present your findings and improvement ideas to the human. For each suggestion:
a) Explain the current issue you've identified
b) Propose a specific change or addition to the instructions
c) Describe how this change would improve Claude's performance

Wait for feedback from the human on each suggestion before proceeding. If the human approves a change, move it to the implementation phase. If not, refine your suggestion or move on to the next idea.

3. Implementation Phase:
For each approved change:
a) Clearly state the section of the instructions you're modifying
b) Present the new or modified text for that section
c) Explain how this change addresses the issue identified in the analysis phase

4. Output Format:
Present your final output in the following structure:

<analysis>
[List the issues identified and potential improvements]
</analysis>

<improvements>
[For each approved improvement:
1. Section being modified
2. New or modified instruction text
3. Explanation of how this addresses the identified issue]
</improvements>

<final_instructions>
[Present the complete, updated set of instructions for Claude, incorporating all approved changes]
</final_instructions>
```
