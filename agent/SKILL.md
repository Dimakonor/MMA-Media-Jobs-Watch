---
name: mma-media-jobs-watch
description: Weekly scout for video/content jobs at combat-sports organizations (UFC/TKO, ONE Championship, PFL, KSW, Migu), focused on Asia and remote/contractor roles. Reports only listings not seen in previous reports, each with a link and date.
when_to_use: Use when asked to check for new combat-sports media vacancies, to run a scheduled job-watch pass, or to research hiring at UFC, ONE, PFL, KSW or Migu.
tags: [jobs, mma, ufc, one-championship, media, scouting, asia]
---

# MMA Media Jobs Watch

## Purpose

Check a fixed source list on a schedule and report **only new** video/content vacancies at
combat-sports organizations. The value is in the filter, not the volume.

## Candidate profile this filters for

Video editor / content producer with an AI stack (Runway, Midjourney, ElevenLabs), inside-industry
combat-sports experience, fluent English, conversational Chinese, based in Russia. Strategic goal:
contractor or staff on a UFC content team in Asia (Shanghai / Singapore). Also in scope: ONE
Championship, PFL, KSW.

## Sources

| Source | URL | Notes |
|---|---|---|
| UFC / TKO Workday | `wwecorp.wd5.myworkdayjobs.com/en-US/UFC` | Primary. Filter Shanghai, Singapore, China, Asia, remote, contractor |
| ShowbizJobs mirror | `showbizjobs.com/jobs/company/ufc` | Lags the portal by days; useful cross-check |
| HireNata | `hirenata.com` | UFC listings |
| ONE Championship | `careers.onefc.com` | **Currently returns a server error — use LinkedIn** |
| PFL | `pflmma.com/careers` | Often "no openings"; check anyway |
| KSW | `ksw.pl`, `kswmma.com` | No careers page found; LinkedIn is the route |
| LinkedIn — UFC Asia | search "UFC Asia hiring content", "UFC Shanghai hiring video", "UFC Performance Institute Shanghai hiring" | Employee posts often precede official listings |
| Migu | Chinese media, Migu Video careers | UFC's China co-organizer since Aug 2026 |

## Relevance filter

**In scope:** Video Editor, Social Media Video Editor, Content Producer, Videographer, Motion
Designer, Live Streaming / Media Management, Digital Content, Localization / Dubbing, Creative
Producer — plus any contractor or freelance role at these companies in Asia.

**Out of scope:** sports, medical, coaching and administrative roles.

**One exception, flagged loudly:** if UFC Performance Institute Shanghai opens *any* media role,
that is a high-signal event. It has never happened. Call it out separately.

## Output contract

For each new vacancy:

- Company
- Exact role title
- Location
- Employment type (staff / contractor / remote)
- 2–3 key requirements
- Fit against the profile: high / medium / stretch — **and why**
- Direct link
- Posting date

Close with exactly one piece of advice on how to approach the application, grounded in the profile:
multilingual EN/RU/ZH content, combat-sports access, AI pipeline.

**When nothing is new, reply with one line:**
`Новых подходящих медиа-вакансий за неделю нет. Проверены: [source list].`

Do not restate old vacancies. Do not offer generic career advice. Do not invent listings — a
vacancy exists only if there is a URL.

## Technique

**Workday portals** expose a JSON API. Listing:

```
POST /wday/cxs/<tenant>/<board>/jobs
{"appliedFacets":{},"limit":20,"offset":0,"searchText":""}
```

Full description:

```
GET /wday/cxs/<tenant>/<board>/job/<externalPath>
```

Server-side curl is typically blocked. Navigate a browser session to the portal, then run `fetch()`
against the same origin from inside the page — that works.

**LinkedIn** blocks scraping but the guest endpoint is open:

```
GET /jobs-guest/jobs/api/seeMoreJobPostings/search?keywords=<kw>&location=<loc>&start=0
```

Returns HTML cards; parse `h3` (title), `h4` (company), `.job-search-card__location`,
`time[datetime]`, and the anchor href. Add `&f_TPR=r1209600` to limit to the last 14 days.
Fetch from inside a browser session, not from the shell.

**General:** try clean-content extraction on public listing pages before spending a browser session.
Escalate to a browser only when a page returns empty or a JavaScript shell.

## Failure modes to avoid

- **Padding.** An empty week is a real result. Reporting marginal or out-of-scope roles to look
  productive destroys the signal the report exists to provide.
- **Restating.** If it appeared in a previous report, it is not news.
- **Guessing.** No link, no listing.
- **Scope creep.** Sports-science and admin roles at MMA promotions are not media jobs.
