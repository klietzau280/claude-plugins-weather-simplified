<div align="center">

<img src="banner.svg" alt="Weather Simplified — MCP Plugin for Claude" width="700" />

</div>

# Weather Simplified — MCP Plugin for Claude

Real-time US weather data from the **National Weather Service (NOAA)** — available as tools for Claude via the [Model Context Protocol](https://modelcontextprotocol.io).

No API key required. No authentication. Just weather.

---

## Install via Claude Code Plugin Marketplace

**Add the marketplace:**
```shell
/plugin marketplace add klietzau280/claude-plugins-weather-simplified
```

**Install the plugins you want:**
```shell
/plugin install weather-forecasts@weather-simplified    # Forecasts & alerts
/plugin install weather-tropical@weather-simplified      # Hurricane tracking
/plugin install weather-severe@weather-simplified        # Tornado watches & SPC outlooks
```

Or browse them all in `/plugin` → **Discover** tab.

---

## Plugins

### weather-forecasts

Current conditions, forecasts, and alerts for any US zip code.

| Skill | Description |
|-------|-------------|
| `/weather-forecasts:current-weather` | Current temperature, wind, humidity, conditions |
| `/weather-forecasts:forecast` | Today & tonight forecast with sunrise/sunset |
| `/weather-forecasts:extended-forecast` | 4-day / 8-period detailed outlook |
| `/weather-forecasts:hourly-forecast` | Hour-by-hour, up to 156 hours |
| `/weather-forecasts:weather-alerts` | Active NWS warnings and advisories |

**MCP Tools:** `get_current_conditions`, `get_forecast`, `get_extended_forecast`, `get_hourly_forecast`, `get_weather_alerts`

---

### weather-tropical

Atlantic and Pacific tropical weather from the National Hurricane Center.

| Skill | Description |
|-------|-------------|
| `/weather-tropical:tropical-weather` | Active storms, formation chances, outlooks, discussions |

**MCP Tools:** `get_tropical_weather`, `get_tropical_atlantic`, `get_tropical_pacific`

---

### weather-severe

Severe weather data from the Storm Prediction Center.

| Skill | Description |
|-------|-------------|
| `/weather-severe:severe-weather` | Watches, convective outlooks, mesoscale discussions |

**MCP Tools:** `get_severe_weather`, `get_watches`, `get_convective_outlooks`, `get_mesoscale_discussions`

---

## Example Prompts

Once installed, just ask Claude naturally:

- **"What's the weather like in Denver?"** → `get_current_conditions`
- **"Will it rain in NYC this week?"** → `get_extended_forecast`
- **"Hourly forecast for the next 12 hours in Miami"** → `get_hourly_forecast`
- **"Any weather warnings near zip code 73301?"** → `get_weather_alerts`
- **"Any tropical storms forming in the Atlantic?"** → `get_tropical_atlantic`
- **"Are there any active tornado watches?"** → `get_watches`

---

## Alternative Setup (Claude Desktop)

### Remote (HTTP, no install)

Add to `claude_desktop_config.json`:

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

### Local (stdio)

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

---

## Submitting to the Anthropic Official Plugin Directory

1. **Submit via the form**: [clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)
2. **Review process**: Anthropic checks quality, security, and MCP server safety
3. **Badge types**: Listed (automated review) or Anthropic Verified (manual review)

---

## Data Sources

All data comes from official **National Weather Service (NWS)** APIs:

- [api.weather.gov](https://api.weather.gov) — Current conditions, forecasts, alerts
- [National Hurricane Center (NHC)](https://www.nhc.noaa.gov) — Tropical weather
- [Storm Prediction Center (SPC)](https://www.spc.noaa.gov) — Severe weather

Free, public, no API key required.

---

## Architecture

```
Claude Code
    │
    ▼
┌────────────────────┐
│ Plugin Skills       │   /current-weather, /forecast, /tropical-weather, ...
└────────┬───────────┘
         │ invokes
         ▼
┌────────────────────┐
│ MCP Server (HTTP)   │   weather-simplified-graphql.azurewebsites.net/mcp
│ 12 tools            │
└────────┬───────────┘
         │
         ▼
┌────────────────────┐
│ NOAA / NWS APIs     │   api.weather.gov · NHC · SPC
└────────────────────┘
```

---

## Privacy

- **No personal data collected** — only accepts 5-digit US ZIP codes
- **No cookies, analytics, or tracking**
- **ZIP codes are not stored or logged**
- Full privacy policy: [weather-simplified-graphql.azurewebsites.net/privacy](https://weather-simplified-graphql.azurewebsites.net/privacy)

---

## Links

- **Source code**: [weather-simplified-graphql](https://github.com/klietzau280/weather-simplified-graphql)
- **Web app**: [Weather Simplified](https://github.com/klietzau280/weather-simplified)
- **Plugin docs**: [code.claude.com/docs/en/plugins](https://code.claude.com/docs/en/plugins)
- **Submit to Anthropic**: [clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)
- **Issues**: [Report a bug](https://github.com/klietzau280/claude-plugins-weather-simplified/issues)

---

## License

MIT
