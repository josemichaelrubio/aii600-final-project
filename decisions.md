# Decisions

This file is the history of the project. Append an entry when a choice changes the work: the quantity, the data, the split, the model, the loss, or the action. Leave old entries in place. A later entry can reverse an earlier one. If a result depends on a random draw, record the seed under Why. The split entry records the cutoff date, or the seed and the fraction. The pull request that merges the code names this entry.

## YYYY-MM-DD: short title

- Decision. What you chose.
- Why. The evidence.
- Alternative. What you rejected.
- Revisit. What would change the choice.

## 2026-10-26: intake risk among adults in treatment, on NSDUH

- Decision. Predict, for adults who received mental-health treatment in the past year, the probability of serious suicidal thoughts in the past year, to set a new FirstHarbor client's starting level of monitoring. Data: NSDUH public-use files, 2021 through the latest year. Hold out the latest year. Baseline: every client starts on the same level.
- Why. FirstHarbor can use the data and the result. The data are federal and free, while research datasets of crisis text are limited to research use or carry Reddit's terms. NSDUH surveys the population FirstHarbor serves, adults in treatment, and asks about suicidal thoughts directly.
- Alternative. A crisis-message classifier trained on the Reddit C-SSRS dataset (Zenodo 4543776, CC BY 4.0). It is closer to FirstHarbor's per-message alert, but the posts are Reddit text, not client messages, and commercial use of Reddit content is uncertain. Also set aside: county targeting with CDC PLACES and HRSA shortage areas (a sales question, not a product one), and therapy dropout with MEPS (variables not yet checked).
- Revisit. If too few adults in treatment report suicidal thoughts for a held-out year to estimate the miss rate, or if FirstHarbor will not ask intake questions like the survey's, switch to the C-SSRS classifier.
