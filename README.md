# Weather Simplified — MCP Plugin for Claude

```
       ☀                  ___
      -+-              __(   )__
      / \           .-(         )-.
                   (    ☁    ☁     )
                    '-(       )-'
                      | | | | |
                      ' ' ' ' '

                  .~~~~~~~~~~~~~.
                .~~~~~~~~~~~~~~~~~.
              .~~~~~~~~~~~~~~~~~~~~~.
            .~~~~~~~~~~~~~~~~~~~~~~~~~.

              W e a t h e r
           S I M P L I F I E D

         ~~~ MCP Plugin for Claude ~~~
```

Real-time US weather data from the **National Weather Service (NOAA)** — available as tools for Claude via the [Model Context Protocol](https://modelcontextprotocol.io).

No API key required. No authentication. Just weather.

---

## Tools (12)

### Location-Based (by ZIP code)

| Tool | Parameters | What it returns |
|------|-----------|-----------------|
| `get_current_conditions` | `zipCode` | Temperature, wind speed/direction, humidity, dew point, heat index, text description |
| `get_forecast` | `zipCode` | Today & tonight forecast periods, precipitation chance, sunrise/sunset |
| `get_extended_forecast` | `zipCode` | 4-day / 8-period forecast with day & night detail |
| `get_hourly_forecast` | `zipCode`, `hours` | Hour-by-hour forecast (default 24h, max 156h) with temp, wind, precip, humidity |
| `get_weather_alerts` | `zipCode` | Active NWS alerts — severity, event type, headline, description, affected areas |

### Tropical Weather (no parameters)

| Tool | What it returns |
|------|-----------------|
| `get_tropical_weather` | Both Atlantic & Pacific basins — active storms, advisories, outlooks, formation chances |
| `get_tropical_atlantic` | Atlantic basin only — storms, advisories, outlook, formation chances, discussion |
| `get_tropical_pacific` | Eastern Pacific basin only — storms, advisories, outlook, formation chances, discussion |

### Severe Weather (no parameters)

| Tool | What it returns |
|------|-----------------|
| `get_severe_weather` | Combined overview — all watches, outlooks, and mesoscale discussions |
| `get_watches` | Active tornado & severe thunderstorm watches from the Storm Prediction Center |
| `get_convective_outlooks` | SPC Day 1–8 categorical, tornado, wind, and hail risk maps |
| `get_mesoscale_discussions` | SPC real-time severe weather analysis and short-term forecasts |

---

## Setup

### Option 1: Remote (HTTP) — No install required

The MCP server is deployed and accessible over HTTP. Add this to your Claude Desktop config:

**`claude_desktop_config.json`**
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

### Option 2: Local (stdio)

Clone the main repository and run the MCP server locally:

```bash
git clone https://github.com/klietzau280/weather-simplified-graphql.git
cd weather-simplified-graphql
npm install
cp .env.example .env   # add your NOAA config
npm run build:mcp
```

Then add to your Claude Desktop config:

**`claude_desktop_config.json`**
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

### Option 3: Local dev (no build step)

```bash
cd weather-simplified-graphql
npm run dev:mcp
```

```json
{
  "mcpServers": {
    "weather": {
      "command": "npx",
      "args": ["tsx", "/absolute/path/to/weather-simplified-graphql/src/mcp/server.ts"]
    }
  }
}
```

---

## Example Prompts

Once connected, try asking Claude:

- **"What's the weather like in Denver right now?"** — calls `get_current_conditions`
- **"Will it rain in NYC this week?"** — calls `get_extended_forecast`
- **"Give me the hourly forecast for the next 12 hours in Miami"** — calls `get_hourly_forecast`
- **"Are there any weather warnings near zip code 73301?"** — calls `get_weather_alerts`
- **"Any tropical storms forming in the Atlantic?"** — calls `get_tropical_atlantic`
- **"What does the severe weather outlook look like today?"** — calls `get_severe_weather`
- **"Are there any active tornado watches?"** — calls `get_watches`

---

## Data Sources

All weather data comes from official **National Weather Service (NWS)** APIs:

- [api.weather.gov](https://api.weather.gov) — Current conditions, forecasts, alerts
- [National Hurricane Center (NHC)](https://www.nhc.noaa.gov) — Tropical weather products
- [Storm Prediction Center (SPC)](https://www.spc.noaa.gov) — Severe weather watches, outlooks, mesoscale discussions

Data is free, public, and requires no API key.

---

## Architecture

```
Claude Desktop / claude.ai
        │
        ▼
┌─────────────────────┐
│  MCP Server          │
│  (stdio or HTTP)     │
│                      │
│  12 tools registered │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Weather Services    │
│                      │
│  • CurrentConditions │
│  • ForecastDay       │
│  • ForecastExtended  │
│  • HourlyForecast    │
│  • WeatherAlerts     │
│  • TropicalV2        │
│  • SevereWeather     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  NOAA / NWS APIs     │
│  (api.weather.gov)   │
└─────────────────────┘
```

---

## Privacy

- **No personal data collected** — the only input is a 5-digit US ZIP code
- **No cookies, analytics, or tracking**
- **ZIP codes are not stored or logged**
- Weather data may be cached temporarily for performance
- Full privacy policy: [weather-simplified-graphql.azurewebsites.net/privacy](https://weather-simplified-graphql.azurewebsites.net/privacy)

---

## Links

- **Source code**: [weather-simplified-graphql](https://github.com/klietzau280/weather-simplified-graphql)
- **Web app**: [Weather Simplified](https://github.com/klietzau280/weather-simplified)
- **Issues**: [Report a bug](https://github.com/klietzau280/claude-plugins-weather-simplified/issues)
- **MCP Protocol**: [modelcontextprotocol.io](https://modelcontextprotocol.io)

---

## License

MIT
