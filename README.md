# Analysis of Thomas Frank's Tenure at Tottenham Hotspur Football Club

Created by **[Holden Green](https://www.hgorledeenn.github.io)** in February 2026 <br>
Columbia Journalism School, Data Studio

<br>

## The Project
Thomas Frank was removed as head coach of the Tottenham mens team in mid-February 2026. This story, concieved following his separation from the club and published just a few days later, combines data from a few sources to analyze Frank's tenure in the context of other 2000s-era Spurs coaches.

<br>

## Data Collection and Wrangling
The data for this project came from a few sources and required extensive wrangling.

<b>(1) Football-Data.co.uk </b>

![football-data.png](/img/football-data.png)


I got

<br>

## What I Learned
For this project, I put to work a lot of what I learned in my Foundations of Computer class (see other classwork in this [repo](https://github.com/hgorledeenn/CJS-founds-of-comp)). In addition to skills from class, like creating functional scrapers, using for loops in data manipulation and general Pandas knowledge, I challenged myself and learned several new skills for this project.

(1)&ensp;I learned the `.concat` and `.drop_duplicates` command pair, which enabled me to read in stored data and combine it with newly scraped results

```python
df_orig = pd.read_csv("employee_reimbursements.csv")
df_safe = pd.concat([df_orig, df_new], ignore_index = True)
df_safe = df_safe.drop_duplicates(subset=['voucher_name', 'amount', 'payment_date', 'description'], keep='first')
df_safe.to_csv("employee_reimbursements.csv", index=False)
```
(2)&ensp;I learned how to iterate through dataframe groups, which enabled me to succinctly create individual csv files for the transactions by each department

```python
groups = df.groupby(by="DEPARTMENT")
keys = groups.groups.keys()

for i in keys:
   dept = groups.get_group(i)
   name = i.lower()
   name = name.replace(" ", "-")
   name = name.replace("'", "")
   dept.to_csv(f"docs/dept-csvs/{name}.csv", index=False)
```

(3)&ensp;I learned this structure for defining a function, which enabled me to automatically add the html formatting to hyperlink each department name to its transaction list page

```python
def make_link(dep):
   folder = (
       dep.lower()
       .replace(" ", "-")
       .replace("'", "")
   )
   return f"<a href="https://hgorledeenn.github.io/Chicago-Reimbursements-site/{folder}/index.html">{dep}</a>"

df_dept_sum['DEPARTMENT'] = df_dept_sum['DEPARTMENT'].apply(make_link)

df_dept_sum.to_csv("docs/by_department_summary.csv", index=False
```

<br>

## What I Would Add Next Time
I learned a lot through this project and am happy that I challenged myself to create multiple pages and display the data in this way (the assignment only required us to make one visualization on one page). While the website does achieve the goals I set for myself, it also gives me ideas about more functionality that could be included.

In future projects, I would like to add more ways for a user to interact with the data. Some ideas I have for increased functionality include:

- <ins>A more powerful search tool</ins> to allow for the use of advanced search parameters
- <ins>Filtering options</ins> like the ability to specify date or total amount ranges
- <ins>More/varied visualizations</ins>, for instance showing change over time line charts to demonstrate how employee reimbursement spending has fluctuated historically.
- <ins>Further analysis of spending</ins> using natural language processing (specifically of the   `description` column in the data set). This could lead to interesting insights and allow for more complex visualizations like spending by category or analysis of employee travel locations.



















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