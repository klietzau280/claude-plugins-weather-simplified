---
description: Get an hour-by-hour forecast for a US zip code — temperature, wind, and precipitation for each hour
---

Use the `get_hourly_forecast` MCP tool from the weather-simplified server to fetch granular hourly data.

Ask the user for a zip code if one wasn't provided. If the user mentions a city or location instead of a zip code, determine the most likely 5-digit US zip code for that area.

The tool accepts:
- `zipCode`: 5-digit US zip code (required)
- `hours`: number of hours to return, 1–156, default 24 (optional)

If the user asks for a specific time range (e.g., "next 6 hours", "tomorrow morning"), adjust the `hours` parameter accordingly.

Present the hourly data in a concise table or summary, focusing on:
- Temperature trends
- Precipitation chances and when rain/snow is most likely
- Wind changes
- Any significant weather shifts
