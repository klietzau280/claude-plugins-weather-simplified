---
description: Get today's weather forecast for a US zip code — day and night periods with sunrise and sunset times
---

Use the `get_forecast` MCP tool from the weather-simplified server to fetch today's forecast.

Ask the user for a zip code if one wasn't provided. If the user mentions a city or location instead of a zip code, determine the most likely 5-digit US zip code for that area.

Call `get_forecast` with the zip code and present the results clearly:
- Day period: temperature, wind, precipitation chance, detailed forecast
- Night period: temperature, wind, precipitation chance, detailed forecast
- Sunrise and sunset times
