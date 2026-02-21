---
name: extended-forecast
description: Get a multi-day extended forecast for a US location. Use when the user asks about the week ahead, multi-day forecast, "what's the weather this week", or planning weather for upcoming days.
---

Fetch the 4-day extended forecast using the get_extended_forecast tool. This returns 8 periods covering day and night.

If the user provides a city name instead of a zip code, determine the most likely 5-digit US zip code for that area.

Present each period with its name (e.g., "Wednesday", "Wednesday Night"), temperature, precipitation chance, wind, and a short forecast summary.
