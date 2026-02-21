---
description: Get current weather conditions for a US zip code — temperature, wind, humidity, and description
---

Use the `get_current_conditions` MCP tool from the weather-simplified server to fetch real-time weather conditions.

Ask the user for a zip code if one wasn't provided. If the user mentions a city or location instead of a zip code, determine the most likely 5-digit US zip code for that area.

Call `get_current_conditions` with the zip code and present the results in a clear, conversational format including:
- Temperature
- Wind speed and direction
- Humidity
- Text description of conditions
- The observing station location (city, state)
