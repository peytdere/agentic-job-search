# Human-in-the-loop

The pipeline's job is a **Ready packet**. The human's job is the last mile. These limits are load-bearing. They are not a backlog of automations to finish later.

## Apply-walk vs Submit

**Apply-walk** (human): open a Ready tracker row, open the apply URL, attach the resume / letter, fill leftovers, handle captcha and pickers, click Submit, mark Applied.

**Submit** (human only): the actual application send. Agents may prepare. They may not click it — not on "my" ATS, not on localhost, not in a lab framing.

The Consigliere brief mentions apply-walk so the morning run has a defined consumer. It still forbids Submit.

## Limits

### Captcha

ATS pages (Greenhouse, Lever, SmartRecruiters, and the CDNs in front of them) show captchas. Agents stop. A human solves them. Estimated extra: **0.5–2 min** when present — an estimate, not a measurement.

### Submit is human-only

See above. No specialist brief includes permission to send the application.

### Gmail and Drive connect

Connectors need an OAuth consent screen. That is a person in the browser on first setup (and on re-auth). One-time setup estimate: **30–60 min** together with tracker + source bank + agent-computer login — again an estimate.

### Login / 2FA on the agent computer

The runtime is a persistent Linux computer with Chrome. Sites will ask for password + 2FA. The human does first login (**about 1–3 min per site**, amortized). Agents reuse the session; they do not complete 2FA challenges.

### LinkedIn via email, not API

Job alerts are Gmail messages. There is no LinkedIn jobs API in this stack and no "just scrape LinkedIn" substitute. The watcher parses mail and then fetches the **posting** behind the link. If that fetch lands on a login wall, skip or leave it for a human — do not build a LinkedIn client.

### Greenhouse file picker

Greenhouse (and some Lever / SmartRecruiters flows) opens a native file chooser for resume upload. That dialog is a poor agent surface. The human attaches the Doc/PDF during apply-walk. Do not click randomly through the picker.

### Drive PDF export truncation

Google Docs "Download as PDF" can clip a one-page resume: last bullet, extra blank page, header cut off. The generator writes a one-page **Doc**. If an ATS wants a PDF, the human skims the export (**about 2–5 min** when they bother). Do not treat export as lossless.

### Extra tabs

Apply links spawn cookie banners, sign-in popups, and extra ATS tabs. Agents do not hunt every tab. The human owns the live form. See [architecture.md](architecture.md) failure modes.

### Recruiter inbound is not automated

The same inbox that carries job alerts also carries recruiter mail. This system does not auto-reply, auto-schedule, or scrape those threads into the tracker. Weekday **3:00pm PT outcome-mail** is a cue for the human to look, not a bot that negotiates.

### Skip is success

A skip (no salary, below the example $200k floor, off-target title, duplicate, older than 60 days, missing post date, over the 10 Ready cap) is a completed job. Lowering gates to keep agents busy produces junk packets and a longer last mile.

## What the human still does, every Ready row

Estimates, not a timed study. Typical last mile **2–8 min** per apply:

1. Review the packet (JD vs resume vs letter) — about 1–3 min
2. Optional resume skim — about 2–5 min if you open the PDF
3. First login / 2FA if the ATS session is cold — about 1–3 min
4. Captcha if shown — about 0.5–2 min
5. File picker / leftover fields
6. Submit — about 10 seconds
7. Mark Applied on the tracker

The 10 Ready/day cap exists so this list cannot become another full-time job.
