# Throng

**Run your AI coding agents remotely. Review and ship from anywhere.**

Throng is a Claude Code orchestration platform that manages your coding agents so you don't have to. Define a task, review the plan, then let Throng handle the rest — building, testing, and raising a PR while you focus on what matters.

---

## How it works

Throng follows an opinionated Kanban workflow where agents handle analysis, planning, and development — prompting you only when human input is needed.

<div class="grid cards" markdown>

-   :material-plus-circle:{ .lg .middle } **1. Create a task**

    ---

    Add a task card and move it to the **Planning** column. Include as much or as little detail as you like.

-   :material-file-document-edit:{ .lg .middle } **2. Agent plans**

    ---

    Claude analyses your task, writes an implementation plan, and notifies you if it needs more detail.

-   :material-check-circle:{ .lg .middle } **3. Review the plan**

    ---

    Refine the plan in conversation with Claude. Approving it moves the card to **Ready**.

-   :material-code-braces:{ .lg .middle } **4. Agent builds**

    ---

    Development kicks off automatically according to your WIP limits. Each Claude session runs in full isolation — run as many in parallel as you like.

-   :material-source-pull:{ .lg .middle } **5. PR raised & reviewed**

    ---

    Claude submits a pull request. Any review feedback is automatically passed back to Claude for revision.

-   :material-flag-checkered:{ .lg .middle } **6. Done**

    ---

    Once the PR is merged, the task moves to **Done** automatically.

</div>

---

## Key benefits

- **No more juggling git worktrees.** Every task runs in its own isolated sandbox — branches, dependencies, and all.
- **Bypass permission interruptions.** Throng runs Claude in a dedicated, controlled environment so agents can work uninterrupted.
- **Walk away.** Throng notifies you when agents are blocked or ready for more work. No need to sit at your desk.
- **Flexible handoff.** Write a detailed spec on your own machine, then hand it off to Throng for implementation.
- **Superpowers built in.** Throng integrates with the Superpowers plugin for the best possible agent experience out of the box.

---

## Hosting options

### Self-hosted

Throng works best on a dedicated, always-on machine. A **Mac Mini** is a great option.

[Get started with self-hosting →](install.md)

### Docker Compose

Run Throng alongside your existing infrastructure using Docker Compose.

[Docker Compose setup →](docker-compose.md)

### Cloud hosting

Don't have a dedicated machine? Choose a cloud hosting option and be up and running within minutes.

!!! tip "Coming soon"
    Cloud hosting options are on the roadmap. Follow the repo for updates.
