# Schedule

All times **Pacific (PT)**. Harvest runs **daily, including weekends**. Outcome-mail is **weekdays only**.

This is the operating cadence, not a SLA. Agents can miss a window; the human does not owe the clock a Submit.

## Daily

| Time (PT) | Actor | What | Constraint |
| --- | --- | --- | --- |
| **6:30am** | Watcher | Harvest new alerts (and assigned searches). Gate. Dedupe. Log **Waiting for Review** (company, role, pay, post date, apply link). Docs wait. | Daily, including weekends. Work **toward Waiting for Review**, not 10 Ready. Do not follow every JD into a packet. Do not add rows if Ready is already ~10. Do not replay backlog. |
| **7:00am** | Consigliere | Check that harvest happened. Nudge Watcher to log Waiting for Review if it did not. | Do **not** start generators for unreviewed rows. Do not fill 10 Ready. Do not write the resume or letter. Do not Submit. |
| **8:30am** | Consigliere | Stay quiet unless harvest failed. | If harvest ran, stay silent — even if Ready is under the cap. One ping only if Watcher never ran or logged nothing. Not a second harvest. |
| **3:00pm** | Watcher | **Outcome-mail only.** | **Weekdays.** A cue to look at recruiter / ATS outcome mail. Not a harvest, not auto-reply. |
| Unscheduled | Human + Consigliere | Approve Waiting for Review (or slam dunk). Then generate → Quality Reviewer → letter → Ready. Apply-walk Ready → Applied. | Submit is human-only. Captcha, file pickers, 2FA as they appear. When Ready is full, do not add more until the human asks. |

Weekends get 6:30 harvest + 7:00 harvest-check + 8:30 quiet-unless-failed. They do not get the 3pm outcome-mail.

## Caps and example policy

| Rule | Example in this search |
| --- | --- |
| Harvest status | **Waiting for Review**, apply URL only. Docs wait until the human (or slam dunk) says the row is ready. |
| Ready cap | **~10 Ready** is a last-mile full queue. Extra qualifying jobs wait. Do not generate past the cap. Do not add harvest rows when Ready is already ~10. |
| Compensation | Posted salary required. Example floor **$200k posted**. Ranges must actually reach the floor. Pay is a **floor**, not a rank key. |
| Fit first | Rank HITL / evals / data ops / AI-related PM fit ahead of a bigger number. |
| Skip family | Cloud infra, compute, SPMO, horizontal BizOps, infra TPMs. |
| Freshness | Skip if **older than 60 days**. Skip if **no post date**. |
| Role | Target family only (HITL / evals / data ops / AI-related PM). |
| New-only | No day-one replay of the historical inbox. |
| Dedupe | One row per job id. |
| Quality Reviewer | **On** every packet that generates. No letter without a pass. |

Skip is success. A morning that logged Waiting for Review at 6:40am is success; 7am does not start generators; 8:30 stays quiet.

## How this meets the human

The morning is for **harvest rows the human can review**. Generation is after that review (or a slam dunk). The afternoon weekday mail is for **outcomes**. The human is not scheduled at a fixed apply hour — they walk Ready rows when they can. The Ready cap exists so a weekday apply-walk is **about 20–80 minutes** for 10 Ready, as an **estimate**, versus **about 12–20 hours** to do those same ten fully manually. See the time comparison in the root [README](../README.md) (labeled estimates, not a timed study).

## What the schedule does not do

- Does not click Submit
- Does not solve captcha
- Does not connect Gmail / Drive
- Does not complete 2FA on the agent computer
- Does not auto-handle recruiter inbound
- Does not start Resume Generator on unreviewed Waiting for Review rows
- Does not fill 10 Ready because the clock hit 7:00
- Does not ping at 8:30 when harvest already ran
- Does not add rows because "there were good jobs after Ready was full"
