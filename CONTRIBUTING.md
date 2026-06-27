# Contributing to a Lab Wiki

A lab wiki is a lab-level knowledge base that merges multiple NeuroWiki project wikis into a unified synthesis. It is maintained by a lab or group and built from project-level wikis submitted by individual researchers, synthesized by LLM agents following a strict provenance and quality protocol.

---

## What You Are Contributing

You are submitting a project-level wiki — a folder of structured markdown pages covering phenomena, models, theories, brain regions, and experimental paradigms relevant to your research. Your pages will be synthesized into the lab wiki, enriching shared pages where your evidence overlaps with existing content and creating new pages where it does not.

Your original citation keys are preserved. You are credited in the `provenance` field of every page you contribute to.

---

## Before You Submit

Run the following in your project root and confirm all pass:

```bash
# 1. Structural harmonization — fixes formatting, does not touch content
# Run: REFINE_A ingestion session (see QUICKSTART.md)

# 2. Depth audit — identifies thin pages (review report, not a blocker)
# Run: REFINE_B ingestion session

# 3. Cross-link audit — ensures pages link correctly
# Run: REFINE_C ingestion session

# 4. Validation script — catches structural errors before submission
python3 validate.py --source wiki/ --report pre-submission-check.json
# Submission requires zero errors in the report.
```

Your `wiki/log.md` must contain at least one verified session entry (signed off by a human who checked claims against source PDFs). The log is submitted alongside your wiki as evidence of internal review.

---

## Submission Process

1. **Fork** your lab wiki repository on GitHub
2. **Copy** your `wiki/pages/` folder into `submissions/<YourName>/`
3. **Copy** your `wiki/primary.bib` and `wiki/secondary.bib` into the same folder
4. **Copy** your `wiki/log.md` into the same folder
5. **Open a Pull Request** with the title: `Submission: <Name> — <brief topic description>`
6. **Complete the PR checklist** (appears automatically from `.github/PULL_REQUEST_TEMPLATE.md`)

---

## PR Checklist

The following is checked automatically by CI and must also be confirmed by you:

- [ ] All pages pass structural validation (`validate.py` exits with code 0)
- [ ] All pages have complete YAML frontmatter (no `<!-- MISSING -->` fields)
- [ ] No page consists entirely of stubs
- [ ] `log.md` contains at least one signed verification entry
- [ ] No page uses `PAP_` citation prefix (deprecated)
- [ ] All `†` secondary citations have corresponding entries in `secondary.bib`

---

## What Happens After Submission

1. CI runs the hub's validation and merge scripts automatically. Structural errors block the PR
2. A community reviewer (rotating maintainer) reviews the merge report and spot-checks a sample of claims
3. The agent synthesizes your pages into the lab wiki on a branch
4. The reviewer approves the branch and merges

Turnaround target: 2 weeks. You will be tagged on the PR if clarification is needed.

---

## Confidence Levels in the Community Wiki

Community confidence is more conservative than project-level confidence:

| Community level | Requires |
|-----------------|----------|
| `established` | Two or more independent lab submissions supporting the same claim |
| `debated` | Conflicting claims across submissions, or one submission with debated status |
| `speculative` | Single submission, or thin evidence noted in source project |

Your submission will not be rejected for having `speculative` pages. The lab wiki explicitly tracks the state of knowledge including what is uncertain.

---

## Questions and Corrections

Open a GitHub Issue for:
- Factual errors you find in community pages
- Requests to add your lab as a maintainer
- Questions about the submission process

Do not edit community pages directly — all updates flow through project wiki submissions.
