<div align="center">

<img src="banner.svg" alt="Weather Simplified — MCP Plugin for Claude" width="700" />

</div>

# Weather Simplified — MCP Plugin for Claude

Real-time US weather data from the **National Weather Service (NOAA)** — available as tools for Claude via the [Model Context Protocol](https://modelcontextprotocol.io).

No API key required. No authentication. Just weather.

---

## Install via Claude Code Plugin Marketplace

### One-line install

```shell
/plugin marketplace add klietzau280/claude-plugins-weather-simplified
/plugin install weather-simplified@weather-simplified
```

### Step by step

1. **Add the marketplace** — In Claude Code, run:
   ```shell
   /plugin marketplace add klietzau280/claude-plugins-weather-simplified
   ```

2. **Browse available plugins** — Run `/plugin` and go to the **Discover** tab to see the Weather Simplified plugin.

3. **Install the plugin** — Select it and choose your scope:
   - **User scope**: available across all your projects (default)
   - **Project scope**: shared with collaborators via `.claude/settings.json`
   - **Local scope**: just for you in this repo

4. **Start using it** — The 7 skills and 12 MCP tools are immediately available:
   ```shell
   /weather-simplified:current-weather
   /weather-simplified:forecast
   /weather-simplified:severe-weather
   ```

   Or just ask Claude naturally — it will use the tools automatically:
   > "What's the weather like in Denver?"

---

## What's Included

### 7 Skills (slash commands)

| Skill | Command | Description |
|-------|---------|-------------|
| Current Weather | `/weather-simplified:current-weather` | Current conditions for any US zip code |
| Forecast | `/weather-simplified:forecast` | Today & tonight forecast with sunrise/sunset |
| Extended Forecast | `/weather-simplified:extended-forecast` | 4-day / 8-period detailed outlook |
| Hourly Forecast | `/weather-simplified:hourly-forecast` | Hour-by-hour forecast, up to 156 hours |
| Weather Alerts | `/weather-simplified:weather-alerts` | Active NWS warnings and advisories |
| Tropical Weather | `/weather-simplified:tropical-weather` | Atlantic & Pacific storms, formation chances |
| Severe Weather | `/weather-simplified:severe-weather` | Watches, outlooks, mesoscale discussions |

### 12 MCP Tools

Skills invoke these tools automatically, but Claude can also call them directly:

**Location-based (by ZIP code)**

| Tool | Parameters | Returns |
|------|-----------|---------|
| `get_current_conditions` | `zipCode` | Temperature, wind, humidity, dew point, heat index, description |
| `get_forecast` | `zipCode` | Day & night periods, precipitation chance, sunrise/sunset |
| `get_extended_forecast` | `zipCode` | 4-day / 8-period forecast with day & night detail |
| `get_hourly_forecast` | `zipCode`, `hours` | Hour-by-hour (default 24h, max 156h) temp, wind, precip, humidity |
| `get_weather_alerts` | `zipCode` | Active NWS alerts — severity, event type, headline, description |

**Tropical weather (no parameters)**

| Tool | Returns |
|------|---------|
| `get_tropical_weather` | Both basins — active storms, advisories, outlooks, formation chances |
| `get_tropical_atlantic` | Atlantic basin — storms, advisories, outlook, formation chances |
| `get_tropical_pacific` | Eastern Pacific — storms, advisories, outlook, formation chances |

**Severe weather (no parameters)**

| Tool | Returns |
|------|---------|
| `get_severe_weather` | Combined watches, outlooks, and mesoscale discussions |
| `get_watches` | Active tornado & severe thunderstorm watches |
| `get_convective_outlooks` | SPC Day 1–8 categorical, tornado, wind, hail risk |
| `get_mesoscale_discussions` | SPC real-time severe weather analysis |

---

## Alternative Setup (without plugin marketplace)

### Claude Desktop — Remote (HTTP, no install)

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

### Claude Desktop — Local (stdio)

```bash
git clone https://github.com/klietzau280/weather-simplified-graphql.git
cd weather-simplified-graphql
npm install
npm run build:mcp
```

Add to `claude_desktop_config.json`:

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

Want this plugin in the official `/plugin` Discover tab? Here's the process:

1. **Submit via the form**: [clau.de/plugin-directory-submission](https://clau.de/plugin-directory-submission)

2. **What Anthropic reviews**:
   - Plugin quality and functionality
   - Security (no credentials, no data exfiltration)
   - MCP server safety (`readOnlyHint: true`, `destructiveHint: false`)
   - Clear descriptions and documentation

3. **Badge types**:
   - **Listed**: basic automated review, appears in the directory
   - **Anthropic Verified**: additional manual review for quality and safety

4. **Our plugin meets the requirements**:
   - All tools are read-only (no destructive operations)
   - No authentication or API keys required
   - No personal data collected
   - Public NOAA data source
   - MIT licensed
   - Clear tool descriptions with parameter validation

---

## Hosting Your Own Marketplace

If you want to fork this and create your own weather plugin marketplace:

### Repository Structure

```
your-repo/
├── .claude-plugin/
│   └── marketplace.json        # Marketplace catalog
├── plugins/
│   └── weather-simplified/
│       ├── .claude-plugin/
│       │   └── plugin.json     # Plugin manifest
│       ├── .mcp.json           # MCP server config (remote HTTP)
│       └── skills/
│           ├── current-weather/
│           │   └── SKILL.md
│           ├── forecast/
│           │   └── SKILL.md
│           ├── extended-forecast/
│           │   └── SKILL.md
│           ├── hourly-forecast/
│           │   └── SKILL.md
│           ├── weather-alerts/
│           │   └── SKILL.md
│           ├── tropical-weather/
│           │   └── SKILL.md
│           └── severe-weather/
│               └── SKILL.md
├── LICENSE
└── README.md
```

### Key Files

**`.claude-plugin/marketplace.json`** — defines the marketplace catalog:
```json
{
  "name": "weather-simplified",
  "owner": { "name": "Weather Simplified" },
  "plugins": [
    {
      "name": "weather-simplified",
      "source": "./plugins/weather-simplified",
      "description": "12 weather tools powered by NOAA",
      "version": "1.1.0",
      "category": "external-integrations",
      "keywords": ["weather", "forecast", "noaa"]
    }
  ]
}
```

**`plugins/weather-simplified/.mcp.json`** — connects to the remote MCP server:
```json
{
  "mcpServers": {
    "weather-simplified": {
      "type": "streamable-http",
      "url": "https://weather-simplified-graphql.azurewebsites.net/mcp"
    }
  }
}
```

**`plugins/weather-simplified/skills/*/SKILL.md`** — each skill tells Claude how to use the MCP tools for that weather domain.

### Team Configuration

Add to your project's `.claude/settings.json` to auto-suggest the marketplace:

```json
{
  "extraKnownMarketplaces": {
    "weather-simplified": {
      "source": {
        "source": "github",
        "repo": "klietzau280/claude-plugins-weather-simplified"
      }
    }
  },
  "enabledPlugins": {
    "weather-simplified@weather-simplified": true
  }
}
```

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
Claude Code / Claude Desktop
        │
        ▼
┌─────────────────────────┐
│  Plugin: Skills (7)      │
│  /current-weather        │
│  /forecast               │
│  /tropical-weather  ...  │
└──────────┬──────────────┘
           │ invokes
           ▼
┌─────────────────────────┐
│  MCP Server (12 tools)   │
│  stdio or HTTP transport │
└──────────┬──────────────┘
           │
           ▼
┌─────────────────────────┐
│  NOAA / NWS APIs         │
│  api.weather.gov         │
│  NHC · SPC               │
└─────────────────────────┘
```

---

## Privacy

- **No personal data collected** — only accepts 5-digit US ZIP codes
- **No cookies, analytics, or tracking**
- **ZIP codes are not stored or logged**
- Weather data may be cached temporarily for performance
- Full privacy policy: [weather-simplified-graphql.azurewebsites.net/privacy](https://weather-simplified-graphql.azurewebsites.net/privacy)

---

## Links

- **Source code**: [weather-simplified-graphql](https://github.com/klietzau280/weather-simplified-graphql)
- **Web app**: [Weather Simplified](https://github.com/klietzau280/weather-simplified)
- **Plugin docs**: [Claude Code Plugins](https://code.claude.com/docs/en/plugins)
- **Marketplace docs**: [Plugin Marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- **Submit to Anthropic**: [Plugin Directory Submission](https://clau.de/plugin-directory-submission)
- **Issues**: [Report a bug](https://github.com/klietzau280/claude-plugins-weather-simplified/issues)

---

## License

MIT
