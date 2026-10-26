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

## 2026-10-26: the decision maker is the founder, before launch

- Decision. The model informs my decision, as FirstHarbor's founder, whether to build intake risk screening and where to set its default threshold. It does not assign real clients, because FirstHarbor has none yet.
- Why. The proposal as first pushed described FirstHarbor assigning clients to monitoring levels, which does not happen yet. Whether to build the feature is the decision I am actually making now.
- Alternative. A generic counselor at any practice deciding whom to check in with more often in the first weeks. It does not depend on FirstHarbor, but the person who acts would be hypothetical.
- Revisit. If FirstHarbor signs pilot counselors before December, they become the decision makers, and their own estimates of r replace mine.

## 2026-10-26: a range for the cost ratio r, from published costs

- Decision. Report the decision across r from 10 to 300, where r is the cost of a missed at-risk client in units of one unneeded week of close monitoring. Sources and arithmetic are in `REFERENCES.md`.
- Why. r = (events prevented per client monitored × cost per event) / (cost of one week of close monitoring). Follow-up care prevented about 2.3 suicidal-behavior events per 100 people (Stanley et al. 2018). A nonfatal attempt costs about $13,300, and an event averages about $137,000 once deaths are counted (Shepard et al. 2016, 2013 dollars, scaled by about 1.34 to 2024). A week of close monitoring costs $14 to $28 (BLS counselor wage × an assumed 30 to 60 minutes). That gives r of about 14 to 28 counting attempts only, and about 150 to 300 counting deaths.
- Alternative. A single value of r, which hides how much the threshold depends on it. Asking counselors how many low-risk clients they would watch to catch one at-risk client measures r more directly, and is still planned.
- Revisit. If counselors' answers fall outside 10 to 300, or the model beats the baseline only over part of the range, the talk says which r the decision depends on.
