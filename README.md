# Tech Lead for Claude Code

A cost-optimized task routing system for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Give it a complex task — it decomposes it into subtasks and delegates each to the right-sized AI agent.

## How It Works

Run the slash command in Claude Code:

```
/tech-lead <your task description>
```

The tech lead will:

1. **Analyze** — explore the codebase and understand the scope of your task
2. **Decompose** — break it into the smallest independent subtasks, classify each by complexity
3. **Delegate** — route each subtask to the appropriate agent tier and execute in parallel where possible

## Agent Tiers

| Tier | Model | Best For |
|------|-------|----------|
| **junior-dev** | Haiku | Boilerplate, renames, type additions, simple tests, formatting |
| **mid-dev** | Sonnet | Standard features, moderate bugs, single-file refactors, API endpoints |
| **senior-dev** | Opus | Architecture decisions, cross-module refactors, security, performance |

## Cost Optimization

The system biases toward cheaper agents — aiming for **60%+ of subtasks** routed to junior-dev or mid-dev. Senior-dev (Opus) is only used when genuine complexity demands it.

Independent subtasks run **in parallel**, reducing both cost and wall-clock time.

## Setup

1. Clone this repo
2. Make sure you have [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
3. Run Claude Code from the repo root — the `/tech-lead` command will be available automatically

### Recommended: Pre-approve subagent permissions

For the cost savings to work, subagents need file read/write access. You can configure this in your Claude Code permissions settings, or approve the prompts when they appear.

## Project Structure

```
.claude/
├── commands/
│   └── tech-lead.md      # The /tech-lead slash command
└── agents/
    ├── junior-dev.md      # Haiku-powered agent for simple tasks
    ├── mid-dev.md         # Sonnet-powered agent for standard work
    └── senior-dev.md      # Opus-powered agent for complex work
CLAUDE.md                  # Project-level routing instructions
```

## Example

```
/tech-lead Add user authentication with JWT tokens, login/signup endpoints, and middleware
```

The tech lead might decompose this into:
- **junior-dev**: Create user model boilerplate, add type definitions
- **mid-dev**: Implement login/signup API endpoints, write auth middleware
- **senior-dev**: Design token refresh strategy, review security of auth flow

## License

MIT
