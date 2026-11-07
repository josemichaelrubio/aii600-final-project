# References

Each source lists what was taken from it, why, and how it was checked. "Read directly" means the numbers came from the source itself. "Secondary" means they came from a summary of the source and still need checking against the original before the final talk.

## Data

**SAMHSA. National Survey on Drug Use and Health (NSDUH), public-use files.** https://www.samhsa.gov/data/data-we-collect/nsduh-national-survey-drug-use-and-health/datafiles/2023

- Pulled: the files come in SAS, SPSS, Stata, R, ASCII, and tab-delimited formats. Data from 2021 on cannot be compared or pooled with earlier years, because web interviews were added. The public files leave out most geographic variables. The page states no license or redistribution terms.
- Why: it is the project's data source. The comparability break sets the years used (2021 on). A later break in the treatment questions narrows that to 2022 on (next entry).
- Checked: read directly, 2026-10-26.

**Center for Behavioral Health Statistics and Quality, SAMHSA. (2025). *2024 National Survey on Drug Use and Health (NSDUH): Methodological summary and definitions*, §3.4.10 Mental Health Treatment, pp. 90–91, and footnote 9 (p. 13).** https://www.samhsa.gov/data/sites/default/files/reports/rpt56485/2024-nsduh-method-summary-defs.pdf

- Pulled:
  - The mental-health treatment questions were heavily revised for 2022. Estimates from 2022 "should not be compared with estimates from 2021."
  - Starting in June 2024, every inpatient and outpatient location got the added text "for mental health, emotions, or behavior," and the grid headings became "LOCATION." Treatment estimates overall and for inpatient or outpatient locations from 2024 "are not comparable with those from 2022 and 2023." Prescription medication, telehealth, and jail or prison treatment remain comparable.
  - Footnote 9: the changes "were presented to respondents starting in June 2024," so 2024 mixes the two wordings.
- Why: sets the split. Train on 2022, test on 2023, check on 2024 (`decisions.md`, 2026-11-06).
- Checked: read directly (PDF text, including the recommended citation on the title page), 2026-11-06.

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

**Stanley, B., Brown, G. K., Brenner, L. A., et al. (2018). Comparison of the Safety Planning Intervention with follow-up vs usual care of suicidal patients treated in the emergency department. *JAMA Psychiatry*, 75(9), 894–900. doi:10.1001/jamapsychiatry.2018.1776** https://pmc.ncbi.nlm.nih.gov/articles/PMC6142908

- Pulled:
  - Suicidal behavior over six months, 36 of 1,186 (3.03%) with safety planning plus follow-up calls (SPI+), against 24 of 454 (5.29%) with usual care. Odds ratio 0.56, 95% CI 0.33 to 0.95. Number needed to treat 44.43.
  - "Suicidal behavior" comes from VA Suicide Behavior Reports: suicide attempts, suicide deaths, and other suicidal behaviors, including interrupted attempts.
  - The number of follow-up calls was not associated with suicidal behavior (P = .13). The authors suggest the safety plan may matter more than the calls.
- Derived:
  - About 2.3 events prevented per 100 people (1 / 44.43).
  - Across the odds ratio's 95% CI, 0.25 to 3.5 per 100.
- Why: how much close monitoring helps, the term that turns cost per event into the cost of a miss.
- Limits:
  - A cohort comparison at matched sites, not a randomized trial.
  - Mostly male veterans seen in the emergency department for a suicidal crisis and not admitted, a higher-risk group than adults in outpatient treatment.
  - The intervention was a safety plan plus calls. FirstHarbor's close monitoring is neither, and the call count did not predict the outcome, so the paper supports the plan more than the monitoring.
  - Events mix deaths with interrupted attempts, so the average cost per event is likely below the deaths-included figure from Shepard.
- Checked: read directly, full text, 2026-10-26.

**Nock, M. K., et al. (2008). Cross-national prevalence and risk factors for suicidal ideation, plans and attempts. *British Journal of Psychiatry*.** https://pubmed.ncbi.nlm.nih.gov/18245022/

- Pulled: across 17 countries, about 60% of transitions from suicidal ideation to a plan or attempt happen within the first year after ideation starts.
- Why: the case for monitoring new clients closely early. It is not a term in r.
- Checked: secondary (abstract summary).

**U.S. Bureau of Labor Statistics. Occupational Outlook Handbook: Substance abuse, behavioral disorder, and mental health counselors.** https://www.bls.gov/ooh/community-and-social-service/substance-abuse-behavioral-disorder-and-mental-health-counselors.htm

- Pulled: 2024 median pay, $28.46 per hour.
- Derived: one week of close monitoring at 30 to 60 minutes of counselor review ≈ $14 to $28. The review time is my assumption, not a sourced number.
- Why: the cost of a false alarm, the denominator of r.
- Checked: secondary (search summary of the BLS page).

## Counselor capacity

**American Psychological Association. (2025). *AI in the therapist's office: 2025 Practitioner Pulse Survey*. December 2025.** https://www.apa.org/pubs/reports/practitioner/2025/full-report.pdf

- Pulled:
  - 46% of psychologists had no openings for new patients, and 40% had a waitlist (p. 7).
  - The share with no openings, by year: 65% (2021), 60% (2022), 56% (2023), 53% (2024), 46% (2025) (Figure 8).
  - 22% agreed they had not been able to meet the demand for treatment from their patients (Figure 8).
  - Method: online survey, probability-based sample from APA membership and state licensing boards. 1,742 completed of 26,502 received, a 6.6% completion rate. Licensed doctoral psychologists who treat patients (p. 10).
- Why: counselor time is scarce, so the capacity view leads (`decisions.md`, 2026-11-07).
- Limits: doctoral psychologists, not the master's-level counselors many FirstHarbor clients will see. A low completion rate. It measures openings for new patients, not time for reviewing clients between sessions.
- Checked: read directly, from a copy downloaded from apa.org, 2026-11-07.

**American Psychological Association. (2024). *Topline data tables for 2024 Practitioner Pulse Survey report*.** https://www.apa.org/pubs/reports/practitioner/2024/topline-data-2024-practitioner-survey.pdf

- Pulled:
  - Q20 "Which of the following best describes your current caseload?": 53% (453 of 851) "I do not have any openings for new patients right now."
  - Q21 waitlist: 39% (327 of 849).
  - Q23A time to a new patient's first appointment: under 1 month 56%, 1–3 months 27%, 4–6 months 9%, 7–12 months 4%, more than 12 months 4% (n = 825).
- Why: the exact question wording and counts behind the 2024 figure.
- Checked: read directly, from a copy downloaded from apa.org, 2026-11-07.

**American Psychological Association. (2023, December 5). *Mental health crisis highlights access challenges* [Press release].** https://www.apa.org/news/press/releases/2023/12/mental-health-access-challenges

- Pulled: 56% of psychologists had no openings for new patients in 2023. 561 licensed psychologists responded, from a random sample of 16,557 (August 30 to September 29, 2023).
- Why: the 2023 point, with its sample.
- Checked: read directly, from a saved copy, 2026-11-07.

## Not sourced yet

- The CPI factor that converts 2013 dollars to 2024 dollars (about 1.34, from memory). Look up BLS CPI-U before using it.
- The counselor review time for one week of close monitoring. Ask counselors.
- The share of new clients FirstHarbor's counselors can watch closely in week 1. The capacity view uses 5% to 50% as illustrations, with 20% as the example. Ask counselors.
