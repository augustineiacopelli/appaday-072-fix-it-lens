# Fix-It Lens

**AppADay #072** &middot; Category: Utility (U) &middot; AI-powered

Point your phone at something broken, describe it in a sentence, and Claude reads the photo like a cautious contractor: what it sees, how confident it is, the supplies and tools you'll need, the fix step by step, and the safety flags that actually matter. Answer its follow-up questions and it re-diagnoses from the same photo to tighten the plan.

## What it does

Fix-It Lens is a two-pass repair diagnostic. A single photo almost never contains enough to be certain about a home repair &mdash; it can't tell you whether a wall is drywall or plaster, what's behind it, or how deep the damage runs. So instead of pretending to a confident one-shot answer, the app:

1. **Reads the problem** from your photo and description, and states its confidence honestly.
2. **Plans the fix** &mdash; difficulty, rough time and materials cost, a DIY-or-call-a-pro verdict, a checkable supplies list (essential vs. optional), the tools you'll need, diagnosis checks to run before you buy anything, and the ordered repair steps.
3. **Asks what it can't see.** The two to four questions that would most change the plan render as answerable fields. Fill in what you can, add any other detail you noticed, and hit **Refine the plan** for a second, sharper pass.

A safety layer runs through the whole thing: the model is prompted to flag anything involving electrical, gas, plumbing behind walls, structural members, suspected mold, or asbestos-era materials, and to say plainly when a job belongs with a licensed professional rather than talk a homeowner into dangerous work.

## Sharing a plan

Once a plan is on screen, an actions row gives you four ways to take it with you. **Print / PDF** renders a clean light-themed report (with the photo) through the browser's print dialog, which doubles as save-to-PDF. **Email** opens a pre-filled message with the plan as the body. **Download** saves the plan as a plain-text file. **Copy** puts the full plan on your clipboard. All of them draw from the same report so the contents stay consistent.

## Saving and resuming a job

Repairs rarely get diagnosed and finished in one sitting &mdash; often you need to go measure something, look behind a panel, or wait until the weekend. The folder button in the header opens **Saved jobs**, where you can stash the current job (photo, description, plan, and any answers you've typed) and come back to it later. Resuming restores everything exactly as you left it, including partially answered questions, so you can add the answers you couldn't give before, drop in new information mid-task, and refine from there. A draft saved before diagnosis comes back ready for its first **Diagnose**. Jobs live in `localStorage` on your device; the app keeps the six most recent.

## Using it

Open the &#9881; Settings gear and paste an Anthropic API key (stored only in your browser's `localStorage`, sent straight to Anthropic, never committed or logged). Optionally pick a model &mdash; Sonnet 5 by default, Opus 4.8 for a tricky job, Haiku 4.5 for something simple. Then shoot or choose a photo, describe the problem, and tap **Diagnose**.

On a phone the capture button opens the camera directly, so the real flow is standing in front of the problem, snapping it, and getting a plan.

## How it's built

Single-file vanilla HTML, CSS, and JavaScript. No build step, no dependencies beyond Google Fonts. Direct browser-to-Anthropic API calls using the `anthropic-dangerous-direct-browser-access` header, with a vision request (photo as base64) returning a structured JSON plan that renders into panels. Photos are downscaled to a 1568px long edge on a canvas before upload to keep requests fast and cheap.

Visual identity is a field-inspection instrument: a viewfinder capture frame with a reticle and an amber scan sweep while Claude "looks," results laid out as a structured job ticket. Typeface is the IBM Plex family (Sans, Sans Condensed, Mono) for a technical-documentation feel. Fully responsive with `100dvh` layout, visible focus states, and reduced-motion support.

## Safety note

Fix-It Lens reads a photo, not your house. Every plan is a starting point &mdash; confirm on site, pull permits where required, and call a licensed professional for anything electrical, gas, structural, or hidden behind a wall.

---

Part of [AppADay](https://augustineiacopelli.github.io/appaday/) &mdash; one complete, functional, mobile-friendly web app shipped every day.
