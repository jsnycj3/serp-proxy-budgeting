# serp proxies: How to Pick and Budget IPs for Google Rank Tracking and SERP Scraping

Most people who search for SERP proxies aren't looking for a definition. They already know what a proxy is. They've bought a pile of residential IPs, pointed their rank tracker or scrapy at Google, and watched the whole thing collapse into CAPTCHAs, timeouts, and half-empty CSVs after about forty requests. The question is usually narrower: which IP type actually survives Google, how much traffic will this burn, and what am I supposed to be paying for it.

That's what this covers. What makes search engines a different target from an ordinary site, how the pricing math works out once you account for how heavy a results page is, and how a per-IP provider like 9Proxy fits into a SERP workflow — including its full current price list.

## What "SERP proxies" really describes

A SERP proxy is just a proxy you use against a search engine. Nothing exotic about the technology. What makes the phrase stick is that search engines sit at the far end of the difficulty scale, so the requirements that follow are stricter than for generic scraping.

Google, Bing, and Yandex evaluate request patterns per address. Send a handful of automated queries from one IP and you start getting served a consent wall, a CAPTCHA, or a degraded page instead of ten blue links. A benchmark from AIMultiple that pushed 5,000 URLs per domain through residential IPs found success rates clustering around 50% for the leading providers — roughly 54% for the best performer, 52% for the runner-up. That's the ceiling for a good residential network against search engines, not a budget problem.

Meanwhile the job itself got heavier. Google increasingly requires JavaScript to render results, retired the `num=100` parameter (so what used to be one request is now ten), and pushes AI Overviews mainly to mobile traffic. More requests, more bytes, and a block layer that reacts in seconds.

## Why a general-purpose pool falls apart on a results page

Two failure modes show up again and again.

**Datacenter IPs get flagged almost immediately.** They're cheap and fast, and against Google in particular they survive somewhere in the range of 5–10 requests before friction appears. That's fine for debugging your parser. It is not fine for tracking 2,000 keywords.

**Residential IPs work, but only if the pool is clean and the rotation is sane.** Residential addresses look like real household connections, which is why they carry the bulk of serious SERP work. The catch is that quality varies more between providers than price does, and a stale or recycled address behaves like a datacenter one.

Mobile proxies sit in a category of their own. Carrier-grade NAT means hundreds of real subscribers share each address, so a blanket ban on a mobile range costs the search engine legitimate users too. One 2026 guide to Google scraping puts mobile IPs at 50–200 requests before friction, versus 5–10 for datacenter. They're also the type that reliably triggers AI Overviews, because Google renders those blocks for mobile audiences first-and-foremost.

| IP type | Holds up against | Breaks down when | Cost shape |
| --- | --- | --- | --- |
| Datacenter | Bing, DuckDuckGo at low volume; parser testing | Google, within a few requests | Cheapest per IP |
| Rotating residential | Volume organic collection, positions, snippets, local packs | Heavy mobile-only blocks; weak pools degrade fast | Per GB or per IP |
| Sticky residential | Repeatable rank checks, multi-step flows | Broad keyword sweeps that need constant rotation | Per GB or per IP |
| Mobile | AI Overviews, hardened queries, local accuracy | Budget — usually the priciest per GB | Per GB |

## The bandwidth trap nobody warns you about

If you're on per-GB billing, the price on the rate card tells you less than the weight of what you're downloading. A full SERP with scripts and images can run 2–5 MB per page. Strip images and trackers and keep the DOM, and you're nearer 80–500 KB.

Here's the same per-GB rate applied to different page weights, assuming a $2/GB residential rate:

| Page weight | Pages per GB | Cost per 1,000 pages |
| --- | --- | --- |
| 3 MB (full page, no blocking) | ~341 | ~$5.86 |
| 500 KB (scripts kept, images blocked) | ~2,048 | ~$0.98 |
| 80 KB (DOM only, aggressive blocking) | ~12,800 | ~$0.16 |

The spread between the top and bottom row is more than thirty times, and it comes entirely from how you configure the scraper — not from which vendor you picked. If your SERP tool renders JavaScript and doesn't block anything, you can burn through 200 GB faster than you'd expect: 100,000 full-weight pages is somewhere in the 300 GB range.

That's the argument for per-IP pricing on SERP work. When bandwidth is unlimited and you're paying per address, page weight stops being a budgeting variable. Whether you pull 10,000 pages or 200,000 through that IP, the invoice is the same.

## Sizing a SERP proxy setup

Skip the "one proxy per X keywords" rules floating around; there isn't a universal ratio, and any sales page that offers one is guessing. Do the multiplication yourself:

1. Tracked keywords.
2. × number of locations you check (country, city, ZIP — each is a separate SERP).
3. × device variants (desktop and mobile produce different results, especially with AI blocks in play).
4. × retries and pagination depth. Ten pages of results instead of one is a tenfold multiplier.
5. + periodic competitor checks on the same queries.

That number is your request volume. Then decide session behaviour. Rank tracking rewards stability: a sticky session over a short window keeps results comparable between runs, because the IP's geography doesn't drift mid-check. Broad keyword sweeps reward rotation, since you're not comparing anything run-to-run and you want each request to look like a different person.

One practical gotcha: don't use `google.com` as your proxy connectivity test. Most serious providers block search-engine targets from generic proxy zones, and you'll see a proxy error on a perfectly healthy IP. Test against a neutral endpoint, then test the search engine separately with your real query set.

## Where 9Proxy fits into SERP work

9Proxy is a residential proxy provider running a 20M+ IP pool across 90+ countries, with targeting down to country, city, ZIP code, and ISP level over HTTP(S) and SOCKS5. The company advertises 99.95% uptime, and its stated audience is squarely SEO teams, market researchers, and data analysts doing scraping, SERP analysis, and price aggregation.

The billing model is the part that matters for the workflow above. You can buy IPs with unlimited bandwidth and no expiry on unused addresses, or buy traffic in GB blocks, or combine both in a bundle. Access methods differ by model: IP-based packages run through a desktop proxy program that routes traffic at the OS level (with port-level auto-rotation and auto-refresh), while GB-based traffic works straight from the dashboard via username/password or IP whitelist, which is the simpler path for browser automation and anti-detect setups.

A few mechanics worth knowing before you commit:

- IP-based addresses live somewhere between a few hours and roughly 24 hours. Long-acting sessions are the point; permanent addresses are not.
- Auto-refresh swaps out addresses that drop offline, which matters when a run is only half finished.
- The company advertises a 60-second credit for any IP that fails to connect on first use.
- Sticky and rotating sessions are supported on both billing models.

👉 [Check 9Proxy's current sign-up offer and plan options](https://bit.ly/9-Proxy)

## 9Proxy pricing: every plan currently on offer

Prices below reflect the adjustment that took effect on 1 June 2026, when IP-based packages and bundles were repriced and GB-based packages stayed put.

### IP-based residential packages (unlimited bandwidth per IP)

| Package | Price per IP | Total | Purchase |
| --- | --- | --- | --- |
| 100 IPs | $0.24 | $24 | [Start with 100 IPs](https://bit.ly/9-Proxy) |
| 500 IPs | $0.144 | $72 | [Grab the 500 IP package](https://bit.ly/9-Proxy) |
| 1,000 IPs + 500 bonus | $0.084 | $126 | [Take the 1,500 IP deal](https://bit.ly/9-Proxy) |
| 2,500 IPs | $0.084 | $210 | [Compare the 2,500 IP tier](https://bit.ly/9-Proxy) |
| 5,000 IPs | $0.072 | $360 | [See the 5,000 IP pricing](https://bit.ly/9-Proxy) |
| 15,000 IPs | $0.048 | $720 | [Review the 15,000 IP package](https://bit.ly/9-Proxy) |
| 25,000 IPs | $0.035 | $863 | [Check the 25,000 IP tier](https://bit.ly/9-Proxy) |
| 50,000 IPs | $0.029 | $1,438 | [Open the 50,000 IP option](https://bit.ly/9-Proxy) |
| 100,000 IPs (Business) | $0.023 | $2,300 | [See the 100,000 IP business plan](https://bit.ly/9-Proxy) |
| 200,000 IPs (Business) | $0.021 | $4,140 | [View the 200,000 IP plan](https://bit.ly/9-Proxy) |
| 500,000 IPs (Business) | $0.018 | $8,625 | [Request the 500,000 IP plan](https://bit.ly/9-Proxy) |

### GB-based residential packages

| Package | Price per GB | Total | Traffic validity | Purchase |
| --- | --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days | [Try the 5 GB pack](https://bit.ly/9-Proxy) |
| 50 GB + 5 GB bonus | $2.10 | $105 | 180 days | [Get the 55 GB pack](https://bit.ly/9-Proxy) |
| 100 GB | $1.50 | $150 | 180 days | [Pick the 100 GB plan](https://bit.ly/9-Proxy) |
| 200 GB | $1.00 | $200 | 180 days | [See the 200 GB plan](https://bit.ly/9-Proxy) |
| 1,000 GB | $0.80 | $800 | 180 days | [Review the 1,000 GB plan](https://bit.ly/9-Proxy) |
| 2,000 GB | $0.75 | $1,500 | 180 days | [Compare the 2,000 GB plan](https://bit.ly/9-Proxy) |
| 3,000 GB (Enterprise) | $0.72 | $2,160 | No expiry | [Check the 3,000 GB enterprise pack](https://bit.ly/9-Proxy) |
| 6,000 GB (Enterprise) | $0.70 | $4,200 | No expiry | [View the 6,000 GB enterprise pack](https://bit.ly/9-Proxy) |
| 10,000 GB (Enterprise) | $0.68 | $6,800 | No expiry | [Open the 10,000 GB enterprise pack](https://bit.ly/9-Proxy) |

### Bundle packages (IPs + bandwidth)

| Bundle | Contents | Price | Traffic validity | Purchase |
| --- | --- | --- | --- | --- |
| Starter | 100 IPs + 5 GB | $30 | 180 days | [Start with the Starter bundle](https://bit.ly/9-Proxy) |
| Popular | 1,500 IPs + 50 GB | $180 | 180 days | [Take the Popular bundle](https://bit.ly/9-Proxy) |
| Pro | 5,000 IPs + 500 GB | $720 | 180 days | [Go with the Pro bundle](https://bit.ly/9-Proxy) |

Payment covers cards, crypto (USDT, BTC, ETH, LTC, DOGE), Alipay, Apple Pay, and Google Pay. 9Proxy also states that certain payment methods add a 5% discount or a 5% balance bonus, and the affiliate program attached to the sign-up link above carries a 5% discount for referred users.

## Which tier actually suits a SERP job

Working through the math, most SERP setups land in one of three places.

**Solo SEO or a small site.** A handful of clients, a few hundred tracked keywords, one or two markets, sticky sessions for repeatable checks. The 100 IP package at $24 or the Starter bundle at $30 is the sensible entry, and the bundle wins here — rank tracking at low volume doesn't consume much traffic, so 5 GB stretches further than you'd think.

**Agency with real clients.** Multiple markets, desktop and mobile variants, scheduled runs several times a week. This is where the IP-based model earns its place: 500 IPs at $72, or 1,500 IPs plus bonus at $126 once the keyword list gets long. Rotating through five hundred addresses for hourly checks is well inside normal territory. If a chunk of the work is broad sweeps against e-commerce and only part is ranking checks, the Popular bundle at $180 covers both without buying the two products separately.

**SERP data operation.** Continuous collection, thousands of queries per location, AI Overview capture, historical archiving. At that point traffic is the constraint, not IP count, and the numbers get boringly linear: 1,000 GB at $800 or 2,000 GB at $1,500 on the GB side, or 15,000 IPs at $720 if the workload is bandwidth-heavy but IP-light. The enterprise GB blocks are the ones to look at if your volume never lines up neatly with a 180-day window — those don't expire.

## Honest limitations

9Proxy is a proxy network, not a managed SERP API. If you want parsed JSON of Google results without maintaining a scraper, a SERP API product is the tool you're after, and no amount of clean IPs replaces it. What you get here is the raw connection quality underneath your own parser.

The GB packages carry a 180-day validity window, so bulk traffic bought "for later" is a bad idea unless you buy an enterprise block. IP-based packages require the desktop client for routing, which is a friction point on headless Linux boxes; GB-based traffic avoids that via standard credentials. And address lifetimes of hours-to-24-hours mean anything depending on the same IP for days — long-lived accounts, for instance — belongs on a sticky session with a plan for rotation, not on a permanent-address assumption.

The last one is not specific to this provider: test before you commit. Buy the smallest package that lets you run your real queries against your real targets for a few days, and measure success rate per region yourself. Pool quality shifts, and a trial against your own workload beats any benchmark table.

## Quick answers

**Do I need mobile proxies for SERP work?** Only if AI Overviews or the most hardened queries are the target. Regular organic results, positions, snippets, and local packs are residential work.

**Per-IP or per-GB?** If your SERP pages are heavy or you render JavaScript, per-IP with unlimited bandwidth removes the guesswork. If your requests are lightweight and bursty, GB billing usually costs less.

**How many IPs do I need?** Multiply keywords by locations by device variants, add retries, then divide by how hard you're willing to push each address. Most teams underestimate the locations and device multipliers and overestimate the IP count they actually need.

**Will a proxy alone stop CAPTCHAs?** No. Your request pacing, TLS handshake, headers, and User-Agent all get evaluated alongside the IP. Randomised delays beat fixed intervals, and a matching browser handshake resolves blocks that header spoofing can't.

**Can I test 9Proxy before buying?** The company runs a limited trial for new users depending on availability — ask for either an IP-based or a GB-based trial when you register.

👉 [Sign up and pick the SERP proxy package that matches your volume](https://bit.ly/9-Proxy)
