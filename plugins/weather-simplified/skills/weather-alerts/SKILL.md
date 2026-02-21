---
description: Check active weather alerts and warnings for a US zip code — severe weather, flood watches, heat advisories, etc.
---

Use the `get_weather_alerts` MCP tool from the weather-simplified server to check for active NWS alerts.

Ask the user for a zip code if one wasn't provided. If the user mentions a city or location instead of a zip code, determine the most likely 5-digit US zip code for that area.

Call `get_weather_alerts` with the zip code. If alerts are active, present each one with:
- Event type and severity
- Headline
- Key details from the description
- When it expires

If no alerts are active, let the user know there are currently no weather warnings for that area.
