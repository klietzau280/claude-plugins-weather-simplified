---
name: hourly-forecast
description: Get an hour-by-hour forecast for a US location. Use when the user asks about specific hours, "when will it rain", "hourly forecast", or needs granular time-based weather data.
---

Fetch hourly forecast data using the get_hourly_forecast tool.

Parameters:
- zipCode — 5-digit US zip code (required)
- hours — number of hours to return, 1-156, default 24 (optional)

If the user asks for a specific time range (e.g., "next 6 hours"), adjust the hours parameter accordingly. If they provide a city name, determine the most likely zip code.

Focus on temperature trends, when precipitation is most likely, wind changes, and any significant weather shifts.
