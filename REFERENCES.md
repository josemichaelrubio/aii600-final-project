# References

Each source lists what was taken from it, why, and how it was checked. "Read directly" means the numbers came from the source itself. "Secondary" means they came from a summary of the source and still need checking against the original before the final talk.

## Data

**SAMHSA. National Survey on Drug Use and Health (NSDUH), public-use files.** https://www.samhsa.gov/data/data-we-collect/nsduh-national-survey-drug-use-and-health/datafiles/2023

- Pulled: the files come in SAS, SPSS, Stata, R, ASCII, and tab-delimited formats. Data from 2021 on cannot be compared or pooled with earlier years, because web interviews were added. The public files leave out most geographic variables. The page states no license or redistribution terms.
- Why: it is the project's data source. The comparability break sets the years used (2021 on).
- Checked: read directly, 2026-10-26.

**Gaur, M., et al. (2021). Characterization of time-variant and time-invariant assessment of suicidality on Reddit using C-SSRS. *PLOS ONE*. Dataset: Zenodo record 4543776.** https://zenodo.org/records/4543776

- Pulled: Reddit posts from about 450 to 500 users, labeled by psychiatrists on the Columbia Suicide Severity Rating Scale. License CC BY 4.0.
- Why: the alternative set aside in `decisions.md` (a crisis-message classifier).
- Checked: the license was read directly on the Zenodo record. The user count is secondary (the description says 448, the file name says 500).

**UMD Reddit Suicidality Dataset.** https://users.umiacs.umd.edu/~resnik/umd_reddit_suicidality_dataset.html

- Pulled: access requires documented IRB approval, and an advisor's review alone does not qualify.
- Why: the reason it was rejected.
- Checked: secondary (search summary of the access page).

**ICPSR terms of use (example: study 36501).** https://www.icpsr.umich.edu/web/ICPSR/studies/36501/terms

- Pulled: data may be used "solely for research or statistical purposes" and may not be redistributed without ICPSR's written agreement.
- Why: the reason GMU's ICPSR access cannot supply data for FirstHarbor.
- Checked: secondary (search excerpts of the terms pages).

## The cost ratio r

r is the cost of a missed at-risk client in units of one unneeded week of close monitoring: r = (events prevented per client monitored × cost per event) / (cost of one week of close monitoring).

**Shepard, D. S., Gurewich, D., Lwin, A. K., Reed, G. A., & Silverman, M. M. (2016). Suicide and suicidal attempts in the United States: Costs and policy implications. *Suicide and Life-Threatening Behavior*, 46(3), 352–362.** https://pmc.ncbi.nlm.nih.gov/articles/PMC5061092

- Pulled (2013 dollars):
  - Total cost of nonfatal attempts, $5,251 million (Table 1).
  - 395,000 intentional self-inflicted injuries in 2013, from CDC WISQARS (introduction).
  - Average cost per suicide death, $1,329,553 (Table 2).
  - 9.6 self-injuries for every suicide (Discussion).
  - 97.1% of the total cost is lost productivity (Abstract).
- Derived:
  - Cost per nonfatal attempt ≈ $5,251M / 395,000 ≈ $13,300.
  - Cost per suicidal-behavior event, deaths included ≈ (9.6 × $13,300 + $1,329,553) / 10.6 ≈ $137,000.
- Why: the cost of a miss, the numerator of r.
- Limits: almost all of the cost is lost earnings. The authors say emotional costs are not estimated.
- Checked: read directly, full text, 2026-10-26.

**Stanley, B., et al. (2018). Comparison of the Safety Planning Intervention with follow-up vs usual care of suicidal patients treated in the emergency department. *JAMA Psychiatry*.** Summary used: https://www.npr.org/sections/health-shots/2018/07/11/628029412/a-simple-emergency-room-intervention-can-help-cut-future-suicide-risk

- Pulled: suicidal behavior over six months was 3.03% with safety planning plus follow-up calls, against 5.29% with usual care (odds ratio 0.56).
- Derived: about 2.3 events prevented per 100 people followed.
- Why: how much close monitoring helps, the term that turns cost per event into the cost of a miss.
- Limits: a cohort comparison, not a randomized trial. Veterans seen in the emergency department, a higher-risk group than adults in outpatient treatment. Weekly calls are not FirstHarbor's close monitoring. Treat 2.3 per 100 as an upper bound.
- Checked: secondary (news and trade-press summaries). Check against the paper before the final talk.

**Nock, M. K., et al. (2008). Cross-national prevalence and risk factors for suicidal ideation, plans and attempts. *British Journal of Psychiatry*.** https://pubmed.ncbi.nlm.nih.gov/18245022/

- Pulled: across 17 countries, about 60% of transitions from suicidal ideation to a plan or attempt happen within the first year after ideation starts.
- Why: the case for monitoring new clients closely early. It is not a term in r.
- Checked: secondary (abstract summary).

**U.S. Bureau of Labor Statistics. Occupational Outlook Handbook: Substance abuse, behavioral disorder, and mental health counselors.** https://www.bls.gov/ooh/community-and-social-service/substance-abuse-behavioral-disorder-and-mental-health-counselors.htm

- Pulled: 2024 median pay, $28.46 per hour.
- Derived: one week of close monitoring at 30 to 60 minutes of counselor review ≈ $14 to $28. The review time is my assumption, not a sourced number.
- Why: the cost of a false alarm, the denominator of r.
- Checked: secondary (search summary of the BLS page).

## Not sourced yet

- The CPI factor that converts 2013 dollars to 2024 dollars (about 1.34, from memory). Look up BLS CPI-U before using it.
- The counselor review time for one week of close monitoring. Ask counselors.
