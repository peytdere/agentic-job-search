# Agentic Job Search Framework

## What this is

I built a few helpers to take the boring parts of my job search off my plate.

This is about 5x faster than doing it by hand. The bots never make up jobs I didn’t have, or skills I don’t have. If a posting uses different words for the same real work, they decide carefully whether to match those words. If the work isn’t in my history, they leave it out.

This page is the public story of how that works. My inbox, my full work history, and the live job list stay private.

## Who does what

**Job Watcher** reads job-alert emails and also searches LinkedIn for new postings. It only keeps roles that fit (the right kind of work, posted pay high enough, posted in the last 60 days). It logs them as Waiting for Review. It does not fill 10 Ready by itself.

**Resume Generator** opens my private work history (about 10 years of real jobs) and builds a one-page resume for that posting. It picks the relevant parts, shortens them, and may reuse the posting’s words when they still mean the same real work. It will not invent a job, a date, a tool, or a skill.

**Quality Reviewer** reads that resume next to the job posting. It flags weak fit, missing pieces, and anything that sounds made up. If something needs a fix, Resume Generator tries again.

**Cover Letter Generator** writes a short letter from the resume that passed review, not from thin air.

**Consigliere** works with me, keeps the other bots in line, holds them accountable, and pushes back on bad decisions. It still fills the application form and attaches the PDFs. It never clicks Submit.

I do captcha, logins, a last look, and the Submit click.

## A typical morning

Times are Pacific.

6:30am — Job Watcher looks at new emails and new listings. For each good one, it adds a row to my job tracking sheet: company, role, posted pay, when it was posted, the apply link. Status starts as Waiting for Review. Resume and letter docs wait.

7:00am — Consigliere checks that harvest happened. It does not auto-generate resumes or letters.

8:30am — Quiet unless harvest failed. If Watcher already logged the morning, nobody bothers me.

Late morning — When I sit down, Consigliere and I walk the Ready list until those rows say Applied. When Ready is already full, we do not add more rows until I ask. When I’m close to finishing the queue, Consigliere asks if I want more for the day. Otherwise we just muscle through what we have and e-high-five, because why not.

3:00pm on weekdays — Job Watcher only checks “you got an interview / you got rejected” mail. It does not pile on more new jobs. It just updates my tracking sheet.

## Resume generator in action

I keep one large private file of about 10 years of real work: jobs, dates, what I actually did, and the numbers that are true. It's basically the DISTINCT and UNION of 4 recent resumes that I put real time and effort into. That file never goes on GitHub.

For each posting, Resume Generator does three things:

1. Picks the parts of my history that match this job.

2. Shrinks those parts onto one page. It usually ends up being more than one and less than two when the final doc is generated, because LLMs are ADHD-adjacent, but that's okay. I'm not looking to dazzle with forceful brevity and a clean set of punches. I'm just making sure I am thorough while not completely overwhelming the human who might actually read it.

3. Sometimes uses the posting’s words when they still mean the same real work.

It will not invent a job, a date, a tool, or a skill. If the posting wants something I have never done, that line stays off the page.

Cover Letter Generator only writes after that resume exists. The letter has to match the resume, not a fantasy version of me. These files are not commonly required, but they usually don't go to waste, either. Most application pages ask if you want to explain why you want the job.

Quality Reviewer reads both next to the posting and sends anything fishy back for a fix.

Consigliere will start filling fields, then dump the cover letter material in the "why you want the job" field, and I will usually ruthlessly edit and put things in my own friendlier voice. Nothing I submit, even the resume, ever goes untouched. That's the only way to be.

## What this runs on

This is Cursor and Grok Bot, not a custom app I built from scratch.

Each helper is a Grok Bot with a job. Cursor is where they live, where the morning alarms are set, and where Gmail and Google Drive get plugged in.

The helpers also have a computer of their own: a Linux desktop with Chrome. That’s where they open job sites, fill forms, and save PDFs. When a site needs my password, a captcha, or the Submit click, I take that computer for a minute.

### How Job Watcher finds jobs

1. LinkedIn already emails me Job Alerts. Job Watcher reads those emails through Gmail (that part is a real Google connection, not scraping).

2. Each email is only a teaser, so Watcher opens the job link in Chrome when it needs pay, when it was posted, and the real apply button. It logs Waiting for Review. It does not turn every posting into a resume packet.

3. It also searches for extra matches the same way a person would: run a search, open the listings, keep the good ones. That is not a LinkedIn API. **It’s a browser on the helper computer looking at search pages. I’ll say that again: the bot uses a browser and searches for jobs.**

If LinkedIn asks that computer to log in, I have to do that once. Job Watcher does not get a secret feed.

Resumes and letters are Google Docs. The queue is a Google Sheet. Apply pages are whatever the company uses (Greenhouse, Lever, SmartRecruiters, or their own site).

For my own work, this feels like the third big jump I’ve seen in AI. First was self-attention at scale, when text generation actually got useful. Second was chain of thought, and some real ability to break a problem into steps. Third is this: bots that can operate computers, together.

## How long this takes

These are guesses from using it, not a stopwatch study.

By hand, one application is about 30 to 50 minutes of real focus, mostly tailoring the resume and hitting keywords so the ATS doesn’t throw it out.

With this system, one application is about 5 to 10 minutes. A lot of that is waiting for Consigliere to fill fields carefully, or for a captcha or login to show up. I can do something else in that window, or just relax and play with my toddler.

Ten 'Ready' jobs is about 5 to 8 hours by hand, or about an hour of half-attention with the helpers. That’s roughly 5x faster, which is the point.

## Stack

This runs on **Cursor + Grok Bot**, not a custom orchestrator.

| Layer | What it is |
| --- | --- |
| Agents | Grok Bot agents, each with a specialist brief |
| Scheduling / tools | Cursor routines and MCP |
| Runtime | A persistent agent Linux computer with Chrome |
| Mail / files | Gmail and Google Drive connectors |
| Artifacts | Google Docs (resumes, letters) and Google Sheets (tracker) |
| ATS surfaces | Greenhouse, Lever, SmartRecruiters (plus employer career pages when those resolve) |

LinkedIn is an **email ingest**, not an API. Job alerts land in Gmail; the watcher reads those messages. There is no LinkedIn posting API in this design.

## Architecture

See [docs/architecture.md](docs/architecture.md) for data flow and failure modes.

## Agents

Details: [docs/agents.md](docs/agents.md)

## Time comparison (ESTIMATES, not a timed study)

These are **order-of-magnitude estimates** from running the search, not a stopwatch study, not a benchmark, and not a productivity claim with fake precision.

**Per apply**

| | Estimate |
| --- | --- |
| Manual (no pipeline) | **30–50 min** |
| This pipeline, human last mile | **5–10 min** |

| Typical Workflow | Estimate |
| --- | --- |
| Review the Ready packet | 1–3 min |
| Captcha, when present | 0.5–2 min |
| First login / 2FA on a site | 1–3 min (amortized across later applies on that ATS) |
| Optional resume skim (Doc linked in tracker) | 2–5 min |
| Submit | ~10 seconds |

## What's in this repo

```
README.md                      this case study (includes resume/letter strategy)
docs/architecture.md           components, data flow, failure modes
docs/agents.md                 who owns what; select / condense / reword
docs/human-in-the-loop.md      last-mile limits
docs/schedule.md               Pacific cadence and caps
prompts/                       sanitized role briefs (not the live ones)
LICENSE                        MIT
```

What's **not** in this repo:

- Personal contact info, inbox contents, or live tracker rows
- The resume source bank
- Agent identifiers, credentials, connector configs, or Drive / Sheet IDs
- Real job descriptions or generated documents

## Prompts vs. production

The files under `prompts/` are **illustrative briefs**: the job of each specialist and the rules it has to obey. They are not a drop-in clone of the running system, and they are not enough to recreate anyone's private search.

If you adapt this, write your own source bank, set your own floors, and keep PII out of git.

## Status

Personal production system. The public artifact here is the design, not a hosted app.
