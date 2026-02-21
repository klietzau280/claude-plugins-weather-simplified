<div align="center">

<img src="banner.svg" alt="Weather Simplified — MCP Plugin for Claude" width="700" />

</div>

# Weather Simplified

Real-time US weather data from the **National Weather Service (NOAA)** — current conditions, forecasts, alerts, tropical weather, and severe weather — available as tools for Claude via the [Model Context Protocol](https://modelcontextprotocol.io).

## Installation

Add the marketplace, then install the plugins you need:

```shell
/plugin marketplace add klietzau280/claude-plugins-weather-simplified
```

```shell
/plugin install weather-forecasts@weather-simplified    # Forecasts & alerts
/plugin install weather-tropical@weather-simplified      # Hurricane tracking
/plugin install weather-severe@weather-simplified        # Tornado watches & SPC outlooks
```

Or browse all three in `/plugin` > **Discover**.

## What It Does

Three plugins, each focused on a different domain of weather data. Install one, two, or all three.

### weather-forecasts

Current conditions, forecasts, and alerts for any US ZIP code.

| Skill | Tool | Description |
|-------|------|-------------|
| `/current-weather` | `get_current_conditions` | Temperature, wind, humidity, conditions |
| `/forecast` | `get_forecast` | Today & tonight forecast with sunrise/sunset |
| `/extended-forecast` | `get_extended_forecast` | 4-day / 8-period detailed outlook |
| `/hourly-forecast` | `get_hourly_forecast` | Hour-by-hour forecast, up to 156 hours |
| `/weather-alerts` | `get_weather_alerts` | Active NWS warnings and advisories |

### weather-tropical

Atlantic and Pacific tropical weather from the National Hurricane Center.

| Skill | Tool | Description |
|-------|------|-------------|
| `/tropical-weather` | `get_tropical_weather` | All tropical data combined |
| | `get_tropical_atlantic` | Atlantic basin storms, formation chances, outlooks |
| | `get_tropical_pacific` | Eastern Pacific basin storms, formation chances, outlooks |

### weather-severe

Severe weather data from the Storm Prediction Center.

| Skill | Tool | Description |
|-------|------|-------------|
| `/severe-weather` | `get_severe_weather` | All severe data combined |
| | `get_watches` | Active tornado and severe thunderstorm watches |
| | `get_convective_outlooks` | SPC Day 1-8 categorical risk outlooks |
| | `get_mesoscale_discussions` | Real-time SPC severe weather analysis |

## Example Prompts

Ask Claude naturally — it will pick the right tool:

- **"What's the weather like in Denver?"** — current conditions
- **"Will it rain in NYC this week?"** — extended forecast
- **"Hourly forecast for the next 12 hours in Miami"** — hourly forecast
- **"Any weather warnings near zip code 73301?"** — weather alerts
- **"Any tropical storms forming in the Atlantic?"** — tropical weather
- **"Are there any active tornado watches?"** — severe weather

## Requirements

- **Claude Code** with plugin support
- US locations only (5-digit ZIP codes)
- No API key, no authentication, no account required

## Data Sources

All data is sourced from official US government APIs:

- [api.weather.gov](https://api.weather.gov) — Current conditions, forecasts, alerts
- [National Hurricane Center](https://www.nhc.noaa.gov) — Tropical weather
- [Storm Prediction Center](https://www.spc.noaa.gov) — Severe weather

## Architecture

```
Claude Code
    |
    v
+--------------------+
| Plugin Skills      |   /current-weather, /forecast, /tropical-weather, ...
+--------+-----------+
         | MCP tool call
         v
+--------------------+
| MCP Server (HTTP)  |   weather-simplified-graphql.azurewebsites.net/mcp
| 12 tools           |
+--------+-----------+
         |
         v
+--------------------+
| NOAA / NWS APIs    |   api.weather.gov, NHC, SPC
+--------------------+
```

## Alternative Setup (Claude Desktop)

You can also use the MCP server directly without the plugin marketplace.

**Remote (no install)** — add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "weather": {
      "type": "streamable-http",
      "url": "https://weather-simplified-graphql.azurewebsites.net/mcp"
    }
  }
}
```

**Local (stdio):**

```bash
git clone https://github.com/klietzau280/weather-simplified-graphql.git
cd weather-simplified-graphql
npm install && npm run build:mcp
```

```json
{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": ["/absolute/path/to/weather-simplified-graphql/dist-mcp/src/mcp/server.js"]
    }
  }
}
```

## Privacy

- **No personal data collected** — only accepts 5-digit US ZIP codes
- **No cookies, analytics, or tracking**
- **ZIP codes are not stored or logged**
- Full policy: [weather-simplified-graphql.azurewebsites.net/privacy](https://weather-simplified-graphql.azurewebsites.net/privacy)

## License

MIT

## Author

Weather Simplified — [github.com/klietzau280](https://github.com/klietzau280)

Source: [weather-simplified-graphql](https://github.com/klietzau280/weather-simplified-graphql) | Issues: [Report a bug](https://github.com/klietzau280/claude-plugins-weather-simplified/issues)
