# UFC Fight Analysis: Power BI Dashboard

This project is a Power BI dashboard built on 32 years of UFC data (8,500+ fights, 4,400+ fighters, March 1994 to March 2026). It rebuilds the six findings from my [SQL analysis](https://github.com/Mustafa-GitHub/ufc-fight-analysis-sql), with an overview page and one page per finding.

![Overview](screenshots/01_overview.png)

## Tools

- **Power BI Desktop**
- **Power Query**: cleaning and reshaping
- **DAX**: measures, calculated columns and a calculated table

## How It Was Built

**Power Query**

- Cleaned messy weight class labels into 13 divisions with a conditional column.
- Grouped 10 finish methods into Decision, KO/TKO and Submission.
- Reshaped the fights table so each fight became two rows, one per fighter, using Append. This gave 17,102 rows, the same as my SQL view.

**Data model**

- Linked fighters to fights on fighter name. The link is many-to-many because 7 fighters share a name.
- Set the filter to flow one way only: fighters filter fights.

**DAX**

- Measures for wins, win rate, finishes and accuracy.
- CALCULATE to count only finishing wins.
- RANKX to rank fighters within each division and each volume tier.
- A calculated table to give one row per fighter for the striking analysis.
- SWITCH to group fighters into volume tiers.
- A running count of losses, using VAR, to find win streaks. Each new loss starts a new streak.

## Validation

Every page was checked against my SQL results, and all of them matched. For example: southpaws win 52.5%, and Jon Jones's longest streak is 19. The win streak page used a different method from SQL, but gave the same streaks and dates.

## Pages

**Overview (shown above):** the size of the data, and the number of fights in each division.

**Stance:** southpaw and switch fighters win about 52.5%, while orthodox fighters win 49.4%.

![Stance](screenshots/02_stance.png)

**Finish Methods:** decisions rose from 0% of fights in 1994 to about 50% today. Submissions fell from about 65% to under 20%, while KO/TKOs stayed steady.

![Finish Methods](screenshots/03_finish_methods.png)

**Finishers:** Gerald Meerschaert finished all 12 of his wins. Charles Oliveira stands out for volume, with 21 finishes from 25 wins.

![Finishers](screenshots/04_finishers.png)

**Division Leaders:** ranking by win rate alone found the real champions, including Khabib, Jon Jones, Volkanovski and Amanda Nunes.

![Division Leaders](screenshots/05_division_leaders.png)

**Striking:** the best accuracy drops as volume rises, from 74% for low-volume fighters to 59% for high-volume ones. Volkanovski keeps 57% across 3,178 attempts.

![Striking](screenshots/06_striking.png)

**Win Streaks:** Jon Jones holds the longest streak, 19 wins from 2010 to 2024. Anderson Silva's famous run of 16 lasted from 2006 to 2012.

![Win Streaks](screenshots/07_win_streaks.png)

## How to View

- **[ufc-dashboard.pdf](ufc-dashboard.pdf):** the full dashboard, readable by anyone
- **[ufc-fight-analysis-dashboard.pbix](ufc-fight-analysis-dashboard.pbix):** the Power BI file. Open it with Power BI Desktop (free, Windows)
- **screenshots:** one image per page

The data comes from the CSVs in my [SQL repo](https://github.com/Mustafa-GitHub/ufc-fight-analysis-sql). To refresh it, point Power BI to the two CSVs in that repo's `data` folder.

## Notes and Limitations

- 2026 is a partial year, so it is left out of the finish methods trend.
- Fighter name is not a perfect key: 7 fighters share a name.
- Strike data is missing for many early fights, so striking results lean towards the modern era.
- The "Other" division mixes non-standard bouts, so it is left out of the division leaders.
