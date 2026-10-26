# Proposal

## Hypothesis

Among adults in mental-health treatment, a few intake answers (age, recent psychological distress, substance use, kind of treatment) identify who is still having serious thoughts of suicide well enough that sorting new clients by predicted risk costs less than treating every new client the same.

The quantity is, for each adult who received mental-health treatment in the past year, the probability that they seriously thought about suicide in the past year. It is scored on a held-out survey year as the expected cost per 100 new clients, in units of one unneeded week of close monitoring (defined below).

## Data

Source: the National Survey on Drug Use and Health (NSDUH) public-use files, published each year by SAMHSA. NSDUH is a national household survey of the U.S. civilian, non-institutionalized population aged 12 and over, answered by computer-assisted interview in person or on the web. The unit of observation is one adult respondent. I will use 2021 through the latest released year. SAMHSA states that 2021 onward cannot be pooled with earlier years because web interviews were added. The number of adults in treatment per year will be counted from the files, not assumed. The survey weights will be used for every population estimate.

What I measure differs from what the decision needs in three ways. First, FirstHarbor clients are people a counselor invited, not a random sample of adults in treatment. Second, the answers cover the past year, while the decision needs current risk at intake, and the survey cannot say whether the suicidal thoughts came before or after treatment began. Third, the answers are self-reported to a survey, and FirstHarbor would ask them in a clinical app, where people may answer differently. The first two are bias, not noise. The public files also remove most geography, so the model cannot use location.

Terms: the SAMHSA data page states no license or redistribution terms. Until I confirm that the files may be republished, they stay off GitHub, and `data/README.md` gives the command that downloads them from SAMHSA.

## Decision affected by the model

Who acts: FirstHarbor, a between-sessions support app in which therapy clients talk to an AI companion, Anchor, and their counselor watches a dashboard. At intake, FirstHarbor assigns each new client a starting level of monitoring: standard, or close (the counselor reviews the first week of conversations and risk alerts fire at a lower level).

What changes: today every new client starts the same. With the model, clients whose predicted risk is above a threshold start on close monitoring.

Which mistake costs more: starting an at-risk client on standard monitoring costs far more than starting a low-risk client on close monitoring, which costs a week of counselor review time. Loss per 100 new clients: L = r · FN + FP, where FN counts at-risk clients put on standard monitoring, FP counts low-risk clients put on close monitoring, and r is the cost of a miss in units of one unneeded week of close monitoring. The best threshold depends on r, so I will report the decision across a range of r and say which value I believe and why.
