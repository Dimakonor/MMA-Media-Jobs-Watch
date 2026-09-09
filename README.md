# MMA Media Jobs Watch

A weekly job-scouting agent for combat-sports media work, plus the portfolio it supports.

## The agent

[`agent/`](agent/) contains a portable, self-contained agent that checks a fixed list of
combat-sports employers — UFC / TKO, ONE Championship, PFL, KSW, Migu — and reports only vacancies
that have not appeared in a previous report. Drop `SKILL.md` into a skills directory, or paste
`system-prompt.md` into any agent runtime.

Three rules do most of the work:

1. **Report deltas, not state.** Re-listing the same jobs every week teaches the reader to skip the
   report.
2. **Refuse to pad.** "Nothing new this week" is a valid answer. An agent that manufactures findings
   to look busy is worse than no agent.
3. **Every claim carries a link.** No listing exists until there is a URL and a date.

### Technique notes worth stealing

- **Workday portals** expose a JSON API at `/wday/cxs/<tenant>/<board>/jobs` (POST) and
  `/wday/cxs/<tenant>/<board>/job/<path>` (GET). Server-side curl is usually blocked; run `fetch()`
  from inside a browser session on the same origin and it works.
- **LinkedIn** blocks scraping but leaves a guest endpoint open:
  `/jobs-guest/jobs/api/seeMoreJobPostings/search?keywords=&location=&start=`. Returns parseable
  HTML cards with title, company, location, posted date and URL. Add `&f_TPR=r1209600` for the last
  14 days.
- Try clean-content extraction on public listing pages before spending a browser session. Escalate
  only when a page returns empty or a JavaScript shell.

See [`agent/sources.md`](agent/sources.md) for the source list with live/broken status.

## The portfolio

[`portfolio/index.html`](portfolio/index.html) — a single self-contained page for
**@zakulisie_sporta**, a backstage combat-sports channel: 115.7K followers, 2.5M likes, and 60.7M
views across its top three videos on UFC athletes. Backstage coverage of Petr Yan, Khamzat Chimaev,
Rafael Fiziev, Fedor Emelianenko, Bellator 269, ACA and EFC.

No build step, no dependencies. Open it in a browser or serve it from GitHub Pages.

## Market data

[`research/market-2026.md`](research/market-2026.md) — September 2026 salary and cost-of-living
figures in USD for combat-sports media roles in Shanghai, Singapore and Las Vegas, with the FX rates
and sources used. Includes what separates a 10–15K CNY editor role from a 20–30K 编导 role in
Shanghai, and the H-1B sponsorship record for UFC's operating entity.

## CV

[`resume/`](resume/) — English and Chinese versions. The Chinese one is written for the market, not
translated from the English.
