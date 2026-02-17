# Analysis of Thomas Frank's Tenure at Tottenham Hotspur Football Club

Created by **[Holden Green](https://www.hgorledeenn.github.io)** in February 2026 <br>
Columbia Journalism School, Data Studio

<br>

## The Project
Thomas Frank was removed as head coach of the Tottenham mens team in mid-February 2026. This story, concieved following his separation from the club and published just a few days later, combines data from a few sources to analyze Frank's tenure in the context of other 2000s-era Spurs coaches.

<br>

## Data Collection and Wrangling
The data for this project came from a few sources and required extensive wrangling.

### <b>(1) [Football-Data.co.uk](https://www.football-data.co.uk/englandm.php) </b>

![football-data.png](/img/football-data.png)

I got most of my team performance data from Football-Data.co.uk, a website with season-by-season results for all Premier League games from the 1993/94 season - present.

Once I had the csvs downloaded, I needed to read them into one dataframe and clean the data. My steps were:

(1) Filter the full dataset to only games where Tottenham was the home team or the away team
```python
only_tot = all_games[(all_games['HomeTeam'] == 'Tottenham') | (all_games['AwayTeam'] == 'Tottenham')]
```

(2) I used (and learned) the `np.where` function and used it to create a new dataframe that organizes the same stats from a Tottenham-focused view (as opposed to stats being, for instance, "Home Team Shots" and "Away Team Shots", my dataframe had "Tottenham Shots" and "Other Team Shots"). A few examples of how I used `np.where` are below:
```python
tottenham['OT'] = np.where(only_tot['HomeTeam'] == 'Tottenham', only_tot['AwayTeam'], only_tot['HomeTeam'])

tottenham['TL'] = np.where(only_tot['HomeTeam'] == 'Tottenham', "H", "A")

tottenham['TFTG'] = np.where(only_tot['HomeTeam'] == 'Tottenham', only_tot['FTHG'], only_tot['FTAG'])
```

### <b>(2) [thfcdb.com](https://www.thfcdb.com)</b>

![thfcdb.png](/img/thfcdb.png)

I also brought in some data from THFCDB.com, specifically using their [manager history](https://thfcdb.com/collections/manager-history) data to create my own dictionary of coach timelines.

(1) I manually entered coach names and dates as a dataframe in my notebook (see an excerpt of the dictionary below). This helped me later when I created a new dataframe analyzing stats across the coaches' tenures.
```python
...
{"coach":"Thomas Frank","start":"2025-06-07","end":"2026-02-11"},
{"coach":"Igor Tudor","start":"2026-02-12","end":"2026-03-01"}
]

coach_df = pd.DataFrame(coaches)
coach_df["start"] = pd.to_datetime(coach_df["start"])
coach_df["end"]   = pd.to_datetime(coach_df["end"])
```

STILL WORKING HERE

<br>

<br>
<br>
<br>
<br>
<br>
<br>
<br>







# project-1-spurs


Short description of what you aimed to accomplish
Short description of your findings
Summary of the data collection process, with links
Overview of the data analysis process
A section about what new skills, approaches, etc you used, or where you grew the most during the project
A section about things you tried to do or wanted to do but did not have the skills/time (but if you have more time you might do)




### Data Diary for my columns:
<b>Season</b>: Season of the game (in the format 0203, where the season spanned 2002 and 2003)
<br><b>Date</b>: Date of the game
<br><b>OT</b>: The team Tottenham played
<br><b>TL</b>: The location of the game, from Tottenham's perspective (H = Home, A = Away)
<br><b>TFTG</b>: Tottenham Full-Time Goals
<br><b>OTFTG</b>: Other Team Full-Time Goals
<br><b>FTR</b>: Full Time Result (W if Tottenham win, L if Tottenham loss, D if draw)
<br><b>THTG</b>: Tottenham Half-Time Goals
<br><b>OTHTG</b>: Other Team Half-Time Goals
<br><b>HTR</b>: Half Time Result (W if Tottenham winning, L if Tottenham losing, D if tied)
<br><b>TS</b>: Total shots by Tottenham
<br><b>OTS</b>: Total shots by the Other Team
<br><b>TST</b>: Tottenham shots on target
<br><b>OTST</b>: Other Team shots on target
<br><b>FTGD</b>: Full-Time goal differential (+ if Tottenham won, - if Tottenham lost, 0 if draw)
<br><b>HTGD</b>: Half-Time goal differential (+ if Tottenham won, - if Tottenham lost, 0 if draw)