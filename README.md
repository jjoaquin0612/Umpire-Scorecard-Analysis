# MLB Umpire Scorecard Analysis 
**Author:** Jack Joaquin, Bridgewater State University   

This repository is a semester-long data mining project that evaluates MLB home-plate umpire performance using game-level data downloaded from [umpscorecards.us](https://umpscorecards.us/data/games). Home-plate umpires make roughly 150 balls-or-strike calls a game, and this project calculates the average for each umpire statistic, groups umpires into performance tiers, flags unusually poor games, investigates umpire output by team and stadium, and examines how umpire accuracy relates to how often calls are challenged under the 2026 automated ball-strike challenge system.

Each folder represents a different analysis I conducted on the dataset. 

## Umpire Analysis  
The `UmpireAnalysis` folder focuses on every umpire's calling quality, accuracy, and consistency relative to their calculated expectations during the 2018-2026 seasons. The following bullets are other mining questions that will be answered within this folder:
- Are umpires performing better in the Postseason?
- Are umpires getting better each season?
- Do umpires demonstrate bias towards home teams?
- Has the expectation of correct calls for umpires gotten higher? (Is MLB expecting too much from their umpires?)  

## Stadium Analysis  
The `StadiumAnalysis` folder focuses on every team/stadiums umpire quality during the 2018-2026 seasons and compares it to the rest of the league. The following bullets are some mining questions that will be answered:
- Which team performed best and worst behind each umpire at home plate?
- Which teams/stadiums consistently get good/bad umpire results?
- Which teams have the most umpire bias?
  
## ABS Analysis  
The `ABSanalysis` folder will focus on just the 2026 season (the only season where ABS existed) to examine the newly added 'Automated Ball-Strike System' (ABS) and its effect on umpire calling quality. The questions that will be answered are the following:
- Which umpires are challenged by ABS the most/least?
- Which umpires are overturned the most/least?
- Is there a relationship between an umpire's overall accuracy/consistency and how frequently their calls are overturned?
- Does ABS affect umpire calling quality?

## Data
These are the columns of the dataset and their meanings: 
| Column | Meaning |
| :--- | :--- |
| `Data`, `Umpire`, `Home`, `Away` | Game date, home-plate umpire, home/away teams |
| `Pitches Called` | Called balls and strikes (taken pitches) in the game |
| `Accuracy` | % of pitches that were correctly called |
| `Expected Accuracy` | Model-estimated % an average umpire would get right |
| `Accuracy Above Expected` | `Accuracy` minus `Expected Accuracy` |
| `Correct Calls Above Exp.` | Net difference of actual correct calls and what was expected |
| `Consistency` | % of calls consistent with the umpire's own zone that game |
| `Total Run Impact` | Runs affected by missed calls |
| `Favor (Home) ` | Net lean of calls toward the home (+) or away (-) team |
| `Num. Challenged`, `Num. Overturned` | ABS challenge counts (2026 only) |
| `Chal Win. Pct` | % of challenges won by the challenger (2026 only) |

Columns created manually: `Game_Type` (regular season vs postseason, by date cutoff), `Stadium_Played`, and `Year`

### Data caveats
- **Accuracy is measured differently in 2026.** This will play a big part in `UmpireAnalysis`. UmpScorecards began grading calls against the official ABS strike zone, and earlier seasons were not recalculated, so raw accuracy is not directly comparable across that boundary. The analysis standardizes each metric within its season (z-scores) to account for this.
- **Challenge data exists for 2026 only.** The correlation and Apriori analyses use 2026 games exclusively.
- **Expected accuracy is a moving baseline.** This will also play a big part in `UmpireAnalysis`. Expected accuracy comes from a gradient-boosted model (pool of all umpires' calls from the prior season) recalibrated on a rolling 30-day window, so it tracks league-wide changes in how the zone is called.

### Acknowledgments
If you are still confused about what a column measures, visit [umpscorecardExplainers.us](https://umpscorecards.us/page/info/explainers) for a better explanation. A big thank you to UmpScorecards for the work they do and for keeping their data up to date.
