# Old Guard Cannabis Advisors — Project Notes

## What this is
Marketing website for Old Guard Cannabis Advisors LLC (Alex Marzec's cannabis
extraction/operations consulting practice). Two pages, no framework, no build step —
plain HTML/CSS/JS, deployed on Vercel from this GitHub repo.

## File structure (flat on purpose — do not nest into subfolders)
```
index.html              <- main site
portfolio.html          <- photo portfolio page
images/                 <- logo, hero photos used on index.html
portfolio-images/       <- all gallery photos used on portfolio.html
```
Both HTML files reference images with relative paths like `images/logo.webp` and
`portfolio-images/cult-01.jpg` — keep that structure exactly as-is.

## Design system
- **Fonts**: Cinzel (display/headlines), Source Serif 4 (body text), Inter (small
  utility labels/nav/buttons) — all loaded from Google Fonts
- **Palette**: near-black background (`--void: #0c0e09`), antique gold
  (`--gold: #c9a24b`), warm parchment text (`--ink: #e8e4d8`) — full variable list
  at the top of each file's `<style>` block
- **Visual motif**: circular "badge/medallion" treatment for awards/credentials,
  echoing the logo's crest styling — this is the one signature visual idea the
  whole site is built around, keep it consistent if adding new badge-style content

## Key decisions made during this project (don't reverse without asking)
- **No captions on portfolio photos.** The portfolio page is a full-bleed crossfade
  carousel + filmstrip, deliberately with zero text overlaid on any image —
  this was an explicit choice, not an oversight.
- **Never caption or label a photo with "Casa Verde Farms" or "Acreage Holdings /
  NYCANNA"** — both are still-operating companies and Alex asked that photos not
  be tied to them by name. Double Black Cannabis has no such restriction, but as
  of the Experience-section removal below, no employer names appear anywhere on
  the site any more — text included, not just images.
- **No employer/company names anywhere on the site, in text or images.** The
  Record section's ledger rows used to name Acreage Holdings/NYCANNA, Buddies
  Brand, and Casa Verde Farms inline (via a `.place` span) — all removed. Record
  now reads as pure capability/outcome statements ("$16M+ in infrastructure
  directed...") with the employer relationship deliberately omitted, not
  reframed as literal client work (these are real past operating roles, not
  Old Guard advisory engagements — don't claim otherwise, just don't name who
  they were for).
- **Writing voice**: avoid "Alex has..." / "Alex did..." as a repeated sentence
  opener — it reads amateurish. Prefer the practice's voice ("this practice is
  built on...") or restructure to lead with the achievement.
- **StoryBrand framework applied to index.html**: section order is intentionally
  Hero → Services (the offer) → Record → Awards (proof/authority) → Plan (3-step
  "how it works") → About ("The Guide," shortened) → ResinOps callout → Contact.
  This order matters — don't move About back to right after the hero, that was
  the specific problem being fixed. The standalone Experience section (a
  chronological job-history list between About and the ResinOps callout) was
  removed entirely — it read as a résumé and stacked a third authority-proof
  beat (Record, Awards, *and* Experience) past what StoryBrand recommends before
  reaching Plan. Its strongest facts (the $16M+ infrastructure figure, the first-
  in-market Comerg 50L R-134a system, the $20M/adult-use-transition figure) were
  folded into Record's ledger instead — don't re-add a separate Experience
  section without revisiting this reasoning first.

## Contact form
The Contact section (`#contact`) has a real inquiry form (`#inquiry-form`: Name,
Email, State, "what do you need help with") above the direct email/LinkedIn/
Instagram links — both "Start a conversation" CTA buttons anchor straight to
`#inquiry-form`. It submits via a client-side `fetch()` POST to Web3Forms
(`https://api.web3forms.com/submit`) — no backend, matching this site's static
setup. The access key lives in plaintext as a JS const (`WEB3FORMS_ACCESS_KEY`)
— that's intentional, not a leak; Web3Forms is designed to have its key exposed
client-side since there's no server to hide it behind. Free tier is 250
submissions/month, no dashboard account required. `resinops-website` uses the
exact same pattern for its own waitlist form — keep both in sync if this
approach ever changes (e.g. switching form providers).

## Related repos (separate projects, don't confuse)
- `resinops-website` (github.com/amoebicextracts-cell/resinops-website) — the
  ResinOps SaaS marketing site, cross-links to this one but is a fully separate
  repo/codebase.
- `resinops-deploy` — the actual ResinOps application (React/Vite/Supabase), also
  fully separate from this marketing site.

## Deploy
Vercel auto-deploys on every push to `main`. No build step, no environment
variables needed for this repo specifically.

## Workflow notes
- Windows, Command Prompt (not PowerShell)
- Always verify HTML tag balance after any structural edit (opening/closing
  section, div, header, main, figure tags) — this project has previously broken
  from mismatched tags after large edits, worth double-checking before committing
