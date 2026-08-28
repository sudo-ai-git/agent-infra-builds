# 💼 Agent-Infra Custom Builds — engagement intake

I build **production MCP servers** and **agent verification layers** at fixed
price, milestone-billed. Public, MIT, E2E-tested reference assets:

| asset | what it does | one-command install |
|---|---|---|
| [`mcp-skill-sec`](https://github.com/sudo-ai-git/mcp-skill-sec) | audit skills/prompts vs 8 supply-chain attack patterns | `uv tool install git+https://github.com/sudo-ai-git/mcp-skill-sec` |
| [`mcp-verify-claim`](https://github.com/sudo-ai-git/mcp-verify-claim) | evidence-gated FACT/INFERENCE/SPECULATION/UNVERIFIED reporting | `uv tool install git+https://github.com/sudo-ai-git/mcp-verify-claim` |
| [`mcp-benchmark-hygiene`](https://github.com/sudo-ai-git/mcp-benchmark-hygiene) | detect pytest config-leakage corrupting agent-eval | `uv tool install git+https://github.com/sudo-ai-git/mcp-benchmark-hygiene` |
| [`harness-audit`](https://github.com/sudo-ai-git/harness-audit) | zero-dependency CLI: audit an agent-eval/CI workspace for the silent mis-scoring bug class | `uvx --from git+https://github.com/sudo-ai-git/harness-audit harness-audit <path>` |
| [`vulcanbench-findings`](https://github.com/sudo-ai-git/vulcanbench-findings) | documented benchmark-harness mis-scoring bug | [Pages](https://sudo-ai-git.github.io/vulcanbench-findings/) |

## How to hire

**Open an issue** using the [custom-build-request](.github/ISSUE_TEMPLATE/custom-build-request.yml)
template (or email pasted into a normal issue). You'll get a same-day scoping note
with a **fixed price band** — no commitment.

### Typical engagements

| build | scope | price band | timeline |
|---|---|---|---|
| **MCP connector** | one internal system → agent-reachable (auth, logging, 3–5 tools, security-scan pass) | $8K–$25K | 2–3 wks |
| **Connector + hosted** | above, plus hosted Streamable-HTTP endpoint + monitoring + 30-day support | $15K–$40K | 3–4 wks |
| **Agent verification layer** | wire `verify-claim` + `benchmark-hygiene` into your agent/test harness | $5K–$20K | 1–2 wks |
| **Agent-eval harness audit** | audit your agent-benchmark/CI grading for silent mis-scoring, config-leakage, and false pass/fail (the class of bug I found in VulcanBench — a repo-root `--cov` leak scored every functional task 0.0) | $2K–$8K | 3–5 days |

Billing: 40% kickoff / 60% acceptance. HIPAA / SOC 2 note if it applies — handled
with care.

**Why the harness audit is worth it before you trust a leaderboard:** automated
agent-eval harnesses routinely inherit host pytest config that turns real passes
into false fails (and vice-versa). I documented one such unverified bug publicly
([vulcanbench-findings](https://sudo-ai-git.github.io/vulcanbench-findings/)) — if
you've shipped an eval harness, a 3-day audit is cheap insurance against
publishing (or hiring against) a wrong number.

**Same forensics, applied to config/environment integrity:** the audit muscle
also catches silent mis-reading of env-var vs CLI defaults. Live contributions
in review — [`redis/mcp-redis#175`](https://github.com/redis/mcp-redis/pull/175)
(fix for [redis/mcp-redis#156](https://github.com/redis/mcp-redis/issues/156)):
CLI `--host/--port/--db` defaults silently overrode `REDIS_*` env vars, so the
env config was ignored. Alongside [`promptfoo#10525`](https://github.com/promptfoo/promptfoo/pull/10525)
and [`graphiti#1805`](https://github.com/getzep/graphiti/pull/1805) covering env
pass-through and config-path precedence in two more major tools.

## What you get (the honest part)

Every delivered connector ships with an *end-to-end test that drives the real MCP
transport* and a `server.json` that passes the Official MCP Registry schema. No
"it works in theory" — the test is the deliverable alongside the server.

If it's not a fit, no hard feelings — the MIT reference assets are free to use
either way, and reading them is exactly how you'd vet a build anyway.
