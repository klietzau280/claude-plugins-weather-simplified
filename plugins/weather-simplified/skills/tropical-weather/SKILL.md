---
description: Get tropical weather information — active storms, hurricane advisories, formation chances for Atlantic and Pacific basins
---

Use the tropical weather MCP tools from the weather-simplified server. Choose the right tool based on what the user asks:

- `get_tropical_weather` — all data for both Atlantic and Pacific basins
- `get_tropical_atlantic` — Atlantic basin only (Atlantic Ocean, Gulf of Mexico, Caribbean)
- `get_tropical_pacific` — Eastern Pacific basin only

These tools require no parameters.

If the user doesn't specify a basin, use `get_tropical_weather` to get both. If they mention the Atlantic, Gulf, Caribbean, or East Coast, use `get_tropical_atlantic`. If they mention the Pacific or West Coast, use `get_tropical_pacific`.

Present the results organized by:
- Active storms (name, classification, location, max winds, movement)
- Formation chances (location, 48-hour and 7-day probability)
- Latest outlook summary
- Latest discussion synopsis if available
