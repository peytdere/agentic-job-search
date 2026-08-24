# Schedule

All times **Pacific (PT)**. Harvest runs **daily, including weekends**. Outcome-mail is **weekdays only**.

This is the operating cadence, not a SLA. Agents can miss a window; the human does not owe the clock a Submit.

## Daily

| Time (PT) | Actor | What | Constraint |
| --- | --- | --- | --- |
| **6:30am** | Watcher | Harvest new alerts (and assigned searches). Fetch JDs. Gate. Dedupe. | Daily, including weekends. Work **toward 10 Ready**. Do not replay backlog. |
| **7:00am** | Coordinator | Kick generators for packets that already passed gates. | Do not write the resume or letter. Do not Submit. |
| **8:30am** | Coordinator | **Shortfall ping only.** | Fire if Ready is under the cap. Stay silent if the morning already hit 10. Not a second harvest. |
| **3:00pm** | Coordinator (or a thin routine) | **Outcome-mail only.** | **Weekdays.** A cue to look at recruiter / ATS outcome mail. Not a harvest, not auto-reply. |
| Unscheduled | Human | Apply-walk Ready → Applied | Submit is human-only. Captcha, file pickers, 2FA as they appear. |

Weekends get 6:30 harvest + 7:00 kick + 8:30 shortfall ping. They do not get the 3pm outcome-mail.

## Caps and example policy

| Rule | Example in this search |
| --- | --- |
| Ready cap | **10 Ready / day**. Extra qualifying jobs wait. Do not generate past the cap to "use" the agents. |
| Compensation | Posted salary required. Example floor **$200k posted**. Ranges must actually reach the floor. |
| Freshness | Skip if **older than 60 days**. Skip if **no post date**. |
| Role | Target family only (program / TPM / AI data ops / evaluation / HITL / governance). |
| New-only | No day-one replay of the historical inbox. |
| Dedupe | One packet per job id. |

Skip is success. Hitting 10 Ready at 7:40am is success; the 8:30 ping stays quiet.

## How this meets the human

The morning is for **packets**. The afternoon weekday mail is for **outcomes**. The human is not scheduled at a fixed apply hour — they walk Ready rows when they can. The cap exists so a weekday apply-walk is **about 20–80 minutes** for 10 Ready, as an **estimate**, versus **about 12–20 hours** to do those same ten fully manually. See the time comparison in the root [README](../README.md) (labeled estimates, not a timed study).

## What the schedule does not do

- Does not click Submit
- Does not solve captcha
- Does not connect Gmail / Drive
- Does not complete 2FA on the agent computer
- Does not auto-handle recruiter inbound
- Does not raise the cap because "there were good jobs after 10"
