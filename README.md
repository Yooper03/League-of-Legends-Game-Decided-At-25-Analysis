# League of Legends Game Decided At 25 Analysis  

League of Legends Game Decided at 25 is a project done at the University of Michigan. The project has multiple stages of analysis, starting from exploratory analysis, to creating a base prediction model and a more complicated model. This analysis focuses on the statistics based around the differences at 25-minutes, and how much the statistics collected can help you predict the outcome of the game.  

Author: Dawson Dolby

# Introduction

League of Legends, also known as LoL, is a very popular multiplayer game released by Riot Games in 2009. Since 2009 the game has seen significant growth, having millions of players daily, and the game continues to be one of the most influential video games in today's age. LoL esports is also the most watched esport in 2024, having a peak viewership this year of just under 7 million viewers on its main channels. The dataset that that is being used here is a dataset from Oracle's Elixir, which contains the data for all individual matches for the year 2024.

When playing League of Legends, many times you hear people wanting to give up part-way through the game, the common phrase "ff15" simply stands for "forfiet 15," or more simply, forfeit at the 15 minute mark in the game. According to League of Graphs, when someone is better at the game, they tend to forfiet the game earlier and more often. At the time of creating this, the average forfiet time for challenger, which is the highest rank in league, is at 25 minutes and 38 seconds. As someone who doesn't like to surrender the game, as every game is theoretically possible to win, this is quite frustrating. 

Thus, the focus of this project is the idea of how decided is the game at 25 minutes. Using data analysis techniques and metrics found at the 25-minute mark of every professional game from the LCS and LEC regions, the aim here is to see how predictable the outcome of a game is at the 25-minute mark.

# Data Cleaning and Exploratory Analysis  

To clean the data, many steps are taken. First, only the rows with the 'league' column corresponding to LCS and LEC are taken. After this, only the blue side data was included. The reasoning behind this is that when taking both blue and red data, you can see that their statistics are essentially mirrored within the same game, thus this just ends up being duplicate data with very high collinearity. Lastly, only the columns that include the "diffat25" columns are taken. These include golddiffat25, xpdiffat25, and csdiffat25. 

The first question that felt like it needed to be answered was simply which side wins more? Red or blue, and thus the following figure was created.
<iframe
  src="assets/side-win.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
