---
description: Get severe weather information — tornado and thunderstorm watches, SPC convective outlooks, and mesoscale discussions
---

Use the severe weather MCP tools from the weather-simplified server. Choose the right tool based on what the user asks:

- `get_severe_weather` — combined overview of all severe weather data
- `get_watches` — active tornado and severe thunderstorm watches only
- `get_convective_outlooks` — SPC Day 1–8 risk outlooks (categorical, tornado, wind, hail)
- `get_mesoscale_discussions` — real-time SPC severe weather analysis

These tools require no parameters.

If the user asks a general severe weather question, use `get_severe_weather` to get the full picture. For specific questions:
- "Any tornado watches?" → `get_watches`
- "What's the severe risk today?" → `get_convective_outlooks`
- "Any mesoscale discussions?" → `get_mesoscale_discussions`

Present the results clearly:
- Active watches: type, areas affected, expiration, threats
- Outlooks: risk level by day, threat types
- Discussions: headline, affected area, key takeaways
