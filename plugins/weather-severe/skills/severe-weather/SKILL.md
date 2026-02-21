---
name: severe-weather
description: Get severe weather information including tornado watches, thunderstorm watches, SPC convective outlooks, and mesoscale discussions. Use when the user asks about severe weather, tornado watches, storm risk, SPC outlooks, or convective activity.
---

Use the severe weather tools based on what the user asks:

- `get_severe_weather` — combined overview of all severe weather data
- `get_watches` — active tornado and severe thunderstorm watches only
- `get_convective_outlooks` — SPC Day 1–8 risk outlooks (categorical, tornado, wind, hail)
- `get_mesoscale_discussions` — real-time SPC severe weather analysis

These tools require no parameters.

For general severe weather questions, use `get_severe_weather` for the full picture. For specific questions like "any tornado watches?" use `get_watches`, or "what's the risk today?" use `get_convective_outlooks`.

Present active watches with type, areas affected, expiration, and threats. Present outlooks with risk level by day and threat types. Present discussions with headline, affected area, and key takeaways.
