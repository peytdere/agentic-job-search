# Agents

Four specialists on the default path, one coordinator beside them, one optional reviewer off to the side. None of them click Submit.

These are roles, not a dump of live agent configs. No agent identifiers belong in this repo.

## Coordinator

**Owns**

- The output contract: each qualifying role is an apply URL, a resume URL, and a cover-letter URL on the tracker.
- Quality gates and caps (example: $200k posted floor, 60-day freshness, 10 Ready/day, role family, new-only, dedupe).
- Who exists: add or refuse a bot. Prefer a thin specialist over a god-bot.
- Morning kick (~7:00am PT) so generators run on packets the watcher already gated.
- 8:30am PT **shortfall ping only** (Ready under cap). No ping when the cap is met.
- 3:00pm PT **weekday outcome-mail only**. Not a second harvest.
- Routing a packet to the Quality reviewer when a human asks.

**Does not own**

- Writing resumes or cover letters.
- Harvesting Gmail or fetching JDs (Watcher).
- Apply-walk clicks, captcha, file pickers, or **Submit**.
- Recruiter inbound threads.

## Watcher

**Owns**

- Ingest: new job-alert mail (Gmail) and any extra searches it was asked to run. Daily including weekends, toward the Ready cap.
- Parse each card: title, company, location, job id, apply URL, salary if posted, post date if posted, full description after fetch.
- Email cards are not JDs. Follow the link and fetch the posting in Chrome.
- Prefer the employer application page (Greenhouse, Lever, SmartRecruiters, company careers) over a social-network tracking URL.
- Gates and skip log. Dedupe by job id.
- Handoff of a qualifying packet to the resume generator.

**Does not own**

- Writing application materials.
- Changing policy (Coordinator).
- Solving captcha or logging the human into ATS accounts.
- Submit.
- Treating LinkedIn as an API. Alerts are email.

## Resume generator

The generator does not start from a blank page or from the JD's wish list. It starts from a private, verified **source bank** (the **meta-resume** / super-resume): about ten years of real employers, titles, dates, bullets, and metrics. That file is the only fact source. It is never dumped wholesale onto a posting.

**Owns**

- One-page tailored resume as a Google Doc, in the existing format, from that source bank.
- **Select** the subset of real experience that is relevant to this posting (evals vs fleet ops vs director AI platform — pick the slice, not the whole career).
- **Condense** the selected slice to one page: keep, shorten, or drop real bullets.
- **Reword** kept bullets to the posting's language and keywords when the underlying fact is the same (SQL against evaluation logs can be phrased as operational telemetry if that is what actually happened).
- Returning the Doc URL. Echoing the apply URL so the tracker does not drop it.

**Does not own**

- Hunting jobs or deciding skip vs generate (Watcher / Coordinator).
- Inventing employers, dates, titles, tools, or metrics. If the bank cannot support a keyword the JD wants, omit it. Do not hallucinate a Tableau dashboard that was never built.
- Dumping the entire bank onto one page "just in case."
- Cover letters.
- PDF-perfect export. Drive "Download as PDF" can truncate; the human skims when the ATS wants a file.
- Submit.

Tailoring is selection and phrasing. Facts cannot be created.

## Cover letter

The letter is written **after** the tailored resume exists. Inputs are that resume and the JD — not a parallel career story.

**Owns**

- A short letter specific to that posting, grounded in the resume that was just written plus the JD.
- The third tracker link. Status → Ready.

**Does not own**

- Hunting jobs.
- Writing or rewriting the resume. Sequence is resume first, letter second.
- Drafting from a title alone. If JD, resume URL, or apply URL is missing, ask; do not invent.
- Claiming facts that are not on the tailored resume or in the source bank. Same hard ban as the generator: no invented employers, dates, titles, tools, or metrics.
- "I am writing to express my interest." The letter is short and specific.
- Confessing that a model wrote the letter. Do not say "AI wrote this."
- Submit.

For roles that are actually about building AI/eval systems, one sentence about having shipped this pipeline is a **project**, not a disclosure. Skip that sentence on unrelated roles.

## Quality reviewer (optional, off default path)

**Owns**

- A second pass when a human (or the coordinator, on request) sends a packet over.
- Checking: resume facts ⊆ source bank (select / condense / reword, never invent); letter claims ⊆ that resume + JD; one-page intent; apply URL still present.

**Does not own**

- The morning default path. Packets do not wait on this role.
- Tightening or loosening gates.
- Regenerating by default. If something is wrong, say so; do not silently become a fourth writer.
- Submit.

## Shared non-ownership

No agent in this design owns:

- Clicking **Submit** on Greenhouse, Lever, SmartRecruiters, or any other ATS
- Captcha
- Native file pickers
- Gmail / Drive OAuth consent
- Login / 2FA on the persistent agent Linux computer
- Auto-replying to recruiters
- Publishing PII, tracker rows, or connector IDs into git

The human apply-walk (Ready → Applied) is allowed as a **person** using the packet. That walk still must not be delegated as "the agent Submitted it."
