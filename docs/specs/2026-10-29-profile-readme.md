# Spec: GitHub profile README (MrBolas/MrBolas)

Status: implemented 2026-10-29
Date: 2026-10-29
Depends on: `2026-10-29-cv-site.md` (the site is the source of truth)

## Problem

There is no `MrBolas/MrBolas` repo, so the top of `github.com/MrBolas` shows nothing but
pinned repos. The profile is the highest-traffic surface and it currently has no
signpost to the CV site or to what João actually does.

## Goal

A public repo named exactly `MrBolas`, with a root `README.md` that renders above the
repo list and sends people to the CV site. Short enough to read in one screen.

## Non-goals

- Not a second CV. No work history, no education, no dates, no tech-stack dump.
- No duplicated project list — the site owns that fact.
- No third-party badge cards (github-readme-stats, streak counters, trophy widgets).
  They add a network dependency, break silently, and read as decoration over substance.
- No auto-generated contribution art of any kind — heatmap, snake, or graph. *(Revised
  2026-10-29 after trying it: GitHub already renders the contribution calendar a few
  hundred pixels below the README, so a heatmap restates the same data in a second format.
  A self-hosted version was built and then removed for exactly this reason.)*

## Content

Six elements, in order:

1. **Name line** — `João André Bolas Soares`
2. **Now-line** — what the work is today: role, employer, stack. The one fact the
   contribution graph cannot express. Bold label, single line.
3. **One-liner** — what he builds, in a sentence. Different job from the now-line: the
   now-line is a position, this is a description.
4. **Three focus bullets** — backend & distributed systems, AI agentic workflows and DevX,
   infrastructure.
5. **Primary CTA** — `→ [My experience](https://mrbolas.github.io)` — visually the loudest
   thing in the file. Not "Full CV": it should read as a section of a page, not a download.
6. **Elsewhere** — LinkedIn, email, GitHub, matching the CV site exactly.

No image. The header is typography, not artwork.

## Decisions

| Decision | Choice | Why |
|---|---|---|
| Link target | Absolute `https://mrbolas.github.io` | Relative links don't work across repos. |
| Badges | None | A CV site's credibility comes from verified repos, not shields. |
| Length | ≤ 20 lines of markdown | Anything longer stops being a teaser and starts drifting from the site. |
| Repo description | "Profile README" | Discoverable, honest. |
| Freshness | Must reference the site, never restate it | Single source of truth. |
| Header image | None — a bold now-line instead | Anything data-driven either duplicates GitHub's own contribution graph or advertises weak numbers (14 stars, zero releases, most public repos dormant since 2023). |
| CTA wording | "My experience" | Reads as a section of a page; "Full CV" reads as a file download. |
| Years of experience | Written as a phrase, not a number that must be maintained | Avoids a yearly drift bug for a fact the experience section already dates. |

## Requirements

- R1 — Repo is public and named `MrBolas`; `README.md` at root.
- R2 — Renders correctly on the profile page (GitHub-flavoured markdown, no HTML that
  GitHub sanitises away).
- R3 — All four links work: site, LinkedIn, email, GitHub-adjacent.
- R4 — Contact details byte-identical to the CV site. Divergence here is the drift bug.
- R5 — No facts that aren't also on the site (R5 is the enforcement rule for "teaser").
- R6 — Readable in GitHub's light and dark themes (markdown only, so this follows from
  avoiding hardcoded colours entirely).
- R7 — The now-line names the current employer, which must match the newest entry on the
  site's experience section.

## Inputs required from João

1. Confirm the three focus bullets. Proposed: backend & distributed systems, AI agentic
   workflows and DevX tooling, homelab/infrastructure.
2. Preferred tone: plain professional, or lightly playful (the existing site leans playful
   with the emoji header).
3. One flourish: yes/no, and if yes, what.

**Resolved:** LinkedIn `linkedin.com/in/jbsoares21`, email `jbolasoares21@gmail.com`,
site `https://mrbolas.github.io`.

## Acceptance criteria

- `https://github.com/MrBolas` shows the README above the pinned repos.
- Every factual statement in the README also appears on `mrbolas.github.io`.
- Readable without horizontal scroll on a narrow mobile viewport.
- Whole file under 20 lines of markdown.

## Verification

- Load the profile page logged out.
- Diff the contact details against `index.html` by eye and by `grep`.
- Check light and dark theme rendering.
