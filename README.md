# The resource wire — control of resources, worldwide

Abortion worldwide, in 25 languages: statutes and court rulings, referendums and bills, clinics and
travel, medication and telehealth, prosecutions, health outcomes and data, international bodies and
the aid attached to them, the movements on both sides, and the data-privacy fights that now come
with all of it.

`harvest_resource.py` runs every two hours in GitHub Actions, reads 61 wires, tags and weighs what
it finds, and writes `wire_resource.json`. `index.html` loads that file and renders it.

Nothing here rewrites a headline. Titles and snippets are the publishers' own, truncated but never
reworded, and every row keeps its original link. No model in the pipeline, no API key, no paid
service, no dependencies beyond the Python standard library.

## Both movements are carried

This is a contested subject, and the feed is built to show the argument rather than to settle it.
A sector on its own is refused; every sector term is gated behind a control term, each wire labelled
on every row it produces, alongside courts, health institutions, research and general press.

| Standing | What it covers |
|---|---|
| Courts & institutions | WHO, UN, court reporting, legal news services |
| Research & health | The Lancet, BMJ, KFF Health News, Guttmacher, Human Rights Watch |
| Press | General news, 25 language editions |
| Abortion-rights advocacy | Center for Reproductive Rights, IPPF, Rewire News Group |
| Industry & finance | Financial press and industry bodies |

Standing is provenance, not endorsement. Filter to one to read a single side; leave it open to read
the argument. The balance of the feed is the balance of `sources_resource.json`, which is meant to
be edited.

## Weight

Separately, each story is scored on what it contains:

| Signal | Worth |
|---|---|
| A decision: ruling, law enacted, referendum result, conviction | 2 |
| Institutional material: WHO or UN guidance, official statistics, a health ministry, peer review | 2 |
| A measured figure | 1 |
| A pending decision with a date attached | 1 |
| A named jurisdiction | 1 |
| Primary source | 1 |

At **3** or more a row is marked consequential, and the *Weight* filter narrows to those. A campaign
statement and a constitutional judgment both appear; the pips are how you tell them apart at a
glance, and the words beside them say what earned the score.

## Ten subjects

Courts & rulings, Legislation & referendums, Access & services, Medication & telehealth,
Criminalisation & enforcement, Health outcomes & data, International bodies & aid, Movements &
protest, Data & privacy, Conflict & crisis settings. Each story carries every subject it matches.

## What is refused

The word *abort* in its other senses — aborted launches, landings, mergers, transactions — plus the
usual commercial and horoscope noise. The status line reports how many stories each harvest refused.

## Files

| File | Path in repo | What it is |
|---|---|---|
| `index.html` | `/index.html` | The feed page. Pages serves the repo root, so it must carry this name. |
| `harvest_resource.py` | `/harvest_resource.py` | The harvester. Self-contained. |
| `sources_resource.json` | `/sources_resource.json` | The wire list, with each wire's standing. |
| `wire_resource.json` | `/wire_resource.json` | The output the page reads. Empty placeholder until the first run. Never hand-edit. |
| `resource-feed-weebly-embed.html` | `/resource-feed-weebly-embed.html` | The page wrapped for a Weebly Embed Code element. Regenerate after changing `index.html`. |
| `README.md` | `/README.md` | This file. |
| `harvest.yml` | `/.github/workflows/harvest.yml` | Runs every two hours at :31 and commits the wire. |

## Setup

1. Push these files to the repository root.
2. Settings → Actions → General → Workflow permissions → **Read and write permissions**, save.
3. Actions tab → **Harvest the resource wire** → *Run workflow*.
4. Settings → Pages → **Deploy from a branch**, branch `main`, folder `/ (root)`.
5. Confirm
   `https://raw.githubusercontent.com/WelcomeToYourGalaxy/resource-feed/main/wire_resource.json`
   loads in a browser.

If the repository is named something other than `resource-feed`, change `REPO` near the top of the
feed script in `index.html` and regenerate the embed.

## Languages

English (US, UK, India, Australia, Ireland, Kenya, Nigeria, South Africa), Spanish (Spain, Mexico,
Argentina), Portuguese, French, German, Italian, Polish, Dutch, Swedish, Greek, Russian, Ukrainian,
Turkish, Arabic, Persian, Hindi, Bengali, Indonesian, Vietnamese, Thai, Japanese, Chinese
(simplified and traditional), Korean, Swahili. Each query is written in that language, not
translated at read time.

## Event searches

Eight aimed at happenings rather than commentary: courts and rulings, legislation and referendums,
money creation, lending and its conditions, trade and investment rule, land, harvest, water, routes,
bodies, movements and protest.

## Limits worth knowing

The gate is mechanical: it reads words, not meaning. Standing is assigned per wire rather than per
article, so a straight news piece from an advocacy outlet still carries that outlet's label, and a
slanted piece from a wire service does not. Google News caps a query at roughly 100 results over
about 30 days. Coverage is uneven by language and the counts show it rather than hiding it.

## Running it locally

```bash
python3 harvest_resource.py              # full run
python3 harvest_resource.py --dry-run    # harvest and report, write nothing
python3 harvest_resource.py --fixtures tests/
```

Python 3.9 or later.
