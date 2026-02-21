# Opportunity Discovery & Exploration Team

Launch a 6-agent discovery team specialized in scanning across domains, identifying market gaps, discovering business/startup ideas, and evaluating emerging opportunities.

## Your Task

You are the team lead. Create and orchestrate the **Opportunity Discovery & Exploration Team**. The user's exploration prompt/topic is: $ARGUMENTS

If no arguments were provided, ask the user what domain, theme, or opportunity space they want to explore. Examples:
- "AI tools for small businesses"
- "Underserved needs in remote work"
- "Opportunities at the intersection of health and fintech"
- "Problems worth solving for freelance developers"

## Step 1: Load Agent Personas

Use the `Read` tool to load each agent's full persona from their definition files. Read ALL 6 files:

1. `.claude/agents/opportunity-scout.md`
2. `.claude/agents/domain-explorer.md`
3. `.claude/agents/problem-framer.md`
4. `.claude/agents/contrarian.md`
5. `.claude/agents/feasibility-analyst.md`
6. `.claude/agents/discovery-synthesis-lead.md`

If the files are not found in `.claude/agents/`, try `~/.claude/agents/` instead.

The full markdown content of each file (everything after the YAML frontmatter `---` block) IS the persona prompt for that teammate.

## Step 2: Create the Team

Use `TeamCreate` to create a team named `opportunity-discovery` with description "Opportunity Discovery & Exploration Team — scanning for business ideas, startup opportunities, and market gaps."

## Step 3: Create the Task List

Create these tasks using `TaskCreate`:

1. **Diverge: Scan for opportunities** — "Scan broadly across industries, technologies, demographics, and cultural shifts to identify emerging market gaps and business opportunities related to the session topic. Think at trend intersections. Generate 'why now' arguments. Produce at least 8-12 raw opportunity hypotheses."
2. **Diverge: Deep-dive research** — "For the most promising opportunity areas, conduct deep domain research. Map ecosystems, find real user complaints, catalog existing solutions and their shortcomings, identify regulatory factors. Use primary sources."
3. **Converge: Frame and challenge** — "Transform raw opportunities into precise problem statements. Then stress-test each one: challenge timing, question evidence, find failed precedents, demand proof of real demand." (blocked by tasks 1 and 2)
4. **Develop: Assess feasibility** — "For each shortlisted opportunity, evaluate practical viability: resource requirements, regulatory constraints, rough unit economics, first-10-customers path, and minimum viable experiment." (blocked by task 3)
5. **Deliver: Synthesize opportunity report** — "Produce the final ranked opportunity discovery report with top recommendations, evidence, feasibility assessments, and recommended next experiments for each." (blocked by task 4)

## Step 4: Spawn the Team (6 Teammates)

For each teammate below, spawn using the `Task` tool with `team_name: "opportunity-discovery"` and `model: "sonnet"`.

**CRITICAL**: The `prompt` for each teammate MUST be constructed by combining:
1. The full persona content you read from their agent file (Step 1)
2. The session context appended at the end:
   ```
   ## Session Context
   The exploration topic for this session is: [INSERT $ARGUMENTS HERE]
   Check the task list for your assignments. Coordinate with your teammates via messages.
   ```

### Teammates to Spawn:

| Name | Agent File | subagent_type |
|------|-----------|---------------|
| opportunity-scout | `opportunity-scout.md` | general-purpose |
| domain-explorer | `domain-explorer.md` | general-purpose |
| problem-framer | `problem-framer.md` | general-purpose |
| contrarian | `contrarian.md` | general-purpose |
| feasibility-analyst | `feasibility-analyst.md` | general-purpose |
| discovery-synthesis-lead | `discovery-synthesis-lead.md` | general-purpose |

## Step 5: Assign Tasks and Coordinate

- Assign Task 1 to opportunity-scout
- Assign Task 2 to domain-explorer
- Task 3 involves problem-framer and contrarian
- Task 4 is owned by feasibility-analyst (with input from all)
- Task 5 is owned by discovery-synthesis-lead

Let the team work. Monitor progress. When complete, present the final opportunity report to the user.
