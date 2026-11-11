# cve.now plugin

Connects an agent to the [cve.now](https://cve.now) MCP server at `https://mcp.cve.now/mcp`. The server is free and needs no account, API key or configuration.

This folder is an [Agent Plugins](https://agent-plugins.org) package: `plugin.json` is the manifest, `mcp.json` declares the server, and `assets/` holds the logo. Cursor loads it through `.cursor-plugin/marketplace.json` at the repository root, and the same folder, zipped, is the ChatGPT plugin package.

## Tools

| Tool                | What it does                                                                                       |
| ------------------- | -------------------------------------------------------------------------------------------------- |
| `get_vulnerability` | One entry by CVE, GHSA or OSV id: summary, severity, exploitation, affected and fixed versions.     |
| `search`            | Searches the catalog by words or by severity, KEV, exploits, technology, ecosystem, vendor or package. |
| `list_feed`         | The newest entries of a feed: critical, known exploited, one technology or one ecosystem.          |
| `get_leaderboard`   | The cve.now Index: the worst CVEs of a week, month or year, ranked by a 0 to 100 score.            |
| `get_package`       | One package's vulnerability history and the fix status of its latest release.                      |
| `check_stack`       | Checks a lockfile or a list of exact package versions against the catalog.                         |
| `send_feedback`     | Sends a private note to the cve.now team about a wrong or missing entry.                           |

## Try it

- "What is CVE-2021-44228 and is it being exploited?"
- "What were the worst CVEs this week?"
- "Check this project's lockfile for known vulnerabilities."

## Support

File an issue in [sazabi/cve.now](https://github.com/sazabi/cve.now/issues) or email [support@sazabi.ai](mailto:support@sazabi.ai).
