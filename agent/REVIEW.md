# REVIEW.md — Agent-Assisted Review Session

```
Read agent/AGENT.md fully, then read agent/REVIEW.md fully.
Run a Review Session. Follow agent/REVIEW.md exactly.
```

---

## Purpose

This workflow leads the human through all open flags in one unsigned session. The human makes every resolution decision; the agent presents, applies, and records. Spot-checks remain the human's responsibility (see `docs/VERIFICATION.md`).

---

## Rules

- Apply each resolution immediately — do not batch changes.
- Only modify the relevant Controversies entry and flag when resolving a ⚑ flag. Do not rewrite surrounding page content.
- Never resolve a flag on the agent's own judgment. Every resolution requires explicit human input.
- Present one item at a time. Wait for the human's response before moving to the next.
- Never modify files in `raw/`.

---

## Step R1 — Identify the Target Session

Read `wiki/log.md`. Find all entries with `**Sign-off**: *(pending)*`.

- **None found**: report "No unsigned sessions found." Stop.
- **One found**: announce it (date and session type) and proceed.
- **Multiple found**: list them with their dates and types. Ask the human which to review. Proceed with the chosen session.

---

## Step R2 — Collect Open Flags

Read the target session's log entry. Collect all items listed under **Flags raised** that have not been listed under **Flags resolved this session**.

For each ⚑ flag: read the flagged page and locate the corresponding Controversies entry.

Build a working list in this order:

1. ⚑ Human review flags (synchronous dialog — Step R3)
2. `<!-- UNCITED -->` flags (sequential — Step R4)
3. `<!-- UNRESOLVED -->` flags (sequential — Step R5)

If the working list is empty, skip to Step R6.

Report to the human: "Found N flag(s): [summary list]. Working through them now."

---

## Step R3 — Resolve ⚑ Flags (Synchronous)

For each ⚑ flag, one at a time:

**Present:**

```
⚑ CONFLICT — <page title> (<TYPE_slug>)

<Paste the full Controversies entry verbatim, including both positions, citations, possible resolution, and current status.>

How would you like to resolve this?
  A) Accept Position A
  B) Accept Position B
  C) Mark as partially resolved — I'll provide a note
  D) Leave open — return to this later
```

**Apply immediately based on human response:**

| Response | Action |
|----------|--------|
| A or B | Update the Controversies entry: set `Status: resolved`, record which position was accepted and why (use the human's words). Remove `> ⚑ **Human review required**: ...` from the page header. If the resolution changes confidence, update the frontmatter field and add a note in Controversies. |
| C | Update the Controversies entry with the human's note and the partial resolution. Set `Status: partially resolved`. Remove the page header flag. |
| D | Leave the page unchanged. Record this flag as still open. |

After applying, confirm: "Done — [describe change made, or 'flag left open']. Moving to next item."

---

## Step R4 — Address UNCITED Flags (Sequential)

For each `<!-- UNCITED: <claim summary> -->` flag, one at a time:

**Present:**

```
UNCITED — <page title>
Claim: <claim summary from the flag comment>

Do you know the source for this claim?
  Y) Yes — provide the citation key (existing key, or I'll add a new secondary.bib entry)
  N) No — leave for the next ingestion session
```

**Apply immediately:**

| Response | Action |
|----------|--------|
| Y | Add the citation inline. If the key is not in either `.bib` file, add a reconstructed entry to `secondary.bib` with `note = {reconstructed from human review, YYYY-MM-DD}`. Remove the `<!-- UNCITED -->` comment. |
| N | Leave the flag. Record as still open. |

---

## Step R5 — Address UNRESOLVED Flags (Sequential)

For each `<!-- UNRESOLVED: <description> -->` flag, one at a time:

**Present:**

```
UNRESOLVED — <description from the flag comment>

This secondary citation could not be reconstructed during ingestion.
  A) Add the PDF to raw/ in the next ingestion session (I'll note it as a priority)
  P) Peripheral — leave as-is for now
```

**Apply:**

No page changes are made here regardless of response. Record the human's decision in the review session's Action items list (built up during this workflow and written in Step R6).

---

## Step R6 — Write Session Log Entry and Sign Off

**Write the review session log entry** — append to `wiki/log.md` (newest first) using the canonical format from AGENT.md Section 11:

For the **Changes** section, include:

```
- Target session: <original session date and type>
- ⚑ flags: N resolved of M total
- UNCITED flags: N resolved of M total
- UNRESOLVED flags: N noted of M total
```

Under **Flags resolved this session**, list each item that was resolved with a one-line description of the resolution.

Under **Action items**, list any UNRESOLVED flags the human decided to address in the next ingestion session.

If any flags remain open, add a **Flags remaining open** subsection (between **Flags resolved** and **Action items**) listing each unresolved item and why it was left open.

The review session log entry is signed immediately — the human is present:

```
**Sign-off**: ✓ Verified — <name>, <date>
```

**Sign off the original session** if and only if all flags from that session are now resolved (either resolved this session or were previously resolved). Edit the original log entry in `wiki/log.md`:

```
**Sign-off**: ✓ Verified — <name>, <date>
```

If flags remain open, leave the original session's `*(pending)*` in place. Report: "Original session [date] remains unsigned — N flag(s) still open. Re-run REVIEW when ready."
