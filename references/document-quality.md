# Plan document quality — single source of truth

This is the canonical quality bar for the written plan inside the HTML document:
how it reads, which sections it carries, and how open questions are surfaced.
Read it before authoring; do not write the plan from memory.

**The document is a serious technical plan, not marketing.** Write it the way a
strong implementation plan reads: outcome-first, prose-first, self-contained, and
specific. State the objective and what "done" means, the scope and non-goals, the
proposed approach with the key decisions and their rationale, ordered steps that
name real files, symbols, actions, and data shapes, the risks, and a closing
verification step (tests, build, or a checkable behavior). Replace vague prose
with specifics; never ship a step like "make it work." No hero art, gradients,
logos, slogans, value props, or marketing cards unless the user explicitly asks.

**Every plan must stand alone.** Even when revising an existing plan, the output
is a plan to do the work, not a changelog of the conversation. Don't write "as
discussed above", "this revision", "unlike the prior version", or "correction
from the earlier plan". Fold the right decisions into normal objective,
architecture, scope, and roadmap prose. A reviewer who opens the HTML with no
chat history should understand it. State the positive model directly.

**Make abstract plans instantly legible.** If the idea is broad, strategic, or
intended for a third-party reviewer, put one concrete snapshot near the top —
before dense architecture, mode tables, or roadmaps — that says what the user
sees and what changes under the hood. Then put mechanics, data flow, and
implementation detail in later sections.

**Preserve the user's level of abstraction.** A motivating use case is not
automatically the architecture. When the prompt describes a broader framework or
reusable primitive, separate the reusable core from specific apps, providers, or
examples. Use the concrete example to make the plan understandable, then make
clear which parts are core, which are adapters, and which are future examples.

**Pick the right structure for each piece:**

- Plan prose as readable paragraphs and nested lists with real `<strong>`,
  `<em>`, `<code>`, and links.
- A **file map** (indented monospace block or nested list) for multi-file work.
- **Annotated code**: for a load-bearing file, show the real planned shape in a
  styled `<pre><code>` block with a file-path label and short margin/inline notes
  on the lines that actually change. Highlight only the files worth reading;
  never an exhaustive list of every touched file. For a throwaway snippet a plain
  code block is fine.
- **Diffs** with added/removed lines colored, not just `+`/`-`.
- **Diagrams** for two-dimensional architecture, dependency, data-flow, or state
  relationships — only when they clarify something real. Author them as inline
  SVG or CSS box/flex layouts: paired before/after panels, layered diagrams,
  swimlanes, dependency maps, matrices, or grouped regions. Don't default to a
  left-to-right chain; use a line only when the relationship is truly a sequence.
  Keep labels short and non-overlapping. No external diagram libraries.
- **Side-by-side comparisons** (current/target, before/after) as two-column CSS
  layouts with clearly labeled columns.
- **Tables, checklists, and callouts** for scannable structure.

**Open questions live in one section near the bottom.** Surface answerable
unresolved decisions there, each with a recommended default so the user can
approve by exception. That section is the ONLY place that enumerates open
questions — a one-line pointer up top ("a few decisions are still open — see Open
Questions") is fine, but don't reproduce the list earlier. For complex plans,
don't end without an open-question audit: if architecture, scope, UX, data shape,
rollout, or ownership still depends on a choice, either commit to a recommendation
with rationale or add it to the Open Questions section with a recommended default.

**Verification must exercise the real workflow.** The final verification section
should go beyond typecheck/unit tests when the plan changes UI, local files,
sync, providers, browser behavior, or multi-app flows. Include at least one
end-to-end smoke that matches the user journey, and name the command or manual
path when known.

**Before handoff, sanity-check the rendered HTML.** Open the file and check for
overlap, clipped content, poor contrast, broken collapsible sections, or
unreadable diagrams before asking for approval.
