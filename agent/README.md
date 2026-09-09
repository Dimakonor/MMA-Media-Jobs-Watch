# MMA Media Jobs Watch — the agent

This folder contains the agent that produced everything else in this repo, packaged so it can be
re-created anywhere: Hyperagent, Claude Code / OpenCode (as a skill), or any agent runtime that
accepts a system prompt.

| File | Use |
|---|---|
| `SKILL.md` | Portable skill definition — drop into a skills directory |
| `system-prompt.md` | The raw system prompt, Russian, ready to paste into an agent config |
| `sources.md` | The source list with access notes and known breakages |
| `report-format.md` | The output contract |

## What it does

Once a week it checks every combat-sports employer that could plausibly hire a multilingual video
producer for Asia, and reports **only vacancies that have not appeared in a previous report**.
If nothing new is relevant, it says so in a single line and stops. No filler, no career advice,
no invented listings.

## Why it works the way it does

Three rules do most of the work:

1. **Report deltas, not state.** Re-listing the same jobs every week trains the reader to skip the
   report. Only new items appear.
2. **Refuse to pad.** "Nothing new this week" is a valid, useful answer. An agent that manufactures
   findings to look busy is worse than no agent.
3. **Every claim carries a link.** No listing exists until there's a URL and a date.

## Re-creating it

**Hyperagent:** create an agent, paste `system-prompt.md`, enable web search (Exa mode) and Browser,
schedule weekly.

**Claude Code / OpenCode:** copy this folder into your skills directory. The skill triggers on
combat-sports job-scouting requests.

**Anything else:** `system-prompt.md` is self-contained.

## Technique notes worth stealing

- **Workday portals** expose a JSON API at `/wday/cxs/<tenant>/<board>/jobs` (POST) and
  `/wday/cxs/<tenant>/<board>/job/<path>` (GET) for full descriptions. Server-side curl is usually
  blocked; run `fetch()` from inside a browser session on the same origin and it works.
- **LinkedIn** blocks scraping but leaves a guest endpoint open:
  `/jobs-guest/jobs/api/seeMoreJobPostings/search?keywords=&location=&start=`. Returns parseable
  HTML cards with title, company, location, posted date and URL. Same trick — fetch from an
  in-browser session, not from the shell.
- Try ExaContents on public listing pages before spending a browser session. Escalate only when a
  page returns empty or a JS shell.
