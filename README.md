# cve.now

**A free, public vulnerability feed.** [cve.now](https://cve.now) merges the CVE List, the GitHub Advisory Database, OSV, CISA's Known Exploited Vulnerabilities catalog (KEV) and FIRST EPSS scores into one deduplicated entry per vulnerability, and publishes it as RSS, Atom, JSON Feed, a JSON API and an MCP server. No account, no API key.

This repository is cve.now's home on GitHub: what it is, how to use it, and where to report problems. The service is built and run by [Sazabi](https://sazabi.com?utm_source=cve-now&utm_medium=github); its source code is not public.

## Feeds

One endpoint, `https://cve.now/feed`, narrowed with filters that combine freely. RSS by default; add `format=atom` or `format=json`.

| Feed | URL |
|---|---|
| Critical: in CISA KEV, CVSS 9+ in a listed technology, or CVSS 7+ with an EPSS score of 0.1 or more | `https://cve.now/feed?filter=critical` |
| New CISA Known Exploited Vulnerabilities | `https://cve.now/feed?filter=kev` |
| Every entry | `https://cve.now/feed` |
| One technology | `https://cve.now/feed?tech=nextjs` |
| One package ecosystem | `https://cve.now/feed?ecosystem=npm` |
| Combined | `https://cve.now/feed?filter=critical&tech=nextjs&format=json` |

Ecosystems: `npm`, `pypi`, `go`, `maven`, `crates.io`, `packagist`, `rubygems`, `nuget`.

Technologies: `nextjs`, `react`, `node`, `express`, `django`, `flask`, `rails`, `spring`, `log4j`, `kubernetes`, `docker`, `nginx`, `apache-httpd`, `openssl`, `postgresql`, `mysql`, `redis`, `php`, `wordpress`, `jenkins`, `gitlab`, `fortinet`, `citrix`, `ivanti`, `cisco-ios`, `palo-alto-panos`, `vmware`, `microsoft-exchange`, `chrome`, `linux-kernel`. Missing one? [Request it](https://github.com/sazabi/cve.now/issues/new?template=technology-request.yml).

In Slack, run `/feed subscribe https://cve.now/feed?filter=critical` in any channel.

## Check your stack

Upload a lockfile (up to 5 MB) at [cve.now](https://cve.now) to get a shareable report and an RSS feed of only the entries that affect your exact package versions. Supported: `package-lock.json`, `bun.lock`, `pnpm-lock.yaml`, `yarn.lock`, `requirements.txt`, `poetry.lock`, `Cargo.lock`, `go.sum`, `Gemfile.lock`.

For a short package list, build the feed URL yourself:

```
https://cve.now/stack?p=npm:lodash@4.17.20,pypi:django@4.2.0
```

## MCP server

A remote Streamable HTTP MCP server at `https://mcp.cve.now/mcp`, no authentication. Tools: `get_vulnerability`, `list_feed` and `check_stack`.

**Claude Code**

```sh
claude mcp add --transport http cve-now https://mcp.cve.now/mcp
```

**Codex**

```sh
codex mcp add cve-now --url https://mcp.cve.now/mcp
```

**Cursor** (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "cve-now": { "url": "https://mcp.cve.now/mcp" }
  }
}
```

Then ask your agent to run `check_stack` on your project's lockfile.

## API

| Endpoint | Returns |
|---|---|
| `https://cve.now/<id>` | Page for a CVE, GHSA or OSV id |
| `https://cve.now/api/v1/entries/<id>` | The same entry as JSON |
| `https://cve.now/api/v1/entries` | All published entries, newest first, paginated with `nextCursor` |
| `https://cve.now/api/v1/status` | Source polling health and catalog coverage |
| `https://cve.now/llms.txt` | A plain-text guide for LLMs and agents |

`/feed` and `/api/v1/*` send `Access-Control-Allow-Origin: *`.

## Issues

[Open an issue](https://github.com/sazabi/cve.now/issues/new/choose) to report:

- a wrong or missing entry
- two entries that should be merged, or one that merged things it shouldn't
- a technology or package ecosystem you want covered
- a disclosure source we should watch
- a bug in a feed, page, the API or the MCP server

For an error in an upstream record (for example a wrong CVE description), we'll point you to the CNA or advisory database that owns it.

**Don't post unpatched vulnerabilities here.** Issues are public. Report a vulnerability in someone else's product to its vendor. Report a vulnerability in cve.now itself to [security@sazabi.ai](mailto:security@sazabi.ai) (see [SECURITY.md](SECURITY.md)).

This repository doesn't accept pull requests: its files are synced from Sazabi's private monorepo, so a direct change would be overwritten. Open an issue instead.

## Sources and licensing

Data: the [CVE List](https://www.cve.org), the [GitHub Advisory Database](https://github.com/advisories), [OSV](https://osv.dev), the [CISA KEV catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) and [FIRST EPSS](https://www.first.org/epss/). Each entry links to its sources.

Entry summaries are written by a model and labeled as such; they're published under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). Upstream data keeps its own license and attribution.

This product uses data from the NVD API but is not endorsed or certified by the NVD.

The text in this repository is licensed under [Apache 2.0](LICENSE).

---

Want to know which of these affect your systems? [Sazabi can tell you](https://sazabi.com?utm_source=cve-now&utm_medium=github).
