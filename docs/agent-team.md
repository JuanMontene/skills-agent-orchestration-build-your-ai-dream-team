# Project Pulse agent team

The custom agents for Mona's Project Pulse dashboard live in `.github/agents/`. They run from GitHub Copilot CLI.

| Agent | Model | Responsibility | File |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 | Breaks the request into tasks, delegates them to the specialists with an explicit file scope, tracks each phase and reports the result. It coordinates but does not implement, and it does not run git. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 | Researches the repository and creates the implementation plan: phases, file ownership, dependencies, edge cases and risks. It does not write code. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.7 Flash | Owns the user experience: usability, accessibility, information hierarchy, interaction flow and visual design of the dashboard. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 | Implements the code in the files the Orchestrator assigns: the static app and its support configuration, such as `.vscode/launch.json`. | `.github/agents/coder.agent.md` |

## How the team will build Project Pulse

1. **Plan:** I ask the Orchestrator for Project Pulse. It asks the Planner for a phased plan with file ownership and dependencies, saved in `docs/`.
2. **Design:** the Orchestrator gives the Designer the dashboard experience (layout, hierarchy, accessibility, styling direction).
3. **Build:** the Orchestrator gives the Coder an explicit file scope: `app/index.html`, `app/styles.css`, `app/project-data.json` and `.vscode/launch.json`. Work runs in parallel only when the file scopes don't overlap; otherwise it runs in sequence.
4. **Validate and hand off:** the Orchestrator checks that the pieces fit together, runs the dashboard, and summarizes the final handoff.

I keep control of git: I stage, commit and push through Copilot CLI prompts.
