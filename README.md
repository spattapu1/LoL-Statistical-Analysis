# By: Shriya Pattapu and Milo Palmquist

## Introduction

### General Introduction
League of Legends is a multiplayer online battle arena game in which two teams of five play against each other with the objective of destroying the other team's base. The game has an extremely large player base, and there are many competitive leagues for professional teams. The dataset we are working with contains information from individual pro-play games that show both the performance overall and throughout the game for both the players and teams, as well as the result of each game.

For this project, we would like to answer the following question: **"Are you more likely to perform better if you are on the blue side?"**

In League of Legends, the map is square-shaped, and players play in three lanes. The top lane is along the left and top edges, the bottom lane is along the right and bottom edges, and the mid lane is along the diagonal from the bottom left corner to the top right one. Each side's base is situated at one of these two corners, with the blue side at the bottom and the red side at the top. Which side a team is on is determined randomly at the start of the game.

In the League of Legends community, many players think that there is an advantage to being on the blue side. This may be attributed to the way the in-game display is set up, as there are generally more features at the bottom of a player's screen, and this may hinder players on the red side's ability to smoothly interact with the part of the screen where their enemies will show up a majority of the game.

Using this dataset, we can see if even the best of the best are safe from the alleged effect of this coin flip. Assuming the skills of each team are similar, then the proportion of wins on one side should not be significantly different from the other.

### Introduction of Columns
The dataset has several columns, and the main ones we will focus on are:

- **`gameid`**: A unique identifier of the individual game played between two teams.
- **`side`**: The side of the map that a particular team within a game played on. 'side' is always 'Blue' or 'Red' in our data.
- **`result`**: A binary column set to 1 indicating a team won and 0 indicating a team lost that game.
- **`earnedgold`**: The amount of gold earned excluding starting gold, purchases, passive gold, and post-death per team in a game.
- **`teamkills`**: The total number of enemy champions a team successfully kills during the game.
- **`damagetochampions`**: The total amount of damage taken to individual champions on each team during the game.
- **`xpat25`**: a measure of how much experience a player has accumulated by the 25-minute mark, reflecting their overall level progression and efficiency in gaining XP compared to the average or their opponent.
- **`csat25`**: Creep Score (CS) at 25 minutes, a measure of how many minions a team has killed, which contributes to gold and experience gain.
- **`dragons`**: The number of dragons secured by the team during the game.
- **`barons`**: The number of barons secured by the team during the game.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning:
We reduced the number of columns to include only relevant data regarding teams. 

Here’s the first five rows of the cleaned dataset named teams:

| gameid                | league   | side   | teamname                | result | teamkills | earnedgold | damagetochampions | xpat25 | csat25 | dragons | barons |
|-----------------------|----------|--------|-------------------------|--------|-----------|------------|-------------------|--------|--------|---------|--------|
| ESPORTSTMNT01_2690210 | LCKC     | Blue   | BRION Challengers        | 0      | 9         | 28222      | 56560             | 45960  | 767    | 1       | 0      |
| ESPORTSTMNT01_2690210 | LCKC     | Red    | Nongshim Esports Academy | 1      | 19        | 33769      | 79912             | 49931  | 864    | 3       | 0      |
| ESPORTSTMNT01_2690219 | LCKC     | Blue   | T1 Esports Academy       | 0      | 3         | 34688      | 59579             | 49409  | 895    | 1       | 0      |
| ESPORTSTMNT01_2690219 | LCKC     | Red    | Liiv SANDBOX Youth       | 1      | 16        | 48063      | 74855             | 57155  | 928    | 4       | 2      |
| ESPORTSTMNT01_2690227 | LCKC     | Blue   | KT Rolster Challengers   | 1      | 14        | 41372      | 67376             | 52441  | 912    | 4       | 1      |

### Univariate Analysis:

#### Histogram of Dragons:
We plotted a histogram of the number of dragons secured by each team. This helps us analyze if securing dragons correlates with winning.

#### Total Kills Histogram:
A histogram of total kills helps us explore whether there's a correlation between kills and game performance, including whether blue side teams tend to have more kills.

### Bivariate Analysis:

#### Total Kills Bivariate 1:


<iframe src="iframe_figures/figure_11.html" width="800" height="600" frameborder="0"></iframe>

#### Total Earned Gold Bivariate 2:


<iframe src="iframe_figures/figure_13.html" width="800" height="600" frameborder="0"></iframe>


### Interesting Aggregates

## Assessment of Missingness
### NMAR Analysis
### Missingness Dependency
## Hypothesis Testing
## Framing a Prediction Problem
## Baseline Model
## Final Model
## Fairness Analysis