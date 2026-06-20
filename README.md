# /visual-plan

Turn ordinary implementation plans into a rich, interactive, self-contained HTML
review surface — instead of a flat wall of Markdown rendered in the terminal.

`/visual-plan` takes the plan an agent would normally dump into chat and renders
it as a single `.html` file the user opens in their browser: a sticky header with
the outcome, a table-of-contents nav, collapsible sections, numbered step cards
naming real files, inline SVG/CSS diagrams, annotated code and diffs, a file map,
and an open-questions section with recommended defaults.

It solves for plans that are too important to bury in chat. The output is
scannable and intuitive enough for a human to approve before code changes start.

## How It Works

- **Self-authored, zero dependencies.** The skill writes one HTML file with CSS
  and any JS inlined — no MCP server, no hosted service, no CDN, no web fonts. It
  opens correctly from a `file://` URL offline.
- **Grounded in real code.** Plans name actual repo files, schemas, actions, and
  symbols, and lead with reuse before additions.
- **Right visual where it helps.** Diagrams are inline SVG or clean CSS layouts
  (before/after panels, lanes, matrices) — no external diagram libraries.
- **The plan is the approval gate.** The HTML is surfaced for review and sign-off
  before any source edits begin.

## When To Use It

Use it for multi-file, ambiguous, risky, architecture-heavy, data-heavy, or
UI-heavy work where the wrong direction would be expensive — plus modest work
like a single UI surface with states or a component/API/data-shape decision that
needs alignment. Skip it for trivial fixes whose diff is easier to review than a
plan.

## Output

A single HTML file (default `/tmp/visual-plan-<slug>.html`, or `plans/<slug>.html`
when the user wants it checked into the repo). By default nothing is uploaded —
the file itself is shareable and check-in-able.

When the user wants a **hosted link**, the skill can deploy the HTML to Cloudflare
Workers with a [temporary account](https://blog.cloudflare.com/temporary-accounts/)
via `npx wrangler@latest deploy --temporary` — no Cloudflare signup, login, or API
token needed up front. It returns a live URL plus a claim link that stays valid
for 60 minutes.

## Files

- `SKILL.md` — the skill instructions and HTML authoring contract.
- `references/html-template.md` — copy-pasteable self-contained HTML skeleton.
- `references/document-quality.md` — the written-plan quality bar.
