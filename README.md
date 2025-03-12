
By: Shriya Pattapu and Milo Palmquist
## Introduction 
### General Introduction 
League of Lengends is a multiplayer online battle arena game in which two teams of five play against each other with the objective of destroying the other team's base. The game has an extremely large player base, and there are many competitve leagues for professional teams. The dataset we are working with contains information from individual pro-play games that show both the performance overall and throughout the game for both the players and teams as well as the result of each game.

For this project, we would like to answer the following question: **"Are you more likely perform better if you are on the blue side?"**

 In League of Legends, the map is square-shaped, and players play in three lanes. The top lane is along the left and top edges, the bottom lane is along the right and bottom edges, and the mid lane is along the diagonal from the bottom left corner to the top right one. Each side's base is situated at one of these two corners with blue side at the bottom and red side at the top, and which side a team is on is determined randomly at the start of the game.
 
  In the League of Legends community, many players think that there is an advantage to being on the blue side. This may be attributed to the way the in-game display is set up, as there are generally more features at the bottom of a player's screen, and this may hinder players on the red side's ability to smoothly interact with the part of the screen where their enemies will show up a majority of the game. 
  
  Using this dataset, we can see if even the best of the best are safe from the alleged effect this coin flip. Assuming the skills of each team is similar, then the proportion of wins on one side should not be significantly different from the other.

### Introduction of Columns
Some introduction to the structure of the data. The original data set has x columns, we are working with a data set of x rows and y columns. 
- 'gameid' : A unique identifer of the individual game played between two teams. 
- 'side': The side of the map that a particular team within a game played on. 
- 'result': A binary column set to 1 indicating a team won and 0 indicating a team lost that game. 
- 'earnedgold': 
- 'teamkills': 
- 'damagetochampions':
- 'xpat25':
- 'csat25':
- 'dragons':
- 'barons':
## Data Cleaning and Exploratory Data Analysis:
### Data Cleaning: 
Reduced the number of columns only pulled teams data.
Include the different dataframes for Baseline and Final Model. 
Specify what is used where. 

| gameid                | league   | side   | teamname                 |   result |   teamkills |   earnedgold |   damagetochampions |   xpat25 |   csat25 |   dragons |   barons |
|:----------------------|:---------|:-------|:-------------------------|---------:|------------:|-------------:|--------------------:|---------:|---------:|----------:|---------:|
| ESPORTSTMNT01_2690210 | LCKC     | Blue   | BRION Challengers        |        0 |           9 |        28222 |               56560 |    45960 |      767 |         1 |        0 |
| ESPORTSTMNT01_2690210 | LCKC     | Red    | Nongshim Esports Academy |        1 |          19 |        33769 |               79912 |    49931 |      864 |         3 |        0 |
| ESPORTSTMNT01_2690219 | LCKC     | Blue   | T1 Esports Academy       |        0 |           3 |        34688 |               59579 |    49409 |      895 |         1 |        0 |
| ESPORTSTMNT01_2690219 | LCKC     | Red    | Liiv SANDBOX Youth       |        1 |          16 |        48063 |               74855 |    57155 |      928 |         4 |        2 |
| ESPORTSTMNT01_2690227 | LCKC     | Blue   | KT Rolster Challengers   |        1 |          14 |        41372 |               67376 |    52441 |      912 |         4 |        1 |

### Univariate Analysis: 

Include Histogram of Dragons
and Total kills Histogram 

### Bivariate Analysis: 
Total Kills Bivariate 1: 
<iframe
  src="iframe_figures/figure_11.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Total Earned Gold Bivariate 2: 
<iframe
  src="iframe_figures/figure_13.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
