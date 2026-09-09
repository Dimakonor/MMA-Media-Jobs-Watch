# Source list — access notes

Verified 10 September 2026.

| Source | Access | Note |
|---|---|---|
| `wwecorp.wd5.myworkdayjobs.com/en-US/UFC` | ✅ via browser + in-page fetch | Server-side curl blocked. JSON API at `/wday/cxs/wwecorp/UFC/jobs` |
| `showbizjobs.com/jobs/company/ufc` | ✅ clean extraction | Mirrors the portal, lags a few days |
| `hirenata.com` | ⚠️ unverified this pass | |
| `careers.onefc.com` | ❌ HTTP 500 | Down. `onefc.com/careers` returns 404 |
| ONE via LinkedIn guest API | ✅ | The only working route to ONE listings |
| `pflmma.com/careers` | ✅ | "No job openings right now" as of this pass |
| `kswmma.com/kariera` | ❌ 404 | |
| `ksw.pl/kariera` | ❌ error | |
| LinkedIn company pages | ❌ authwall | Guest jobs API works; company pages do not |
| `mycareersfuture.gov.sg` | ✅ | ONE does not post there |
| Chinese media on Migu | ✅ | Sina, China Daily, Shanghai municipal sports bureau |

## Reusable endpoints

```
# Workday listing (from inside a browser session on the same origin)
POST /wday/cxs/wwecorp/UFC/jobs
{"appliedFacets":{},"limit":20,"offset":0,"searchText":""}

# Workday job detail
GET /wday/cxs/wwecorp/UFC/job/Las-Vegas-NV/Videographer_R0007860

# LinkedIn guest jobs (last 14 days)
GET /jobs-guest/jobs/api/seeMoreJobPostings/search?keywords=ONE%20Championship&location=Singapore&f_TPR=r1209600&start=0
```
