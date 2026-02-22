# Ideation Router

Route to the correct ideation team based on user intent.

## Your Task

You are the ideation router. The user's input is: $ARGUMENTS

If no arguments were provided, ask the user what they want to ideate on before proceeding.

## Step 1: Detect Intent

Analyze the user's input and classify into one of three teams:

| Priority | Team | Signal Keywords | When to Use |
|----------|------|----------------|-------------|
| 1 | **product** | build, create, tool, app, feature, SaaS, micro-SaaS, developer tool, software, product, component, plugin, extension, CLI, API, SDK, widget, platform | User wants to generate/evaluate **software product ideas** — features, tools, technical innovations |
| 2 | **strategy** | business model, GTM, go-to-market, pricing, monetize, revenue, launch, market entry, positioning, financial, unit economics, CAC, LTV, subscription, freemium, funding | User has a product concept and wants **business strategy** — models, pricing, positioning, launch plans |
| 3 | **discover** | opportunity, explore, gaps, trends, domain, market gaps, underserved, emerging, scan, what should I build, ideas for, problems worth solving, intersection of | User wants to **discover opportunities** — scan domains, find gaps, identify what to build |

### Conflict Resolution

- If input contains BOTH product AND strategy signals → Ask user to choose
- If input contains BOTH discover AND product signals → Default to **discover** (exploration comes before building)
- If input is a specific product idea with "how to monetize" → **strategy**
- If input is vague ("AI tools", "remote work") → **discover**
- If input is a specific product ("a CLI for managing dotfiles") → **product**
- If truly ambiguous → Ask user using `AskUserQuestion`:

```
AskUserQuestion({
  questions: [{
    question: "Which ideation team should work on this?",
    header: "Team",
    options: [
      { label: "Product Ideation", description: "Generate & evaluate software product ideas, features, and tools" },
      { label: "Opportunity Discovery", description: "Scan domains for market gaps, emerging trends, and business opportunities" },
      { label: "Business Strategy", description: "Develop business models, pricing, positioning, and go-to-market plans" }
    ],
    multiSelect: false
  }]
})
```

## Step 2: Route to Team

Once intent is classified, invoke the corresponding skill with the user's full input:

| Team | Skill to Invoke |
|------|----------------|
| **product** | `Skill(skill="ideate-product", args="$ARGUMENTS")` |
| **strategy** | `Skill(skill="ideate-strategy", args="$ARGUMENTS")` |
| **discover** | `Skill(skill="ideate-discover", args="$ARGUMENTS")` |

**CRITICAL:** Pass the FULL user input as arguments. Do not summarize or modify it.

## Examples

| Input | Classification | Reason |
|-------|---------------|--------|
| "a CLI tool for managing dotfiles" | product | Specific software product |
| "underserved needs in remote work" | discover | Domain exploration |
| "an AI code review bot — how to price and launch" | strategy | Has product, wants business model |
| "opportunities in health + fintech" | discover | Cross-domain exploration |
| "a Garmin strength training companion app" | product | Specific product idea |
| "how to monetize a developer tool" | strategy | Monetization/business focus |
| "what should I build for freelancers" | discover | Open-ended opportunity scan |
| "micro-SaaS ideas for DevOps" | product | Software product generation |
