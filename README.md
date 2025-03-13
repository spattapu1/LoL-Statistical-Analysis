
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
The dataset has several columns, and the main ones we will focus on are:

- **`gameid`**: A unique identifier of the each game played between two teams.
- **`league`**: The string that denotes the name of the specific league tournament in which the match took place.
- **`side`**: The side of the map that a particular team within a game played on. 'side' is always 'Blue' or 'Red' in our data.
- **`teamname`**: A string of the name of the team playing the game.
- **`result`**: A binary column set to 1 indicating a team won and 0 indicating a team lost that game.
- **`earnedgold`**: The amount of gold earned excluding starting gold, and passive gold.
- **`teamkills`**: The total number of times a team successfully killed an enemy champion during the game.
- **`gamelength`**: The length of a game in seconds. 
- **`damagetochampions`**: The total amount of damage given to enemy champions on each team during the game.
- **`xpat25`**: a measure of how much experience a player has accumulated by the 25-minute mark, reflecting their overall level progression and efficiency in gaining XP compared to the average or their opponent.
- **`csat25`**:  a measure of how many minions and monsters a team has killed by the 25-minute mark, which contributes to gold and experience gain.
- **`dragons`**: The number of dragons secured by the team during the game.
- **`barons`**: The number of barons secured by the team during the game.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning:
The original dataset contains data that pertains to individual players of a team as well as data relavent to the team as a whole. So only kept data pertaining to the entire team within a game rather then all the players. This significantly reduces the amount of rows within out cleaned data. We also only wanted data pertaining to complete games, not partial games, as partial games do not contain timed data like creep score or xp at different times which is why we chose to excluded it. We also decided to convert the gamelength column from seconds to minutes for better readability. 

We only train our final model on games that are 25 minutes or longer, so later in our prediction models, we queried out games with a 'gamelength' less than 25 minutes in order to ensure there are no missing values in xpat25 or csat25. Most games are longer then 25 minutes and on average games are 30 minutes, we want our final model to make classifications for majority of games, not outliers. 

Here’s the first five rows of the cleaned dataset named teams:

| gameid                | league   | side   | teamname                 | gamelength   |   result |   teamkills |   earnedgold |   damagetochampions |   xpat25 |   csat25 |   dragons |   barons |
|:----------------------|:---------|:-------|:-------------------------|:-------------|---------:|------------:|-------------:|--------------------:|---------:|---------:|----------:|---------:|
| ESPORTSTMNT01_2690210 | LCKC     | Blue   | BRION Challengers        | 00:28:33     |        0 |           9 |        28222 |               56560 |    45960 |      767 |         1 |        0 |
| ESPORTSTMNT01_2690210 | LCKC     | Red    | Nongshim Esports Academy | 00:28:33     |        1 |          19 |        33769 |               79912 |    49931 |      864 |         3 |        0 |
| ESPORTSTMNT01_2690219 | LCKC     | Blue   | T1 Esports Academy       | 00:35:14     |        0 |           3 |        34688 |               59579 |    49409 |      895 |         1 |        0 |
| ESPORTSTMNT01_2690219 | LCKC     | Red    | Liiv SANDBOX Youth       | 00:35:14     |        1 |          16 |        48063 |               74855 |    57155 |      928 |         4 |        2 |
| ESPORTSTMNT01_2690227 | LCKC     | Blue   | KT Rolster Challengers   | 00:32:52     |        1 |          14 |        41372 |               67376 |    52441 |      912 |         4 |        1 |

### Univariate Analysis:
We conducted a univariate analysis on the earned gold per team. 
<iframe src="assets/EarnedGold.html" width="800" height="600" frameborder="0"></iframe> 
The histogram shows a normal distribution meaning that earned gold per team is symmetrically distributed around the mean. The normal shape also implies that earned gold is likely independently and identically distributed (i.i.d.), indicating that the underlying process generating earned gold is consistent and stable across teams, therefore is a reliable statistic for analyzing team behavior.

We also conducted a univariate analysis on the team kills per team. 
<iframe src="assets/TeamKills.html" width="800" height="600" frameborder="0"></iframe> 
The histogram shows a relativley normal distribution that is right-skewed meaning that team kills per team is mostly symmetrically distributed around the mean though the mean is lower and few teams obtain an excpetionally high number of kills. The relativley normal shape also implies that team kills is likely independently and identically distributed (i.i.d.), the way players obtain kills is relavtively consistent across teams (though some are much higher) and, therefore is a reliable statistic for analyzing team behavior.

### Bivariate Analysis:
For our bivariate analysis, we decided to focus on **`side`** which is central to much of our analysis later on, and may potentially provide insights about the data.  

In this first visualization, we look at how earned gold varies depending on the side a team is on. 
<iframe src="assets/EarnedGoldSide.html" width="800" height="500px"></iframe> 
Both overlapping distributions are still normal, so we can ascertain the same as prior as well as the fact side is likely not a strong indicator of earned gold. 

In this second visualization, we look at how team kills varies depending on the side a team is on. 
<iframe src="assets/TeamKillsSide.html" width="800" height="600" frameborder="0"></iframe> 
Both overlapping distributions still have a similar overall direction, but the shape of the distributions look slightly different which may suggest that teamkills could be an indicator of side. It's at least likely a stronger indicator of side then earned gold. 

### Interesting Aggregates
Here are some intresting aggregates we can explore within the data: 

| side   |   result |   teamkills |   earnedgold |   damagetochampions |   xpat25 |   csat25 |   dragons |   barons |
|:-------|---------:|------------:|-------------:|--------------------:|---------:|---------:|----------:|---------:|
| Blue   | 0.523086 |     14.8736 |      36566.6 |             67612.1 |  51893.3 |  820.958 |   2.14002 | 0.669482 |
| Red    | 0.476914 |     14.3222 |      35947.7 |             66651.5 |  51831.3 |  822.529 |   2.35135 | 0.681588 |

We grouped by side in order to see the difference in statistics between teams on the blue vs red side, we then gathered the quantitiave columns in order to find the means of each statistic with respect to side. This way we can see the differences in averages between each statistic with respect to side. Here we find that, the teams on Blue side tend to win more, has more team kills, has more earned gold, gives more damage to enemy champions, more xp at 25 minutes on average but Red side has more dragons, more barons and a larger creep score at 25 minutes on average then Blue side. Though when looking at these aggregate, we do have to realize that these differences in averages are marginal. 

## Assessment of Missingness

### NMAR Analysis
We do not think there are any columns in the dataset that are NMAR. We believe that all of the missing data is either missing by design or MAR. Because the original dataset includes data for both invidual players and the teams they are on, columns that only contain aggregate team data are empty for rows containing player data, and columns that only contain individual player data are empty for rows containing team data. There are also null values in the columns containing ban information for each team if they banned less than five champions, but these cells are intentionally left empty because there is no data to enter. Additionally, since many columns in the dataset are related to game statistics at certain times in the game, there will be missing data in those columns if a game ends before that time. In this case, the missingness in this column is dependent on the game length, which is also included in the dataset. There are also rows missing data in all of these time columns, but they all rows containing data from League of Legends Pro League (LPL) games, and these rows also have the value 'partial' in the datacompletenesscolumn, therefore this data is also MAR.

### Missingness Dependency
In this subsection, we will test if the missingness of the **`xpat25`** column depends on other columns. The other two columns that we will check our missingness dependency on are **`side`**, and **`gamelength`**. 

First, let's take a look wether the missingness of **`xpat25`** is dependent on **`gamelength`**. 

**Null Hypothesis:** The distribution of **`gamelength`** when **`xpat25`** is missing is the same as the distribution of **`gamelength`** when **`xpat25`** is not missing. 

**Alternative Hypothesis:** The distribution of **`gamelength`** when **`xpat25`** is missing is **not** the same as the distribution of **`gamelength`** when **`xpat25`** is not missing. 

**Test Statistic:** Kolmogorov-Smirnov Test Statistic

**Significance Level:** 0.5

Subsequent to the permutation tests, we find that the observed statistic is 0.992025507599341, with a p-value of 0. The empirical distribution of the K-S statistic is shown below. 
<iframe src="assets/EDKS.html" style="border: none; padding: 0; margin: 0; width: 800px; height: 500px;"></iframe> 
In this permutation test, the p-value is less than the 0.5 which means we reject the null hypothesis. Therefore, the missingness of the **`xpat25`** column does infact depend on the gamelength column.

Now, let's take a look wether the missingness of **`xpat25`** is dependent on **`side`**. 

**Null Hypothesis:** The distribution of **`side`** when **`xpat25`** is missing is the same as the distribution of **`side`** when **`xpat25`** is not missing. 

**Alternative Hypothesis:** The distribution of **`side`** when **`xpat25`** is missing is **not** the same as the distribution of **`side`** when **`xpat25`** is not missing. 

**Test Statistic:** Total Variation Distance

**Significance Level:** 0.5

The distribution of **`side`** when **`xpat25`** is missing and the distribution of **`side`** when **`xpat25`** is not missing are shown below: 

| side   |   xpat25_missing = False |   xpat25_missing = True |
|:-------|-------------------------:|------------------------:|
| Blue   |                  0.50005 |                0.499253 |
| Red    |                  0.49995 |                0.500747 |

Subsequent to the permutation tests, we find that the observed statistic is 0.992025507599341, with a p-value of 0. The empirical distribution of the Total Variation Test statistic is shown below. 
<iframe src="assets/EDTVD.html" style="border: none; padding: 0; margin: 0; width: 800px; height: 500px;"></iframe> 
In this permutation test, the p-value is greater than the 0.5 which means we fail to reject the null hypothesis. Therefore, the missingness of the **`xpat25`** column does not depend on the **`side`** column.

## Hypothesis Testing

In our hypothesis test, we aim to determine whether there is a significant difference between the average team kills for the blue side and the red side. We want to understand the relationship between being on the red or blue side and the average kills per side. The motivation comes from wanting to determine whether the blue side is actually more likely to win than the red side, as team kills are likely related to the game outcome, making this an important test to explore.

**Null Hypothesis**: The average team kills for blue and red sides is the same.

**Alternative Hypothesis**: The average team kills for blue side is greater then red side.

**Test Statistic**: Difference in Means of team kills for blue side and team kills for red side.

**Significance Level**: 5 Percent

Below is the sampling distribution for the test statistic:
<iframe src="assets/HypTesyDist.html" style="border: none; padding: 0; margin: 0; width: 800px; height: 500px;"></iframe>

## Framing a Prediction Problem
Previously, we have found that being on blue side may have a significant affect on team kills. Since statistics for blue and red side are different, are there specific statistics of gameplay like xpat25, csat25, barons, dragons, etc. that are higher as a result of being on Blue or Red side, and can we use these statistics to predict which side the player was on?

To address this question, we can use a binary classification algorithm to predict wether or not they were on blue or red side. Therefore, our prediction problem is: Are we able to predict wether a team was blue or red side in a game based on other in-game statistics. In this model we intended to predict the side of the team based on teamkills and earnedgold. We attempted to do this for our baseline model which resulted in a model that was not accurate, which we will address in the next section. 

But as a result, we created a new iteration of our prediction problem, which is: Based on the difference in in-game statistics can we predict wether the winning side of a game was blue or red?. This allows for our classification model to have more accurate measures of differences between sides as apposed to general in-game statistics that are not in relation to the other side. Thus our response variable is wether the winner was red or blue which is included in the differences between team statistics dataframe. 

In this section, we queried out gamelength less than 25 minutes in order to ensure no missing values in xpat25 and csat25. If a game ended before that time, games won't have xp or cs at 25 minutes, and since we want to be able to make accurate predictions the average game (most of which are greater than 25 minutes, the average game is 30 minutes). 

In order to evaluate our model we will only be using accuracy. The reason we are not using F-1 scores and only using accuracy because our data is balanced with each game having a red or blue side, and therefore do not have to consider false positives and negatives in the evalution of our model. 

The information that we would know at the time of prediction for the final model is the differences between the statistics for teamkills, earnedgold, damagetochampions, xpat25, csat25, dragons, and barons for our final model and the statistics themselves for the basline model. 

## Baseline Model
## Final Model
## Fairness Analysis
