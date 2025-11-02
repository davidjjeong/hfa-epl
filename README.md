# Effect of COVID-19 Pandemic on Home Advantage in the EPL

## By David Jeong, Ethan Donecoff, Jon Michael Stroh, Yuan Shan

[Presentation Google Slides](https://docs.google.com/presentation/d/1W6Rr6K3RFelzsA5FaUivAlLYFKmvs66r3GynLpQ3htI/edit?usp=sharing)

[Project Instructions](https://sta323-sp23.github.io/project.html)

Description and instructions for reproducibility:

# Getting Started

- In the *terminal* tab, type `cd ~` to navigate to your home directory. Next,
`git clone git@github.com:sta323-sp23/project-team02.git`

- Navigate to the `project-team02` folder and open the Quarto `project.qmd`
file, and click `Render` button in Rstudio to render our final report. You will
see `project.pdf` generated once it has rendered successfully, which you can
view to look at our report.

### Exploratory Data Analysis

1. Upload results from Premier League into `Data` folder

    1. Game data should be in one file (.xlsx) with each season in its own sheet 
    tab.
    For us, this is called "All premier Leage Results - 1992 Onwards." For each
    season, the sheet contains a table which should include the following 
    variables: `ID`, `Date`, `Round`, 
    `Home`, `Away`, `Winner`, `Draw-1`, `Draw-2`. `Draw-1` and `Draw-2` are 
    empty unless the result is a draw, in which case `Draw-1` and `Draw-2` 
    contain the home and away teams and `Winner` is empty. This sheet also
    contains another table with
    `Team`, `Wins`, `Draws`, `Losses`, `Games Played`, `Goals For`, 
    `Goals Against`, `Goal Difference`, `Points`, and `Position.` These 
    statistics add information for all 20 Premier League teams. 
    
    2. A .csv should also be included, with the same data as the first 
    table in the sheet above, delimited by commas. This file contains
    all match data for the given period; for us this file is called 
    "All_Match_from_1992.csv". Each row in the .csv looks like the following: 
    >"Num", "ID", "Date", "Home", "Away", "Winner", "Draw-1", "Draw-2"
    
    where "Num" is just the observation number, given in order starting
    with 1 being the first game played in the dataset. 
    
    3. For prediction, .csv files containing current season results and 
    schedule should also be placed in the `Data` folder. The format is the 
    same as the .csv from item 2 above. 
    
2. Perform calculations in project.qmd
    1. Calculate home wins for non-COVID seasons. In this code chunk, 
    data is read in from the league results .xlsx for each non-Covid year,
    counting the number of times home teams won. The same is done for 
    COVID years. The next code chunk compares these results by proportion
    and puts them in a `kable` table. Warning: the calculation takes into
    account the fact that the first 3 years of EPL had 22 teams instead 
    of 20. When calculating the proportions be sure to properly record the
    number of games played for both home and away winners. 
    
    2. Display effect of COVID-19 on Avg. Home Win % of the Top 4 and
    Bottom 3 teams. This code chunk uses functions that take into account
    the COVID years, the team difference from 1993-1995 as discussed above,
    and the start/end years of the data. 
    
### Model Implementation 

1. MM Data preparation: data from the match .csv is read in. COVID and non-COVID
games are 
separated by date. 

2. COVID MM algorithm: an MM function is written, which takes in 
`p0`,`theta0`, 
`h0`, `teams`, `A`, `B`, `iter`. The first three of these inputs specify
the initial values for the algorithm, and `teams` is a list of teams to be
applied. `A` and `B` are matrices constructed from previous input data.
Finally, `iter` is the number of iterations to perform. The MM algorithm is
run using these parameters and the results are reported.  

3. non-COVID MM algorithm: a dataframe is created dividing the data into
the non-COVID seasons. Then matrices `A` and `B` for non-COVID data are
created. Then the MM algorithm is run for the non-COVID case. Again, for
reproducibility purposes, years should be adjusted accordingly if a
different/newer set of data is used. Figures are then created, showing the MLEs 
over time. 

### Hypothesis Testing

1. Hypothesis testing is performed to see if the MLEs obtained above are
significant. A figure is created using the desired seasons and list of MLEs
generated for each season. The plot is then created with parameters chosen
for aesthetic purposes. 

2. Next, the mean, variance, and p-value for the distribution are
calculated and presented in a `kable` table using the generated model data.

### Predictions

1. The current standings and season schedule is read from the appropriate files
in the `Data` folder. The results are merged and then processed, so data must be
introduced in the proper format. A prediction is then made from the above model 
and 
expected scores and power indices are computed and reported in a table. This 
code also shortens the names for some teams, e.g. "Man Utd" instead of 
"Manchester United", so if data with different team names is used, this should
be adjusted accordingly. 

2. Probability of win, loss, and draw is computed for the remaining schedule
and output in a table. Here, some adjustments are made with column names being
shortened, e.g. to "Home" and "Away". If new data is used, the indexing should
be checked to ensure that the proper columns are renamed. 