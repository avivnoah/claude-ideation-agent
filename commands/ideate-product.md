# Software & Product Ideation Team

Launch a 6-agent ideation team specialized in generating, evaluating, and refining software product ideas — features, developer tools, micro-SaaS concepts, and technical innovations.

## Your Task

You are the team lead. Create and orchestrate the **Software & Product Ideation Team**. The user's ideation prompt/topic is: $ARGUMENTS

If no arguments were provided, ask the user what software product / feature / tool / micro-SaaS concept they want to ideate on before proceeding.

## Step 1: Load Agent Personas

Use the `Read` tool to load each agent's full persona from their definition files. Read ALL 6 files:

1. `.claude/agents/product-visionary.md`
2. `.claude/agents/technical-architect.md`
3. `.claude/agents/user-advocate.md`
4. `.claude/agents/market-analyst.md`
5. `.claude/agents/devils-advocate.md`
6. `.claude/agents/product-synthesis-lead.md`

If the files are not found in `.claude/agents/`, try `~/.claude/agents/` instead.

The full markdown content of each file (everything after the YAML frontmatter `---` block) IS the persona prompt for that teammate.

## Step 2: Create the Team

Use `TeamCreate` to create a team named `product-ideation` with description "Software & Product Ideation Team — generating and evaluating software product ideas."

## Step 3: Create the Task List

Create these tasks using `TaskCreate`:

1. **Diverge: Generate product ideas** — "Brainstorm a high volume of diverse software product ideas related to the session topic. Focus on quantity, not quality. Think across domains, user segments, and technology approaches. NO evaluation at this stage."
2. **Diverge: Research market landscape** — "Research the competitive landscape, market trends, and existing solutions related to the session topic. Identify gaps, underserved segments, and emerging opportunities. Provide evidence and data."
3. **Converge: Evaluate and shortlist** — "Critically evaluate all generated ideas. Challenge assumptions, identify risks, assess technical feasibility and market viability. Shortlist the top 3-5 ideas based on evidence." (blocked by tasks 1 and 2)
4. **Develop: Enrich top ideas** — "For each shortlisted idea, develop detailed user stories, technical architecture sketches, competitive positioning, and risk assessment." (blocked by task 3)
5. **Deliver: Synthesize final recommendations** — "Produce the final ranked output document with top recommendations, evidence, risks, and next steps." (blocked by task 4)

## Step 4: Spawn the Team (6 Teammates)

For each teammate below, spawn using the `Task` tool with `team_name: "product-ideation"` and `model: "sonnet"`.

**CRITICAL**: The `prompt` for each teammate MUST be constructed by combining:
1. The full persona content you read from their agent file (Step 1)
2. The session context appended at the end:
   ```
   ## Session Context
   The ideation topic for this session is: [INSERT $ARGUMENTS HERE]
   Check the task list for your assignments. Coordinate with your teammates via messages.
   ```

### Teammates to Spawn:

| Name | Agent File | subagent_type |
|------|-----------|---------------|
| product-visionary | `product-visionary.md` | general-purpose |
| technical-architect | `technical-architect.md` | general-purpose |
| user-advocate | `user-advocate.md` | general-purpose |
| market-analyst | `market-analyst.md` | general-purpose |
| devils-advocate | `devils-advocate.md` | general-purpose |
| product-synthesis-lead | `product-synthesis-lead.md` | general-purpose |

## Step 5: Assign Tasks and Coordinate

- Assign Task 1 to product-visionary
- Assign Task 2 to market-analyst
- Task 3 (evaluation) involves devils-advocate, technical-architect, and user-advocate
- Task 4 (development) involves all teammates
- Task 5 (synthesis) is owned by product-synthesis-lead

Let the team work. Monitor progress. When complete, present the final output document to the user.
