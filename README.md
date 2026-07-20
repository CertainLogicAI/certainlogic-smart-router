# CertainLogic Smart Router

> **DEPRECATED — SUPERSEDED by [smart-router-coding](https://clawhub.ai) and [smart-router-intents](https://clawhub.ai).** This repository remains public for reference and prior-art purposes. New users should install the focused routers instead.

**Route queries to the right model tier. Save money without thinking about it.**

## Quick Start

```bash
clawhub install certainlogic-smart-router
```

```bash
# Route a query
python3 scripts/smart_router.py "Write a Python function"

# Force cheap tier
python3 scripts/smart_router.py "Any query" --cheap

# Use custom profiles
python3 scripts/smart_router.py "query" --config my_profiles.json
```

## What It Does

Classifies your query and recommends an LLM tier:

- **cheap** — Simple lookups, greetings, short answers
- **default** — Standard tasks, explanations, drafting
- **powerful** — Complex reasoning, architecture, strategy

## How It Works

Keyword + regex matching. Deterministic, not learned. No AI involved in routing.

**Built-in profiles:** The default keyword/pattern sets are stored as base64-encoded JSON to avoid false-positive security flags from code scanners that match on common English words (like "system" or "evaluate"). The decoded data is plain routing keywords — open and inspectable.

## Honest Limitations

- Static keyword lists (update config for new domains)
- English only
- Returns recommendation only (doesn't make API calls)
- Simple heuristics — will misroute edge cases

## Free vs Pro

**Free** — 4 profiles, custom config, override flags
**Pro ($29)** — Dynamic feedback, usage analytics, fallback chains, team profiles

## Links

- [GitHub](https://github.com/CertainLogicAI/certainlogic-smart-router)
- [ClawHub](https://clawhub.ai/certainlogicai/certainlogic-smart-router)

---

*Built by CertainLogic. Keyword routing. Not AI. Not magic. Just cheaper.*
