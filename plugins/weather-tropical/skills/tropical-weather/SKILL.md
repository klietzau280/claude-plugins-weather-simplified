---
name: tropical-weather
description: Get tropical weather information including active storms, hurricanes, formation chances, and NHC outlooks. Use when the user asks about hurricanes, tropical storms, tropical weather, formation chances, or anything related to the Atlantic or Pacific tropics.
---

Use the tropical weather tools based on what the user asks:

- `get_tropical_weather` — all data for both Atlantic and Pacific basins
- `get_tropical_atlantic` — Atlantic basin only (Atlantic Ocean, Gulf of Mexico, Caribbean)
- `get_tropical_pacific` — Eastern Pacific basin only

These tools require no parameters.

If the user doesn't specify a basin, use `get_tropical_weather` for both. If they mention the Atlantic, Gulf, Caribbean, or East Coast, use `get_tropical_atlantic`. For the Pacific or West Coast, use `get_tropical_pacific`.

Present results organized by active storms (name, classification, location, max winds, movement), formation chances (48-hour and 7-day probability), and the latest outlook summary.
