# MCEM Forecast Comments for Microsoft Scout

This repository packages a Microsoft Scout installer skill that creates:

1. A personalized `/mcem-forecast-comments` skill for drafting evidence-based opportunity forecast comments.
2. A scheduled Scout automation that runs the skill on the teammate's preferred cadence.
3. A private local opportunity roster, review log, and candidate inbox under the teammate's Scout profile.
4. A weekly automation that checks the exact installation repository for updates.

The workflow is based on the FY27 Federal MCEM pipeline guidance and follows the same thin-automation pattern as the Weekly HVA workflow: the automation invokes the skill, while the detailed standards remain in the skill.

## Install

In Microsoft Scout, provide the GitHub repository URL and say:

> Install the skill from this repository, then run `/mcem-forecast-installer`.

The installer asks for:

- An initial opportunity roster, seeded manually and/or from inferred Microsoft 365 activity
- Confirmation of the source GitHub repository
- Review cadence
- Weekly source-update check cadence
- Evidence lookback window
- Output delivery preference
- Comment length preference
- Optional team-specific terminology

It then creates the runtime skill, forecast-review automation, and source-update automation. The installer does not write to MSX or send customer information to third parties.

The installer is self-contained. If Scout copies the full repository, it uses the maintainable template and reference files. If Scout imports only the root `SKILL.md`, it uses the embedded runtime fallback.

## What the runtime skill does

- Reviews authorized Microsoft 365 evidence from email, calendar, Teams, and files.
- Reviews every active roster opportunity on every scheduled run, even when no recent activity exists.
- Uses the lookback window only to gather new evidence, not to decide which roster entries are reviewed.
- Produces one paste-ready comment per active opportunity.
- Suggests possible new opportunities from inferred activity without adding them automatically.
- Maintains a metadata-only review log and candidate inbox.
- Supports listing, adding, pausing, closing, and reactivating roster entries, plus approving or rejecting inferred candidates.
- Separates verified facts from unknowns.
- Applies conservative MCEM commitment and pipeline-hygiene standards.
- Identifies stale comments, missing evidence, risks, blockers, owners, and due dates.
- Never invents customer commitment, timing, value, budget, resources, or technical feasibility.

## Weekly source updates

The installer records the normalized GitHub repository URL, installed source version, and source `SKILL.md` hash in the teammate's local `install-manifest.json`. A separate weekly automation compares both version and hash with the current repository.

- Unchanged checks remain quiet.
- Version or content changes are reported for review.
- Content changes without a version bump are explicitly flagged.
- Repository content is treated as untrusted data and is never executed.
- Updates are never installed automatically; the teammate reviews changes and reruns installation from the same repository.

## Repository layout

```text
SKILL.md
templates/
  mcem-forecast-comments.SKILL.md
references/
  fy27-mcem-forecast-rubric.md
```

## Source and maintenance

The packaged rubric is a concise derivative checklist, not a copy of the source deck. Maintainers should review the current Federal MCEM guidance at least once per fiscal year and update the rubric version and source date when standards change.

Primary source used for this version:

- `FY27-MCEM-Azure-Pipeline-Walking-Deck.pptx`, Federal MCEM Guides, reviewed August 25, 2026.

## Privacy and safety

- Customer and opportunity data stays within the teammate's authorized Microsoft 365 and Scout context.
- The local roster contains opportunity identifiers and review metadata; the review log does not store full forecast comments or copied message content.
- The installation manifest stores only repository/version/hash metadata.
- Scheduled output should use Scout's private automation result/Teams notification or remain in automation history.
- The skill drafts comments only; users remain responsible for reviewing and entering them in MSX.
- Do not commit customer data, opportunity exports, credentials, or generated comments to this repository.
