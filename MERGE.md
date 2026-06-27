# MERGE.md — Community Wiki Merge Workflow

```
Read COMMUNITY_AGENT.md fully, then read MERGE.md fully.
Merge the submitted project wiki at <path> into the community wiki.
Follow this workflow exactly. Print the session summary when done.
```

---

## Rules

- The merge script (merge.py) runs first. The agent synthesizes only after the script completes.
- Never overwrite community page content without synthesizing — concatenation is not merging.
- All claims in the community wiki are treated as secondary: citation keys are preserved from the contributing project but no PDFs are held locally.
- Provenance is tracked in YAML frontmatter, not in citation notation.
- The agent never upgrades confidence to `established` based on a single project submission.

---

## Step M1 — Run merge.py

```bash
python3 merge.py --source <path-to-submitted-wiki> --target wiki/ --report merge-report.json
```

Review `merge-report.json` before proceeding. It contains:
- New pages (no matching slug in community wiki)
- Matching pages (slug exists in both — require synthesis)
- Bib conflicts (same key, different metadata)
- Structural errors (pages failing validation in submitted wiki)

Do not proceed if the report contains structural errors. Return the submission with the error list.

---

## Step M2 — Handle New Pages

For each page flagged as new in `merge-report.json`:

1. Copy the page to `wiki/pages/`
2. Update the YAML frontmatter:
   - Add `provenance` field listing the contributing lab and submission date
   - Set confidence to one level below what the submitted page claims, unless two or more independent project wikis already support the same level
   - All citations are implicitly secondary — do not add `†` to notation, but note in frontmatter: `citation_status: unverified`
3. Add the page to `wiki/index.md`

```yaml
# Added provenance fields example:
provenance:
  - lab: HippocampusLab
    submitted: 2025-03-01
    source_confidence: established
citation_status: unverified
```

---

## Step M3 — Synthesize Matching Pages

For each page flagged as matching, the community page and submitted page cover the same concept. Synthesize them:

1. Read both pages in full
2. For each section, identify:
   - **Concordant claims**: same claim, same or compatible citations → retain, add submitting lab to `provenance`
   - **Additive claims**: claim present in submitted page but not community page → add to section with submitting lab citation
   - **Conflicting claims**: direct contradiction → apply conflict resolution rules from COMMUNITY_AGENT.md Section 7; add structured Controversies entry
3. Rewrite the section as a unified synthesis — not a concatenation
4. Update `provenance` in frontmatter to include the new contributing lab
5. Update `confidence` per the community confidence rules (Section 5 of COMMUNITY_AGENT.md)
6. Update `updated` date

---

## Step M4 — Merge .bib Files

All entries from the submitted `primary.bib` are added to the community `references.bib` if not already present. Key conflicts (same key, different metadata): flag in merge report and defer to human reviewer.

The community wiki has one `references.bib` — no primary/secondary split, since no PDFs are held locally. The `citation_status: unverified` frontmatter field on each page serves the equivalent role.

---

## Step M5 — Update community wiki/index.md

Add all new pages. Update `updated` dates for all modified pages.

---

## Step M6 — Session Summary

```
## Merge Session — <submitted wiki> — YYYY-MM-DD

Submitted by: <lab name>
Pages in submission: N

New pages added: N
  <list>

Pages synthesized (matched existing): N
  <list: page — concordant/additive/conflicting claims count>

Conflicts requiring human review (⚑): N
  <page: issue>

Bib conflicts requiring human review: N
  <key: issue>

Confidence adjustments made:
  <page: submitted confidence → community confidence — reason>

Structural errors (submission returned): N
  <list>
```
