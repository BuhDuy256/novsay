# User dimensions

Catalog of the dimensions that may change how a person uses the product. Format and rules: `_CRITERIA.md` (U-03, U-10). Purpose: help detect use cases and special requirements. This file does not decide scope; `03-use-cases/` does.

**Status: Draft.** Every "What changes" entry and every baseline is `[assumed]` until a recording or a use case confirms it. Dimensions are added or removed as evidence appears.

**Gap check last run:** not run yet.

How to read the table:
- **Baseline** is the value the product can assume without special handling. Segments do not list it, and it needs no coverage. It is not always at one end: stakes, time pressure, domain knowledge, craft, AI literacy and budget have a middle baseline between the two extremes. A dash means the dimension is categorical and has no baseline.
- **Bold** values are the extremes of a spectrum. A *(categorical)* dimension has no spectrum, so every listed value counts as an extreme and none is bold.
- "What changes" names the kind of use case or requirement the dimension affects. It is a pointer for discovery, not a requirement.
- "Covered by" is written `value: USR-xxx`, one entry per non-baseline value that a segment claims in its frontmatter (or, for knowledge, in its Knowledge section).
- "Gap note" lists the non-baseline values no segment claims yet, and what kind of person would hold them. A gap is a discovery task, not a decision to exclude anyone.

<!-- One row per dimension. Groups follow the segment template: need, knowledge, context, constraint.
     Dimension: a short name, in plain English. Its key in the segment frontmatter is the snake_case form.
     Baseline: the value assumed without special handling, or "-" for a categorical dimension.
     Values: every value, separated by " · ". Wrap the extremes of a spectrum in **bold**.
     What changes: required; the kind of use case or requirement affected (U-03). Remove a dimension that changes nothing.
     Covered by: non-baseline values with the segments that claim them, as "value: USR-xxx".
     Gap note: filled only for a non-baseline value with no segment yet (U-10). Delete the row examples below once real rows exist. -->

| Group | Dimension | Baseline | Values | What changes | Covered by | Gap note |
|---|---|---|---|---|---|---|
| Need | "" *(categorical)* | - | "" | "" | "" | "" |
| Need | "" | "" | "" | "" | "" | "" |
| Knowledge | "" | "" | "" | "" | "" | "" |
| Knowledge | Language *(categorical)* | "" | "" | "" | "" | "" |
| Context | "" *(categorical)* | - | "" | "" | "" | "" |
| Context | "" | "" | "" | "" | "" | "" |
| Constraint | "" | "" | "" | "" | "" | "" |

Only the four knowledge kinds in `_CRITERIA.md` section 3 may appear in the Knowledge group.

## Gap check findings (after USR-xxx)

<!-- Run after each batch of segments (U-10). State the count of non-baseline values, the count covered, and each value still uncovered.
     Then note what the gaps mean: missing segment, over-strict baseline, missing dimension, or coverage that rests on one imagined person.
     Remove this section until the first gap check runs. -->

- 

## Proxies, not dimensions

Age, job and similar facts describe people, but they do not change a flow by themselves. Use them to *suggest* dimension values, then confirm the value with evidence. Never assign a value from a proxy alone.

<!-- One row per proxy. "May hint at" names dimensions above; "Caution" states where the hint misleads. -->

| Proxy | May hint at | Caution |
|---|---|---|
| "" | "" | "" |