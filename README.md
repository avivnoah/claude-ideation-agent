# Claude Ideation Agent

Multi-agent ideation teams for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Three specialized 6-agent teams that run collaborative ideation sessions using Claude's native multi-agent orchestration.

Each team follows a **Diverge > Converge > Develop > Deliver** workflow — agents brainstorm in parallel, then evaluate, refine, and synthesize into a final deliverable.

## Teams

### `/ideate-product` — Software & Product Ideation

Generate, evaluate, and refine software product ideas.

| Agent | Role |
|-------|------|
| **Product Visionary** | Creative idea generator — spawns novel concepts, spots unmet needs |
| **Technical Architect** | Feasibility evaluator — assesses architectures, identifies complexity |
| **User Advocate** | User-centered design thinker — frames problems as user stories |
| **Market Analyst** | Competitive intelligence — analyzes market size, trends, pricing |
| **Devil's Advocate** | Critical evaluator — stress-tests ideas, challenges assumptions |
| **Synthesis Lead** | Orchestrator — manages workflow, drives convergence, produces output |

**Output**: Ranked product recommendations with evidence, risks, and next steps.

### `/ideate-discover` — Opportunity Discovery & Exploration

Scan across domains to identify market gaps and business opportunities.

| Agent | Role |
|-------|------|
| **Opportunity Scout** | Cross-domain pattern spotter — scans trends for emerging gaps |
| **Domain Explorer** | Deep-dive researcher — maps ecosystems, uncovers hidden pain points |
| **Problem Framer** | Precision specialist — transforms vague observations into sharp problem statements |
| **Contrarian** | Hypothesis challenger — questions timing, demands evidence |
| **Feasibility Analyst** | Viability assessor — evaluates resources, regulations, unit economics |
| **Synthesis Lead** | Orchestrator — balances breadth vs depth, produces ranked report |

**Output**: Ranked opportunity report with feasibility assessments and recommended experiments.

### `/ideate-strategy` — Business Strategy & Go-to-Market

Develop business models, positioning, financial projections, and launch plans.

| Agent | Role |
|-------|------|
| **Strategic Visionary** | Business model designer — develops moats, expansion paths, positioning |
| **Market Intelligence** | Competitive analyst — maps landscapes, analyzes pricing, benchmarks |
| **Financial Modeler** | Numbers specialist — builds unit economics, CAC/LTV, break-even models |
| **Customer Strategist** | Segmentation expert — defines personas, buying journeys, messaging |
| **Risk Assessor** | Strategic risk analyst — models failure scenarios, identifies contingencies |
| **GTM Architect** | Execution planner — designs launch sequences, 30-60-90 day roadmaps |

**Output**: Strategy document with business model, financials, customer strategy, risk assessment, and GTM plan.

## Installation

Copy the `agents/` and `commands/` directories into your project's `.claude/` directory:

```bash
# From your project root
mkdir -p .claude
cp -r agents/ .claude/agents/
cp -r commands/ .claude/commands/
```

Or copy them to `~/.claude/` to make the teams available globally across all projects:

```bash
cp -r agents/ ~/.claude/agents/
cp -r commands/ ~/.claude/commands/
```

## Usage

In Claude Code, run a slash command with your topic:

```
/ideate-product a CLI tool for managing dotfiles across machines

/ideate-discover underserved needs in remote work tooling

/ideate-strategy an AI-powered code review bot for small teams
```

If you run a command without arguments, the team lead will ask you for a topic.

## How It Works

Each slash command:

1. Spawns a team lead agent
2. The lead creates a 6-agent team with specialized personas
3. Tasks are created with dependencies (diverge before converge)
4. Agents work in parallel where possible, coordinating via messages
5. The synthesis lead produces the final deliverable

Agent personas are built on established innovation frameworks including Basadur's creative problem-solving profiles, Belbin's team roles, De Bono's thinking hats, and Carla Johnson's innovation archetypes.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) with multi-agent support
- A Claude plan that supports agent teams (Max or Team plans)

## License

MIT
