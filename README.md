# Which Side Wins Red or Blue ?
By: Shriya Pattapu and Milo Palmquist 

## Introduction

### General Introduction
League of Legends is a multiplayer online battle arena game in which two teams of five play against each other with the objective of destroying the other team's base. The game has an extremely large player base, and there are many competitive leagues for professional teams. The dataset we are working with contains information from individual pro-play games that show both the performance overall and throughout the game for both the players and teams, as well as the result of each game.

For this project, we would like to answer the following question: **"Are you more likely to perform better if you are on the blue side?"**

In League of Legends, the map is square-shaped, and players play in three lanes. The top lane is along the left and top edges, the bottom lane is along the right and bottom edges, and the mid lane is along the diagonal from the bottom left corner to the top right one. Each side's base is situated at one of these two corners, with the blue side at the bottom and the red side at the top. Which side a team is on is determined randomly at the start of the game.

In the League of Legends community, many players think that there is an advantage to being on the blue side. This may be attributed to the way the in-game display is set up, as there are generally more features at the bottom of a player's screen, and this may hinder players on the red side's ability to smoothly interact with the part of the screen where their enemies will show up a majority of the game.

Using this dataset, we can see if even the best of the best are safe from the alleged effect of this coin flip. Assuming the skills of each team are similar, then the proportion of wins on one side should not be significantly different from the other.

### Introduction of Columns
The original dataset contains 150588 rows and 161 columns. We removed columns that are not relavent in our analysis and maintained columns that represent different key aspects of essential gameplay within games that are relavent. These 12 columns are discribed below: 

- **`gameid`**: A unique identifier of the each game played between two teams.
- **`league`**:
- **`side`**: The side of the map that a particular team within a game played on. 'side' is always 'Blue' or 'Red' in our data.
- **`teamname`**:
- **`result`**: A binary column set to 1 indicating a team won and 0 indicating a team lost that game.
- **`earnedgold`**: The amount of gold earned excluding starting gold, and passive gold.
- **`teamkills`**: The total number of times a team successfully killed an enemy champion during the game.
- **`damagetochampions`**: The total amount of damage given to enemy champions on each team during the game.
- **`xpat25`**: a measure of how much experience a player has accumulated by the 25-minute mark, reflecting their overall level progression and efficiency in gaining XP compared to the average or their opponent.
- **`csat25`**:  a measure of how many minions and monsters a team has killed by the 25-minute mark, which contributes to gold and experience gain.
- **`dragons`**: The number of dragons secured by the team during the game.
- **`barons`**: The number of barons secured by the team during the game.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning:
The original dataset contains data that pertains to individual players of a team as well as data relavent to the team as a whole. So only kept data pertaining to the entire team within a game rather then all the players. This significantly reduces the amount of rows within out cleaned data. We also only wanted data pertaining to complete games, not partial games, as partial games do not contain timed data like creep score or xp at different times which is why we chose to excluded it.

We only train our final model on games that are 25 minutes or longer. So we queried out games with a 'gamelength' less than 1500 inorder to ensure there are no missing values in xpat25 or csat25. Most games are longer then 25 minutes and on average games are 30 minutes, we want our final model to make classifications for majority of games, not outliers. 

Here’s the first five rows of the cleaned dataset named teams:

| gameid                | league   | side   | teamname                | result | teamkills | earnedgold | damagetochampions | xpat25 | csat25 | dragons | barons |
|-----------------------|----------|--------|-------------------------|--------|-----------|------------|-------------------|--------|--------|---------|--------|
| ESPORTSTMNT01_2690210 | LCKC     | Blue   | BRION Challengers        | 0      | 9         | 28222      | 56560             | 45960  | 767    | 1       | 0      |
| ESPORTSTMNT01_2690210 | LCKC     | Red    | Nongshim Esports Academy | 1      | 19        | 33769      | 79912             | 49931  | 864    | 3       | 0      |
| ESPORTSTMNT01_2690219 | LCKC     | Blue   | T1 Esports Academy       | 0      | 3         | 34688      | 59579             | 49409  | 895    | 1       | 0      |
| ESPORTSTMNT01_2690219 | LCKC     | Red    | Liiv SANDBOX Youth       | 1      | 16        | 48063      | 74855             | 57155  | 928    | 4       | 2      |
| ESPORTSTMNT01_2690227 | LCKC     | Blue   | KT Rolster Challengers   | 1      | 14        | 41372      | 67376             | 52441  | 912    | 4       | 1      |


### Univariate Analysis:

#### Earned Gold Histogram:
<iframe src="iframe_figures/dis-of-earnedgold-per-team.html" width="800" height="600" frameborder="0"></iframe>

#### Total Kills Histogram:
A histogram of total kills helps us explore whether there's a correlation between kills and game performance, including whether blue side teams tend to have more kills.
<iframe src="iframe_figures/dis-of-teamkills-per-team.html" width="800" height="600" frameborder="0"></iframe>

### Bivariate Analysis:

#### Total Kills Bivariate 1:
<iframe src="iframe_figures/figure_11.html" width="800" height="600" frameborder="0"></iframe>

#### Total Earned Gold Bivariate 2:
<iframe src="iframe_figures/total-earned-gold-by-side.html" width="800" height="600" frameborder="0"></iframe>

### Interesting Aggregates
Here are some intresting aggregates we can explore wutgun the data: 

| side   |   result |   teamkills |   earnedgold |   damagetochampions |   xpat25 |   csat25 |   dragons |   barons |
|:-------|---------:|------------:|-------------:|--------------------:|---------:|---------:|----------:|---------:|
| Blue   | 0.523086 |     14.8736 |      36566.6 |             67612.1 |  51893.3 |  820.958 |   2.14002 | 0.669482 |
| Red    | 0.476914 |     14.3222 |      35947.7 |             66651.5 |  51831.3 |  822.529 |   2.35135 | 0.681588 |

We grouped by side in order to see the difference in statistics between teams on the blue vs red side, we then gathered the quantitiave columns in order to find the means of each statistic with respect to side. This way we can see the differences in averages between each statistic with respect to side. Here we find that, the teams on Blue side tend to win more, has more team kills, has more earned gold, gives more damage to enemy champions, more xp at 25 minutes on average but Red side has more dragons, more barons and a larger creep score at 25 minutes on average then Blue side. Though when looking at these aggregate, we do have to realize that these differences in averages are marginal. 

## Assessment of Missingness
### NMAR Analysis
### Missingness Dependency
## Hypothesis Testing
## Framing a Prediction Problem
## Baseline Model
## Final Model
## Fairness Analysis
