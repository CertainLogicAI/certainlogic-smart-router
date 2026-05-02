# CertainLogic Smart Router

**Route queries to the right model tier. Save money without thinking about it.**

v1.0.0

---

## What It Actually Does

A **keyword-based query classifier** that recommends which LLM tier to use:

| Tier | Use For | Example |
|------|---------|---------|
| **cheap** | Simple lookups, greetings, short answers | "What is Python?", "Hello!" |
| **default** | Standard tasks, explanations, drafting | "Write a function", "Explain recursion" |
| **powerful** | Complex reasoning, architecture, strategy | "Design a distributed system", "Optimize this algorithm" |

**How:** Scans your query for keywords and patterns. Picks the cheapest tier that can likely handle it.

## What It Does NOT Do

| ❌ Not This | ✅ What It Actually Is |
|-------------|------------------------|
| AI-based classification | Keyword + regex matching. Deterministic, not learned. |
| Guaranteed optimal routing | "Good enough" routing. Test and adjust profiles. |
| Auto-learn from usage | Static keyword lists. Update config manually. |
| Make LLM API calls | Returns recommendation. Your agent calls the API. |
| Perfect accuracy | Simple heuristics. Edge cases will misroute. |

## How to Use

### Standalone CLI

```bash
python3 scripts/smart_router.py "Write a Python function to parse JSON"
```

Output:
```json
{
  "query": "Write a Python function to parse JSON",
  "profile": "coding",
  "model_tier": "default",
  "confidence": 1.0,
  "reasoning": "Profile: coding | Tier: default | default score: 1.00",
  "override": false
}
```

### With Override Flags

```bash
# Force cheap (even for complex queries)
python3 scripts/smart_router.py "Any query" --cheap

# Force powerful (even for simple queries)
python3 scripts/smart_router.py "Any query" --powerful
```

### In Your Agent

```python
from smart_router import SmartRouter

router = SmartRouter()

# Get routing recommendation
result = router.route("Write a marketing email")
# → {"model_tier": "default", "profile": "marketing", ...}

# Use the tier to pick your model
if result["model_tier"] == "cheap":
    model = "anthropic/claude-haiku-4-5"
elif result["model_tier"] == "default":
    model = "anthropic/claude-sonnet-4-6"
else:
    model = "anthropic/claude-opus-4-6"

# Call your LLM API with the selected model
# (This skill does not make API calls — you do)
```

## Profiles

Built-in profiles: `coding`, `research`, `marketing`, `general`

Add custom profiles via JSON config:

```json
{
  "profiles": {
    "my_custom": {
      "description": "My specific workflow",
      "keywords": {
        "cheap": ["quick", "simple"],
        "default": ["standard", "normal"],
        "powerful": ["complex", "advanced"]
      },
      "patterns": {
        "cheap": [r"^quick ", r"^simple "],
        "default": [r"standard"],
        "powerful": [r"complex"]
      }
    }
  }
}
```

```bash
python3 scripts/smart_router.py "query" --config my_profiles.json
```

## Honest Limitations

| Limitation | Truth |
|------------|-------|
| Static keywords | No learning. Update config for new domains. |
| English only | Patterns tuned for English text. |
| No API calls | We tell you which model. You call it. |
| Simple heuristics | Will misroute edge cases. Override flags exist for this. |
| No cost tracking | v1 doesn't log usage. Upgrade for analytics. |

## Free vs Pro

**Free (this skill)**
- 4 built-in profiles
- Custom config support
- Override flags
- Keyword + regex routing

**Pro ($29 one-time)**
- **Dynamic feedback loop** — track which tier actually worked, auto-adjust
- **Usage analytics** — monthly savings report, misroute detection
- **Response quality scoring** — route same query to multiple tiers, pick best
- **Fallback chains** — if cheap fails, auto-try default, then powerful
- **Perplexity-style routing** — "Quick mode" vs "Deep mode" keywords
- **Team profiles** — share routing configs across agents

## Example Savings

Scenario: 100 queries/day

| Without Router | With Router |
|----------------|-------------|
| 100 × Opus @ $15/M = $~150/day | 60 × Haiku @ $0.25/M = $~15/day |
|  | 30 × Sonnet @ $3/M = $~90/day |
|  | 10 × Opus @ $15/M = $~15/day |
|  | **Total: ~$120/day** |
|  | **Savings: ~$30/day (20%)** |

**Note:** These are estimates. Actual savings depend on your query mix.

## Links

- [GitHub](https://github.com/CertainLogicAI/certainlogic-smart-router)
- [ClawHub](https://clawhub.ai/certainlogicai/certainlogic-smart-router)
- [CertainLogic Skills](https://clawhub.ai/certainlogicai)

---

*Built by CertainLogic. Keyword routing. Not AI. Not magic. Just cheaper.*

### Version
latest v1.0.0

### Runtime Requirements
Python 3.10+, zero dependencies
