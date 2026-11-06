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

## 2026-10-26: widen the range for r after reading Stanley et al. 2018

- Decision. Report the decision across r from 2 to 500, replacing 10 to 300.
- Why. The full paper gives an odds ratio of 0.56 with a 95% CI of 0.33 to 0.95, so the events prevented per 100 people range from 0.25 to 3.5, not just 2.3. Recomputed r: attempts only, 2 to 3 at the weak end of the CI, 14 to 29 at the estimate, and 22 to 44 at the strong end. Deaths included, 16 to 33, 148 to 296, and 228 to 456. The paper also found that the number of follow-up calls did not predict the outcome, so the effect may belong to the safety plan more than to monitoring. That pushes r toward the low end.
- Alternative. Keep 10 to 300, which drops the low end that the paper's own confidence interval allows.
- Revisit. If counselors' estimates cluster in a narrow band, report that band as the main result and the wide range as the sensitivity check.

## 2026-11-06: train on 2022, test on 2023, check on 2024; drop 2021

- Decision. Fit on adults (`CATAG6` 2 to 6) in mental-health treatment in 2022, and score the held-out loss on 2023. Score the same fitted model, unchanged, on 2024 as a second check. Drop 2021. "In treatment" is `MHTRTPY == 1` in 2022 and 2023, and `MHTRTPY2 == 1` in 2024. The outcome is `IRSUICTHNK == 1`. No random draw, so no seed: the split is by survey year.
- Why. The treatment questions changed twice. SAMHSA redesigned them for 2022 and says 2022 estimates "should not be compared with estimates from 2021." In June 2024 it added "for mental health, emotions, or behavior" to every inpatient and outpatient location, and says 2024 treatment estimates "are not comparable with those from 2022 and 2023" (2024 Methodological Summary and Definitions, §3.4.10, pp. 90–91). 2022 and 2023 are the only adjacent years with one definition, so the 2023 score measures the model and not a definition change. 2022 is large enough: 11,978 adults in treatment, 2,014 with serious suicidal thoughts. The 2024 check shows how much the score falls when the population shifts, which FirstHarbor will face, since its clients are not NSDUH respondents. The public 2024 file has no interview month, so the January–May (old wording) and June–December (new wording) respondents cannot be separated.
- Alternative. Train on 2021–2023 and hold out 2024, the plan of 2026-10-26. It has three times the training data and tests on the newest year. But it pools three treatment definitions, and the held-out score would mix model error with the 2024 wording change. Also rejected: train on 2022–2023 and hold out 2024 (one definition in training, but the test still mixes the two). Also rejected: define treatment only by its parts SAMHSA says stay comparable (prescription medication, telehealth). That would give one definition through 2024, but it drops in-person outpatient therapy, which is where FirstHarbor's clients are.
- Revisit. If the loss on 2024 is much worse than on 2023, the model does not hold up under shift, and the 2024 number, not the 2023 one, drives the build decision. If SAMHSA publishes a bridge between the 2023 and 2024 definitions, or a public file with interview month, reconsider using 2024 for training.
