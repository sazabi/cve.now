# cve.now plugin

Connects an agent to the [cve.now](https://cve.now) MCP server at `https://mcp.cve.now/mcp`. The server is free and needs no account, API key or configuration.

This folder is an [Agent Plugins](https://agent-plugins.org) package: `plugin.json` is the manifest, `mcp.json` declares the server, and `assets/` holds the logo. Cursor loads it through `.cursor-plugin/marketplace.json` at the repository root, and the same folder, zipped, is the ChatGPT plugin package.

## Tools

Two tools that never change: `search` finds an operation (no arguments lists them all) and `execute` runs one by name.

| Operation                  | What it does                                                                                           |
| -------------------------- | ------------------------------------------------------------------------------------------------------ |
| `cve.get`                  | One entry by CVE, GHSA or OSV id: summary, severity, exploitation, affected and fixed versions.        |
| `entities.search`          | Searches the catalog by words or by severity, KEV, exploits, technology, ecosystem, vendor or package. |
| `feed.read`                | The newest entries of a feed: critical, known exploited, one technology or one ecosystem.              |
| `leaderboard.get`          | The cve.now Index: the worst CVEs of a week, month or year, ranked by a 0 to 100 score.                |
| `package.get`              | One package's vulnerability history and the fix status of its latest release.                          |
| `stack.check`              | Checks a lockfile or a list of exact package versions against the catalog.                             |
| `feedback.send`            | Sends a private note to the cve.now team about a wrong or missing entry.                               |
| `<type>.get`, `<type>.list` | One entity or a page of them: cve, early-warning, breach, vendor, package, tech.                      |

## Try it

- "What is CVE-2021-44228 and is it being exploited?"
- "What were the worst CVEs this week?"
- "Check this project's lockfile for known vulnerabilities."

## Support

File an issue in [sazabi/cve.now](https://github.com/sazabi/cve.now/issues) or email [support@sazabi.ai](mailto:support@sazabi.ai).
