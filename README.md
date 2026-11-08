# How to connect GlossGenius to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your GlossGenius account.** GlossGenius has no official app in the ChatGPT or Claude directories. Cotlet.dev connects your own signed-in GlossGenius account to any AI agent, so you can ask in plain words and the AI books, reschedules and follows up with clients for you.

## What you can ask

> Book Maria Lopez for a gel manicure on Thursday at 11 am and send her the confirmation.

> Who cancelled this week? Offer their open slots to clients who asked for an earlier time.

> Move all of my Saturday afternoon appointments to Sunday and let each client know.

> Which clients haven't come back in 60 days? List them with their last service and visit date.

> Show me tomorrow's schedule and any gaps longer than 45 minutes.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its GlossGenius tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"glossgenius":{"command":"uvx","args":["glossgenius-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t glossgenius-mcp .
docker run -i --rm -e COTLET_API_KEY glossgenius-mcp
```

Tools: `glossgenius_guide`, `glossgenius_status`, `glossgenius_open`, `glossgenius_read`, `glossgenius_click`, `glossgenius_type`, `glossgenius_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install glossgenius-mcp        # or run it once: uvx glossgenius-mcp connect
glossgenius-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 glossgenius_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 glossgenius_agent.py status    # is GlossGenius ready in your Cotlet.dev account
python3 glossgenius_agent.py guide     # GlossGenius screens and sign-in link
python3 glossgenius_agent.py read      # open GlossGenius, read the page, close the browser
python3 glossgenius_agent.py tools     # list Cotlet.dev tools
python3 glossgenius_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from GlossGenius users

**Does GlossGenius have an API?**

You don't need a GlossGenius API to automate your account. Cotlet.dev works in your own signed-in GlossGenius account directly, so your AI agent can book, reschedule and follow up with clients without an API key.

**How do I connect GlossGenius to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to GlossGenius once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no GlossGenius API key.

**Is there a way to use Claude with GlossGenius?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own GlossGenius account.

**Is there a GlossGenius MCP server?**

We found no official GlossGenius app in ChatGPT's directory or connector in Claude's directory. Cotlet.dev is a hosted MCP server that works in GlossGenius for you, 24/7, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

## Find it on

- [GlossGenius on Cotlet.dev](https://cotlet.dev/integrations/glossgenius-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=glossgenius&utm_content=find)
- [PyPI package glossgenius-mcp](https://pypi.org/project/glossgenius-mcp/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-glossgenius-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/glossgenius-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=glossgenius

Start free: https://cotlet.dev/signup?app=glossgenius&utm_source=github&utm_medium=readme&utm_campaign=glossgenius
