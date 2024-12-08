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
  src="assets/side_win.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Looking at this, we can see that blue simply wins more often than red side. Which is interesting, because theoretically this should be an even split. But then the question came to be, why does this happen, so then a a figure was created for how often blue side simply has a gold lead, as from experience playing the game, gold is the most important resource to have in the game.

<iframe
  src="assets/blue_has_gold_lead.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Using this graph, we can see that blue has a gold lead only a little under 60% of the time. So then the question becomes how often does blue side win assuming they have a gold lead.
<iframe
  src="assets/win_with_gold_lead.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Already, we can see that this alone says you have roughly an 80% change to win if you're on blue side with a gold lead at 25 minutes. Of course, then the idea would be to look at another variable, experience(xp) leads at 25.
<iframe
  src="assets/win_with_exp_lead.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Thus we see that with an exp lead at 25 minutes, there's an even higher chance of winning! This is quite surprising, as was mentioner earlier, gold is widely considered the most important resource in the game, so seeing that a lead in exp has a higher chance of winning on blue side than gold is quite interesting. 

Now with the last difference at 25 that is mentioned in the dataset, cs.
<iframe
  src="assets/win_with_cs_lead.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This seems like the weakest relationship with winning so far, but it is still significant to know that there seems to be some sort of correlation between winning a game on blue side and having a cs lead.

Now looking at a couple of these distribuitions:
<iframe
  src="assets/gold_diff_25_dist.html"
  width="400"
  height="300"
  frameborder="0"
></iframe>
<iframe
  src="assets/exp_diff_25_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/cs_diff_25_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Seeing these distributions, we can see that they're relatively normally distributed, meaning that these are relatively well formed for any work that we need to do using them.