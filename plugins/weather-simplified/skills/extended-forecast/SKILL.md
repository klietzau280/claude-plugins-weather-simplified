---
description: Get a 4-day extended forecast for a US zip code — 8 periods covering day and night
---

Use the `get_extended_forecast` MCP tool from the weather-simplified server to fetch a multi-day outlook.

Ask the user for a zip code if one wasn't provided. If the user mentions a city or location instead of a zip code, determine the most likely 5-digit US zip code for that area.

Call `get_extended_forecast` with the zip code and present the 8 forecast periods in a readable format, highlighting:
- Each period name (e.g., "Tuesday", "Tuesday Night")
- Temperature and precipitation chance
- Wind speed and direction
- Short forecast summary for each period
