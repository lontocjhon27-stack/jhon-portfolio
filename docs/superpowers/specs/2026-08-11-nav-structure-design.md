# Site-wide Navigation & Structure

## Problem

1. **Mobile nav gap, not a full break.** Phones (≤768px) already have a working hamburger (`#hamBtn` → `.mob-nav` dropdown). But `.nav-links{display:none}` kicks in at 900px while `.ham{display:flex}` only kicks in at 768px — leaving a 769–900px gap (tablets, small laptop windows) with no nav visible at all. Corrected after live-testing at 375px (hamburger works) and 820px (both hidden).
2. **Long, hard-to-scan homepage.** ~8 major sections stacked with no way to jump directly to one (Work, Services, Results, Process, About, Reviews, Contact).
3. **Duplicate "Tools" section.** Two sections share the same heading ("The stack I build, connect, and run."): `#proficiency-tools` (4 tool screenshots, unnumbered, appears early) and `#tools` (categorized text list, numbered "04", appears later). Reads as a copy-paste repeat.

## Design

### 1. Close the mobile nav gap
- One-line fix: change `@media(max-width:768px){.ham{display:flex}}` to `900px`, matching `.nav-links{display:none}`'s breakpoint.
- No new component — the existing hamburger + `.mob-nav` dropdown now simply appears exactly when the desktop links disappear, closing the gap.

### 2. Quick-link chip strip
- A horizontally-scrollable row of pill links, reusable as one small component.
- Homepage: placed right under the hero (`#cover`), links to `#ghl` (Services), `#case` (Results), `#strategy` (Process), `#about` (About), `#why` (Reviews), `#contact` (Contact), plus `#showreel` (Work).
- Campaign page: placed right under the campaign hero, links to the ad-creative block, `#campaign` funnel carousel, the live opt-in page preview, the proof-screenshots block, and the final result-stats grid. New `id`s are added to those blocks since they don't currently have anchors.
- Plain anchor links with smooth-scroll (CSS `scroll-behavior:smooth` already likely acceptable, or a small scroll handler if not present) — no new state, no build step.
- No existing section is removed, reordered, or rewritten — this only adds a way to jump to what's already there.

### 3. Tools section merge
- Delete the standalone `#proficiency-tools` section (screenshots-only, unnumbered).
- Fold its 4 tool screenshots (Zapier, WordPress, Skool, GHL) into the numbered `#tools` section ("04 · Tools proficiency"), above or alongside the existing categorized list, so there is exactly one "Tools" section with both the visual proof and the full categorized list.
- No other section references `#proficiency-tools`, so this is a safe removal.

## Out of scope

- Campaign weekly-tracker rebuild (separate design, not started).
- Any content reordering/removal beyond the tools-section merge.
- Desktop nav changes.

## Verification

- Load at mobile width (375px) and desktop width (1280px) in the browser preview.
- Confirm bottom tab bar appears only on mobile, links navigate correctly, active state matches current page.
- Confirm chip strips scroll to the right anchors on both homepage and campaign page.
- Confirm only one "Tools" section remains, with screenshots + categorized list both present.
- Check console/network for new 404s introduced by the change.
