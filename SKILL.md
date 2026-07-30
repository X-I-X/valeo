# SKILL.md — Tribune × Valeo Resources Website

**Project:** valeo  
**Repo:** https://github.com/X-I-X/valeo  
**Status:** Complete — pending Netlify deployment  
**Built:** 2026-07-30  
**Meeting deadline:** Friday 2026-07-31, 1:00 PM — 1909 Restaurant, West Palm Beach  
**Built by:** HAL (Praecon Senator + direct HAL edits)  
**Session reset safe:** Yes — read this file to resume

---

## Purpose

A single-page HTML demo site built for a live sales meeting. Ryan Poole (Tribune) is presenting to Rob Murphy (Valeo Resources, healthcare staffing firm, WPB FL) on Friday July 31. The site shows Rob exactly what Tribune would build for Valeo's business — his language, his workflows, his pain points — not a generic AI pitch.

This is the same pattern as:
- `tslhg.netlify.app` — student loan firm (design reference, clone this)
- `tribune-health.netlify.app` — Don Dixon O&P pitch (bio format reference)
- `sales-sleuth.netlify.app` — video section style reference

---

## What Was Built

### Single file: `index.html`
Self-contained. All CSS in `<style>`, all JS inline before `</body>`. Uses Alpine.js from CDN (no build step). Fonts: Inter + JetBrains Mono via Google Fonts.

### `netlify.toml`
```toml
[build]
  publish = "."

[[headers]]
  for = "/*"
  [headers.values]
    X-Robots-Tag = "noindex, nofollow"
```

### Deploy target
Netlify — connect `X-I-X/valeo` GitHub repo via Netlify dashboard. Site name: `valeo-tribune`. No CLI token stored — manual dashboard connection required.

---

## Architecture

### Tab system (Alpine.js)
Four tabs driven by `x-data="{ tab: 'overview', scrolled: false }"`:
- **Overview** — main pitch page
- **The Stack** — L1–L4 layer architecture detail
- **Live Terminal** — Valeo Operations Terminal (simulated data)
- **Next Steps** — tribuneinc.com links, about Tribune

Each tab is a `<div x-show="tab === '...'">` block. All content is in one file.

### Header
- Fixed, blur backdrop, scrolled shadow on scroll
- Tribune SVG logo (inline) + "TRIBUNE × VALEO" wordmark
- Sub-line: "Confidential · Prepared for Valeo Resources"
- Logo click: `@click="tab='overview'"` — returns to Overview
- Logo hover: `transform: scale(1.06)` with cubic-bezier spring (matches tribuneinc.com)
- Nav tabs: pill-style, crimson active state
- Header CTA button links to `tribuneinc.com`

---

## Section Map (Overview tab)

| Section | Background | Notes |
|---|---|---|
| Hero | Dark `#0c1018` + video | Animated grid + orbs + floating badges |
| Stat strip | White | 3 stats: 40-60% admin time, 45-90 day fill, $1k/day open seat |
| The Problem | White | 3 cards: Sourcing Grind, Follow-Up, Knowledge walks out |
| Revenue Calculator | Light gray `#f9fafb` | Alpine.js sliders — see below |
| Tribune Revenue Model | **Hidden** `display:none` | Built but hidden — not for this meeting |
| Layer Architecture | White | L1–L4 with numbered connectors |
| Crawl/Walk/Run | Light gray | 3 phase cards |
| Knowledge Intelligence | Light gray | 4 intel insight cards |
| Marcus Video + Quote | Light gray | Two-column: text left, portrait video right |
| Meet the Team | Light gray | Ryan + Jeffrey bios with headshots |
| CTA Band | Crimson gradient | Links to tribuneinc.com only — NO Calendly |
| Footer | Dark navy | Confidential notice |

**CRITICAL THEME RULE:** Only these elements are dark:
- `.hero` — dark background
- `.cta-band` — crimson gradient
- `footer` — dark navy
- Terminal card (inside the terminal tab) — rounded dark box
- Everything else is WHITE or `#f9fafb` (light gray alternating)

---

## Key Design Decisions & Why

### No Calendly / No CTAs
This site is for a **meeting that is already happening Friday**. Rob does not need to book a call — Ryan is sitting across from him. All CTAs were replaced with `tribuneinc.com` links. No Calendly, no email links.

### No pricing displayed
Marcus (CEO MaxximusAI, Tribune co-presenter) recommended leaving pricing off. The revenue calculator shows ROI upside (placements recovered), not Tribune's fee.

### Revenue Model section hidden (not deleted)
The "How Tribune Gets Paid" section with the performance share slider exists in the HTML at line ~714 with `style="display:none"`. It was built but hidden because:
- The 25% recovery share model is healthcare denial-specific, doesn't map cleanly to recruiting fees
- Pricing conversation belongs in the room, not on the website
- To restore: remove `style="display:none"` from that section

### White theme throughout
TSLHG reference site is white-body with dark accent sections. Multiple iterations were required to enforce this. The final rule: **only hero, terminal card, CTA band, and footer are dark. Everything else is white.**

### Portrait video for Marcus
The Marcus video (`marcus-valeo-tribune-cropped_owuird.mp4`) was shot in portrait orientation. It is embedded as a 9:16 aspect ratio card (260px wide) in the "From Marcus" section, not a widescreen embed.

---

## Content

### About Valeo Resources (verified from their site)
- **Full name:** Valeo Resources
- **Website:** valeoresources.com
- **Phone:** 877-230-7267
- **Address:** 1665 Palm Beach Lakes Blvd, Ste 1003, West Palm Beach, FL 33401
- **Founded:** 2012
- **Tagline:** "Experts in Health Care Talent Acquisition"
- **Services:** Direct Hire, RPO, Project-Based Contracts, Recruiter On Demand, Recruiter On Demand for BH Organizations

### The 4-Agent Stack (L1–L4)
| Layer | Name | What it does |
|---|---|---|
| L1 | Pipeline Execution Layer | Candidate outreach sequences (Day 1/3/7/14), interview reminders, weekly client updates, reactivation |
| L2 | Recruiter Intelligence Layer | Morning briefings, at-risk alerts, candidate scoring, call prep |
| L3 | Talent Intelligence Layer | 20yr placement pattern intelligence, market signals, knowledge capture |
| L4 | BD + Strategy Layer | New BH clinic signal detection, relationship cadence, weekly BD briefing for Rob |

### Key stats used (industry benchmarks)
- 40–60% of recruiter time on admin
- 45–90 day time-to-fill for BH clinical roles
- $800–$1,200/day cost of open seat
- 35–40% annual recruiter turnover in staffing

### Revenue Calculator (Alpine.js sliders)
- Recruiters: 1–20, default **5** (labeled "Industry standard")
- Avg placement fee: $5k–$30k, default **$12,000** (labeled "Industry benchmark BH clinical")
- Additional placements/recruiter/month: 1–5, default **2** (labeled "Conservative estimate with automation")
- Output: additional monthly placements, additional monthly revenue, additional annual revenue

---

## Media Assets

### Hero video (recruiting)
- **Source:** Mixkit — "Reviewing a job application" (free commercial license, no attribution required)
- **Cloudinary:** `https://res.cloudinary.com/dthdxjmgb/video/upload/v1785441262/valeo/hero-recruiting-job-interview.mp4`
- **Usage:** Autoplay, muted, loop, behind hero overlay at 0.52 opacity

### Marcus video
- **Source:** Provided by Ryan/Marcus team
- **Cloudinary:** `https://res.cloudinary.com/dthdxjmgb/video/upload/v1785439055/marcus-valeo-tribune-cropped_owuird.mp4`
- **Usage:** Inline portrait card (9:16, 260px), hover to show play/pause + fullscreen controls. Fullscreen opens lightbox modal.

### Bio headshots (from Cloudinary — same as tribune-health)
- **Ryan Poole:** `https://res.cloudinary.com/dthdxjmgb/image/upload/w_144,h_144,c_fill,g_face,f_auto,q_90/v1780947015/don-dixon/ryan-poole-headshot.jpg`
- **Jeffrey R. Reinhold:** `https://res.cloudinary.com/dthdxjmgb/image/upload/w_144,h_144,c_fill,g_face,f_auto,q_90/v1780947015/don-dixon/jeff-reinhold-headshot.png`

### Tribune logo (inline SVG)
```svg
<svg viewBox="0 0 100 112" xmlns="http://www.w3.org/2000/svg">
  <rect x="18" y="10" width="64" height="16" rx="2" fill="#0A0B12"/>
  <polygon points="18,33 46,33 46,86 37,86 18,60" fill="#0A0B12"/>
  <polygon points="54,33 82,33 82,60 63,86 54,86" fill="#0A0B12"/>
  <polygon points="40,90 60,90 50,104" fill="#7A1A5C"/>
</svg>
```

---

## Team Bios

### Ryan Poole
- **Title:** Co-Founder, Tribune Inc.
- **LinkedIn:** https://www.linkedin.com/in/ryan-poole-0b50b9162/
- **Bio starts:** "Ryan is a builder and operator based in West Palm Beach, Florida. AI architect and Agentic AI systems designer..."
- **Source:** tribune-health.netlify.app

### Jeffrey R. Reinhold
- **Title:** Co-Founder, Tribune Inc.
- **LinkedIn:** https://www.linkedin.com/in/jeffrey-reinhold/
- **Bio starts:** "Jeffrey is an AI Systems Architect specializing in Agentic AI..."
- **IMPORTANT:** Always use full name **Jeffrey R. Reinhold** — never "Jeff Reinhold"
- **Source:** tribune-health.netlify.app

---

## CSS Variables (correct values — do not change)

```css
--crimson: #c41e3a;
--crimson-dark: #9e1830;
--crimson-mid: #e03555;
--crimson-bg: #fff0f2;
--navy: #0a0e1a;
--bg: #ffffff;
--bg-soft: #f9fafb;
--bg-card: #ffffff;
--text: #0f172a;
--text-soft: #475569;
--text-dim: #94a3b8;
--border: #e2e8f0;
--border-mid: #cbd5e1;
```

---

## Terminal (Live Terminal tab)

The terminal tab structure:
1. White header section (section-label + headline + sub)
2. White wrapper div
3. Inside: dark rounded card (`background: var(--term-bg)`, `border-radius: 16px`, `box-shadow`)
4. Terminal content inside the dark card
5. White footer section (note + tribuneinc.com link)

**The terminal card itself is dark. Everything surrounding it is white. This was a recurring fix — enforce this structure.**

Four tabs inside the terminal (Alpine.js):
- **Pipeline Overview** — open roles by client with days open, candidate pipeline bar chart
- **Recruiter Dashboard** — daily stats table, at-risk placements
- **BD Intelligence Feed** — new BH clinic signals, Rob's relationship cadence alerts
- **Morning Briefing** — Rob's daily priority list, week stats, BD intel summary

---

## Build Process Notes

### What worked
- HAL direct edits (exec + Python sed) were faster and more reliable than Worker subagents for surgical CSS/text changes
- Fetching full TSLHG HTML source first and saving to `tslhg-source.html` (deleted before commit) gave the Worker the complete CSS to clone
- Cloudinary remote upload (URL-to-URL, no download) for the hero video

### What required multiple iterations (lessons learned)
1. **Dark/white theme confusion** — The initial Worker built a fully dark site. TSLHG is white-body with dark accent sections only. Had to be corrected 3 times. Rule: hero + terminal + CTA bands + footer = dark. Everything else = white.
2. **Section-tinted class** — `section-tinted` applies a dark gradient. "The Problem" and "Knowledge Intelligence" sections were using it. Both should be white/light.
3. **Hardcoded dark bg on slider sections** — Workers added `style="background:#0a0e1a"` inline on slider sections. These had to be removed manually.
4. **Terminal surrounding** — The `<div style="background:var(--term-bg)">` wrapper was wrapping too much. Fixed by restructuring: white outer div → container → dark rounded card (only terminal content inside).
5. **Em-dashes** — Heisenberg requires zero em-dashes (—) outside terminal `<pre>` blocks. Used Python script to catch all occurrences. Replace with: comma, colon, semicolon, or hyphen depending on context.
6. **Ryan bio truncated** — A Worker accidentally truncated Ryan's bio to one sentence. Always verify both bio cards are complete after any team section edit.
7. **Calendly links** — Initially included, then removed entirely per Heisenberg. Site is for a meeting already scheduled — no booking CTAs needed.
8. **Video orientation** — Marcus video is portrait (9:16), not landscape. Use `aspect-ratio: 9/16` and `max-width: 260px`.

### Em-dash rule (permanent)
No em-dashes anywhere outside terminal `<pre>` blocks. Use this Python check:
```python
with open('index.html') as f: lines = f.readlines()
in_pre = False
for i, line in enumerate(lines, 1):
    if '<pre' in line: in_pre = True
    if '</pre>' in line: in_pre = False
    if not in_pre and '\u2014' in line:
        print(i, line.strip()[:100])
```

---

## Git History Summary

| Commit | What |
|---|---|
| f75ee57 | Initial (README only) |
| 48cb911 | Launch: full site built by Praecon Worker |
| 78fe7ea | Revision: dark theme attempt (wrong), video lightbox, bios, terminal |
| a2bf8ad | Restore white base theme (first attempt) |
| 2dab7c0 | White theme + hero recruiting video |
| 6da4824 | Remove all CTAs, Next Steps → tribuneinc.com |
| 927c63c | All sections white/light, hide revenue model, light tab headers |
| ad1fd01 | White terminal wrapper, logo click/hover, Jeffrey R. Reinhold, zero em-dashes |
| 513432f | Marcus video inline two-column portrait layout |
| 55021ae | Restore full Ryan bio, both bios to tribune-health format |
| 3d05984 | Terminal white wrapper fixed properly, portrait video, real headshots |

---

## Outstanding / Next Session

1. **Netlify deploy** — connect `X-I-X/valeo` on Netlify dashboard, name `valeo-tribune`. No token stored, manual step required. Takes 2 minutes.
2. **Revenue Model section** — hidden at `display:none`. Restore if Tribune wants to show it in a future version.
3. **Valeo logo** — currently no Valeo logo in the header, only Tribune. If Rob provides one, add it to the "TRIBUNE × VALEO" header area.
4. **Post-meeting updates** — after Friday's meeting, any live feedback from Rob can be iterated quickly since it's a single HTML file.

---

## Reference Sites

| Site | Purpose |
|---|---|
| https://tslhg.netlify.app/ | **Design reference** — clone this layout/CSS exactly |
| https://tribune-health.netlify.app/ | Bio format + headshot image URLs |
| https://tribuneinc.com | Logo SVG source + about copy + all CTA links point here |
| https://github.com/X-I-X/valeo | This repo |

---

*Skill file written 2026-07-30 by HAL. Session reset after this commit. Read this file at session start to resume the Valeo project.*
