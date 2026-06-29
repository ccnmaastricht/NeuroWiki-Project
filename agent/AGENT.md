# AGENT.md

Read this file at the start of every session, regardless of which workflow you are running.
After reading this file, read the module file for the current task (all module files live alongside this file in `agent/`).

---

## 1. Project Identity

This file is the identity and rule layer for one specific project wiki. Each project or research line gets its own copy of this template repository with its own `AGENT.md`.

```
Project name:             
Main research question:   
Model type(s):            
Theories:                 
Brain region(s):          
Organism / data type:     
Key phenomena to explain: 
  - 
Project-specific glossary: 
Contributors:             
```

---

## 2. Repository Structure

```
project-root/
├── README.md             ← human-facing project overview
├── CLAUDE.md             ← Claude Code bootstrap (auto-read on launch)
├── AGENTS.md             ← OpenAI Codex bootstrap
├── CURSOR.md             ← Cursor bootstrap
├── GEMINI.md             ← Gemini CLI bootstrap
├── agent/                ← agent instruction files
│   ├── AGENT.md          ← read first, every session (this file)
│   ├── TEMPLATES.md      ← page templates, index structure, conflict resolution, citation rules
│   ├── INGESTION.md      ← workflow: processing new PDFs
│   ├── REVIEW.md         ← workflow: agent-assisted flag resolution
│   ├── REFINE_A.md       ← workflow: structural harmonization
│   ├── REFINE_B.md       ← workflow: depth audit
│   └── REFINE_C.md       ← workflow: cross-link audit
├── docs/                 ← human-facing documentation
│   ├── QUICKSTART.md     ← setup and usage guide
│   ├── VERIFICATION.md   ← verification protocol
│   └── CONTRIBUTING.md   ← lab wiki submission guide
├── scripts/              ← tools
│   ├── validate.py       ← pre-submission structural validator
│   └── setup.sh          ← one-command project initialization
├── raw/                  ← source PDFs; never modified by agent
│   └── *.pdf
└── wiki/
    ├── primary.bib       ← BibTeX: papers with PDFs in raw/
    ├── secondary.bib     ← BibTeX: papers cited within PDFs but not in raw/
    ├── log.md            ← human verification log
    ├── index.md          ← wiki root index; agent navigation entry point
    └── pages/
        └── <TYPE>_<slug>.md
```

---

## 3. Page Types

There are no per-paper pages. Papers are sources synthesized into concept pages. The `.bib` files are the citation layer.

| Prefix | Type | Covers |
|--------|------|--------|
| `PHE_` | Phenomenon / empirical finding | An observed neural or behavioral regularity |
| `MOD_` | Model | A computational or mathematical model that represents a target system and makes claims about it |
| `MET_` | Method | An analysis method, algorithm, or empirical technique that operates on data to extract or transform information |
| `THE_` | Neuroscientific theory | A full theory that provides explanatory schema for models and has explanatory scope over phenomena |
| `REG_` | Brain region or cell type | Anatomy, physiology, connectivity of a region or cell class |
| `PAR_` | Experimental paradigm or dataset | A task, recording protocol, or canonical dataset |

Slug convention: lowercase, hyphenated, descriptive.
Examples: `PHE_place-cell-remapping`, `MOD_ring-attractor`, `REG_v1-layer4`, `PAR_morris-water-maze`

Full page templates, `wiki/index.md` structure, conflict resolution rules, and citation integrity rules: see `agent/TEMPLATES.md`.

---

## 4. Citation Model

| Notation | Meaning | Source |
|----------|---------|--------|
| `(@OKeefe1971)` | Verified from a PDF in `raw/` | `primary.bib` |
| `(@Buzsaki2015†)` | Reconstructed from another paper's citation | `secondary.bib` |

The `†` dagger is never optional. Omitting it on a secondary citation misrepresents the reliability of a claim.

Citation key format: `AuthorYYYY`. Collisions: `Buzsaki2015a`, `Buzsaki2015b`.
Keys are stable across promotion: `(@Key†)` becomes `(@Key)` — the key itself does not change.

**primary.bib** — one entry per PDF in `raw/`. All fields verified against the PDF. Required field:
```
annote = {<one-line description of main contribution>}
```

**secondary.bib** — reconstructed from citations within PDFs. Uncertain fields flagged:
```
note = {reconstructed from @SourceKey}
```

---

## 5. Confidence Levels and Theory Status

### Confidence (PHE_, MOD_, REG_ pages)

Every `PHE_`, `MOD_`, and `REG_` page must carry a confidence field. Default to `speculative` when evidence is thin.

| Level | Meaning |
|-------|---------|
| `established` | Replicated across multiple independent labs, species, or methods; field consensus. Requires at minimum two independent sources. |
| `debated` | Genuine disagreement in the literature; conflicting evidence or interpretations exist |
| `speculative` | Based on limited evidence, a single study, or theoretical inference without strong empirical grounding |

Confidence upgrades and downgrades both require a note in the page's **Controversies** section citing the evidence that motivated the change.

> **Note**: `speculative` reflects thin evidence, not design purpose. A MOD_ page with `explanatory_role: how-possibly` is not speculative by default — how-possibly models are legitimate epistemic stages regardless of evidence quality. Distinguish evidence quality (confidence field) from explanatory status (`explanatory_role` field and **Explanatory Scope** section).

### Status (THE_ pages)

`THE_` pages do not carry a confidence or quality rating. Instead they carry a neutral **Status** field describing the theory's current standing in the field.

| Status | Meaning |
|--------|---------|
| `active-research-area` | The theory is actively developed, debated, and applied in current research |
| `settled` | The theory is broadly accepted; major disputes resolved; still used but no longer a frontier |
| `abandoned` | The theory has been superseded or discredited and is no longer actively pursued |

---

## 6. Behavioral Rules

1. Read AGENT.md first, then the module file, before any file operation.
2. Never modify files in `raw/`.
3. Never fabricate citations. Unresolvable secondary references: `<!-- UNRESOLVED: <description> -->`.
4. The `†` dagger is mandatory on every secondary citation.
5. Equations before prose on all MOD_ pages.
6. PHE_ and REG_ pages describe observations. MOD_ pages describe proposals. Never conflate.
7. Confidence is mandatory on every PHE_, MOD_, and REG_ page.
8. Cross-link using `[[TYPE_slug]]` within page bodies. Use relative paths in `index.md`.
9. Flag uncertainty with `> ⚠️ Uncertain: <reason>`.
10. Rewrite, don't append. Git history is the changelog.
11. Promotions are content reviews, not find-and-replace. Re-evaluate every claim previously citing the secondary source against the actual PDF.
12. End every session by appending a log entry to `wiki/log.md` using the format in Section 7, then printing the entry to the conversation. The final line of every entry must be `**Sign-off**: *(pending)*` — the human replaces this with `**Sign-off**: ✓ Verified — <name>, <date>` after completing the checklist in `docs/VERIFICATION.md`.
13. Every MOD_ page must populate `explanatory_role` in the frontmatter and the **Explanatory Scope** section in the body. State the level-relative explanatory status explicitly — phenomenological at one level and mechanistic at another are not contradictory and both must appear.

---

## 7. Session Log

Every session ends by appending a new entry to `wiki/log.md`, directly after the opening `---` separator (newest entry first). Print the entry to the conversation as well.

Each workflow file specifies what goes in the **Changes** section; everything else is standard across all session types.

```markdown
## Session YYYY-MM-DD — <Ingestion: filename.pdf | Structural Harmonization | Depth Audit | Cross-Link Audit | Review: session-date>

**Run by**: <name or "agent">

### Changes

<session-specific content — see workflow file for exact fields>

### Flags raised
- ⚑ Human review: <page — issue, or "none">
- `<!-- UNCITED -->`: <page — claim summary, or "none">
- `<!-- UNRESOLVED -->`: <description, or "none">

### Flags resolved this session
- <list, or "none">

### Action items
- <list, or "none">

**Sign-off**: *(pending)*
```

The human replaces `*(pending)*` with `✓ Verified — <name>, <date>` after completing the post-session checklist in `docs/VERIFICATION.md`. The CI validator rejects lab wiki submissions that contain any `*(pending)*` entry.
