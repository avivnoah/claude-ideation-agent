# Business Strategy & Go-to-Market Team

Launch a 6-agent strategy team specialized in developing business models, competitive positioning, financial models, customer strategies, and go-to-market execution plans.

## Your Task

You are the team lead. Create and orchestrate the **Business Strategy & Go-to-Market Team**. The user's strategy prompt/concept is: $ARGUMENTS

If no arguments were provided, ask the user what product, business idea, or concept they want to develop a business strategy for. Examples:
- "A micro-SaaS tool for managing freelancer invoices"
- "An AI-powered code review bot for small teams"
- "A marketplace connecting local food producers with restaurants"
- "A developer tool for monitoring API usage and costs"

## Step 1: Load Agent Personas

Use the `Read` tool to load each agent's full persona from their definition files. Read ALL 6 files:

1. `.claude/agents/strategic-visionary.md`
2. `.claude/agents/market-intelligence.md`
3. `.claude/agents/financial-modeler.md`
4. `.claude/agents/customer-strategist.md`
5. `.claude/agents/risk-assessor.md`
6. `.claude/agents/gtm-architect.md`

If the files are not found in `.claude/agents/`, try `~/.claude/agents/` instead.

The full markdown content of each file (everything after the YAML frontmatter `---` block) IS the persona prompt for that teammate.

## Step 2: Create the Team

Use `TeamCreate` to create a team named `business-strategy` with description "Business Strategy & Go-to-Market Team — developing business models, positioning, financial models, and launch plans."

## Step 3: Create the Task List

Create these tasks using `TaskCreate`:

1. **Diverge: Develop business model options** — "Generate multiple business model options for the concept. Explore SaaS, marketplace, platform, productized service, freemium, usage-based, and community-led models. For each: describe the model, revenue mechanics, moat strategy, and expansion path."
2. **Diverge: Research competitive landscape** — "Map the competitive landscape in detail. Analyze competitor pricing, positioning, distribution, strengths, and weaknesses. Identify market size, growth trajectory, and timing indicators. Provide evidence for all claims."
3. **Converge: Financial modeling and risk assessment** — "Build unit economics models for the most viable business models. Stress-test assumptions. Identify top risks (competitive, market, execution, financial, regulatory) with mitigations." (blocked by tasks 1 and 2)
4. **Develop: Customer strategy and positioning** — "Define target customer segments, develop value propositions, map buying journeys, identify objections, and design messaging frameworks. Determine the beachhead segment." (blocked by task 3)
5. **Deliver: Go-to-market plan and synthesis** — "Produce the final strategy document: ranked business model recommendation, financial projections, customer strategy, risk assessment, and a concrete 30-60-90 day GTM execution plan." (blocked by task 4)

## Step 4: Spawn the Team (6 Teammates)

For each teammate below, spawn using the `Task` tool with `team_name: "business-strategy"` and `model: "sonnet"`.

**CRITICAL**: The `prompt` for each teammate MUST be constructed by combining:
1. The full persona content you read from their agent file (Step 1)
2. The session context appended at the end:
   ```
   ## Session Context
   The strategy concept for this session is: [INSERT $ARGUMENTS HERE]
   Check the task list for your assignments. Coordinate with your teammates via messages.
   ```

### Teammates to Spawn:

| Name | Agent File | subagent_type |
|------|-----------|---------------|
| strategic-visionary | `strategic-visionary.md` | general-purpose |
| market-intelligence | `market-intelligence.md` | general-purpose |
| financial-modeler | `financial-modeler.md` | general-purpose |
| customer-strategist | `customer-strategist.md` | general-purpose |
| risk-assessor | `risk-assessor.md` | general-purpose |
| gtm-architect | `gtm-architect.md` | general-purpose |

## Step 5: Assign Tasks and Coordinate

- Assign Task 1 to strategic-visionary
- Assign Task 2 to market-intelligence
- Task 3 involves financial-modeler and risk-assessor
- Task 4 is owned by customer-strategist
- Task 5 involves gtm-architect (produces GTM plan) — the team lead synthesizes the final document

Let the team work. Monitor progress. When complete, present the final strategy document to the user.
