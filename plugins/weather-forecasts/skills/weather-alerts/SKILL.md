---
name: weather-alerts
description: Check active weather alerts and warnings for a US location. Use when the user asks about warnings, watches, advisories, "any weather alerts", or severe weather for a specific area.
---

Fetch active NWS alerts using the `get_weather_alerts` tool.

If the user provides a city name instead of a zip code, determine the most likely 5-digit US zip code for that area.

If alerts are active, present each one with event type, severity, headline, key details, and expiration time. If no alerts are active, let the user know the area is clear.
