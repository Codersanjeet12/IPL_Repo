# IPL_Repo
IPL DASHBOARD AND ORANGE CAP , PURPLE CAP MORE.............
🏏 IPL Matches Analytics Dashboard

An interactive Power BI style dashboard built on 1,169 IPL matches (2008–2025), with a side navigation menu, season and team filters, and six analysis pages.

Dashboard Preview

📌 Project Overview

This project explores IPL match-level data to answer questions like:

Which teams win the most, and how consistent are they?
Does winning the toss actually help win the match?
Is it easier to defend a total or to chase?
Which venues and cities host the most matches?
📂 Dataset
Item	Detail
File	ipl_matches_data.csv
Rows	1,169 matches
Columns	24 (season, teams, toss, venue, city, winner, win margin, result, stage)
Period	2008 – 2025 (18 seasons)

Cleaning steps

NULL in win_by_runs / win_by_wickets converted to blanks (numeric)
Season 2020/21 standardised to 2020
City Bengaluru merged with Bangalore
Venue names unified (e.g. "Wankhede Stadium, Mumbai" → "Wankhede Stadium", Feroz Shah Kotla → Arun Jaitley Stadium)
Team1/Team2 unpivoted into a TeamMatches table for team-wise analysis
📊 Dashboard Pages
Page	What it shows
Overview	Matches, seasons, ties/no result, defending win %, toss-winner win %, matches per season, wins by team
Teams	Played, won, win % and toss won for every team
Toss Analysis	Field vs bat decision by season, toss winner vs match winner
Venues	Top 10 venues and cities by matches
Win by Runs 🟠	Matches won while defending: average and biggest margin, margin distribution
Win by Wickets 🟣	Matches won while chasing: average wickets in hand, distribution
✨ Features
Side navigation menu (collapsible)
Season filter and Team filter for the 10 current IPL teams: CSK, DC, GT, KKR, LSG, MI, PBKS, RR, RCB, SRH
Team chips showing wins, matches and win % for the selected season
All pages respond to both filters
🔍 Key Insights
Mumbai Indians have the most wins (153), followed by Chennai Super Kings (142).
Teams chose to field first in 764 matches vs bat first in 404.
The toss winner won the match in about 52% of decided matches, so the toss is only a small advantage.
Defending teams won 531 matches (avg margin 30.3 runs, biggest 146 runs); chasing teams won 615 (avg 6.2 wickets in hand).
🧮 Key DAX Measures
DAX
Total Matches = COUNTROWS(ipl_matches_data)
Decided = CALCULATE([Total Matches], ipl_matches_data[result] = "win")
Toss Winner Won % =
DIVIDE(
    COUNTROWS(FILTER(ipl_matches_data, ipl_matches_data[toss_winner] = ipl_matches_data[match_winner])),
    [Decided])
Defending Wins = COUNTROWS(FILTER(ipl_matches_data, NOT ISBLANK(ipl_matches_data[win_by_runs])))
Chasing Wins   = COUNTROWS(FILTER(ipl_matches_data, NOT ISBLANK(ipl_matches_data[win_by_wickets])))
Team Played = DISTINCTCOUNT(TeamMatches[match_id])
Team Wins   = COUNTROWS(FILTER(TeamMatches, TeamMatches[team] = TeamMatches[match_winner]))
Team Win %  = DIVIDE([Team Wins], [Team Played])
🛠️ Tools Used

Power BI Desktop · DAX · Power Query · HTML / CSS / JavaScript (Chart.js) for the web version

▶️ How to Run
Power BI version: open IPL_Dashboard.pbix in Power BI Desktop.
Web version: open index.html in any browser (internet needed for Chart.js), or host it with GitHub Pages: Settings → Pages → Deploy from branch → main.
📁 Repository Structure
├── ipl_matches_data.csv
├── IPL_Dashboard.pbix
├── index.html
├── images/
│   └── dashboard_preview.png
└── README.md
👤 Author

Sanjeet Kumar – Data Science & AI learner LinkedIn · GitHub
