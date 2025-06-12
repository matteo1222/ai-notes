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
  - explore -> plan -> confirm -> implement -> test -> deploy

---

MCP are boring
https://www.youtube.com/watch?v=J3oJqan2Gv8&t=1579s

---

https://www.youtube.com/watch?v=fQL1A4WkuJk

- make todo.md for project planning

---

TDD - ai write test (review carefully), ai implement, refactor until all test pass

---

autonomus vs hand holding
hybrid approach

- discuss about the plan, question agent if it understand it, try one instance, give feedback, try 2 more, fan out to multiple subagent to do it all
