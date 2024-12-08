# League of Legends Game Decided At 25 Analysis  

League of Legends Game Decided at 25 is a project done at the University of Michigan. The project has multiple stages of analysis, starting from exploratory analysis, to creating a base prediction model and a more complicated model. This analysis focuses on the statistics based around the differences at 25-minutes, and how much the statistics collected can help you predict the outcome of the game.  

Author: Dawson Dolby

# Introduction

League of Legends, also known as LoL, is a very popular multiplayer game released by Riot Games in 2009. Since 2009 the game has seen significant growth, having millions of players daily, and the game continues to be one of the most influential video games in today's age. LoL esports is also the most watched esport in 2024, having a peak viewership this year of just under 7 million viewers on its main channels. The dataset that that is being used here is a dataset from Oracle's Elixir, which contains the data for all individual matches for the year 2024. This includes 116,916 rows representing individual matches, and 161 columns all representing different statistics.

When playing League of Legends, many times you hear people wanting to give up part-way through the game, the common phrase "ff15" simply stands for "forfiet 15," or more simply, forfeit at the 15 minute mark in the game. According to League of Graphs, when someone is better at the game, they tend to forfiet the game earlier and more often. At the time of creating this, the average forfiet time for challenger, which is the highest rank in league, is at 25 minutes and 38 seconds. As someone who doesn't like to surrender the game, as every game is theoretically possible to win, this is quite frustrating. 

Thus, the focus of this project is the idea of how decided is the game at 25 minutes. Using data analysis techniques and metrics found at the 25-minute mark of every professional game from the LCS and LEC regions, the aim here is to see how predictable the outcome of a game is at the 25-minute mark. To do this, we will be focusing on the column "result" and the columnsthat end with "diffat25," including xpdiffat25, csdiffat25, and golddiffat25. golddiffat25 is gold difference at 25 minutes, and this represents how far ahead or behind a team is in terms of gold, the main resource to buy more stats in the game. Simiilarly, xpdiffat25 and csdiffat25 represent experience difference at 25 minutes and cs difference at 25 minutes respectively. Experience being what you use to level up for an upgrade in your champion's strength, and cs being one of the many sources of gold in the game. Lastly, result is simply the result of the game, marked with a 1 for a win or 0 for a loss.

# Data Cleaning and Exploratory Analysis  

To clean the data, many steps are taken. First, only the rows with the 'league' column corresponding to LCS and LEC are taken. After this, only the blue side data was included. The reasoning behind this is that when taking both blue and red data, you can see that their statistics are essentially mirrored within the same game, thus this just ends up being duplicate data with very high collinearity.

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
  width="900"
  height="700"
  frameborder="0"
></iframe>
<iframe
  src="assets/exp_diff_25_dist.html"
  width="900"
  height="700"
  frameborder="0"
></iframe>
<iframe
  src="assets/cs_diff_25_dist.html"
  width="900"
  height="700"
  frameborder="0"
></iframe>
Seeing these distributions, we can see that they're relatively normally distributed, meaning that these are relatively well formed for any work that we need to do using them.

Thus, we finish the cleaning taking only the columns mentioned earlier: result, golddiffat25, xpdiffat25, and csdiffat25, resulting in a dataframe that looks something like this:

|   csdiffat25 |   golddiffat25 |   xpdiffat25 |   result |
|-------------:|---------------:|-------------:|---------:|
|            5 |           1187 |        -2552 |        0 |
|          -14 |          -4443 |        -6363 |        0 |
|            7 |            689 |         1706 |        0 |
|            3 |            276 |         1127 |        0 |
|           63 |          14686 |         8279 |        1 |



The final thing that was tried in our exploratory analysis was the idea of "buckets." That is, the idea that you can group together a continuous variable in order to make it a bit more interpretable. Specifically, it was chosen to make 5 buckets for the gold difference column: very negative, negative, neutral, positive, and very positive. The bucket ranges were chosen arbitrarily here, but they were chosen based off of what many would consider to be how possible the game would be to win in these specific game states. very negative being almost impossible to win, with between 10,000 gold behind to 5,000 gold behind. Then negative being hard, but possible to win, from 5,000 gold behind to 1,000 gold behind. Neutral, being essentially even between 1,000 gold behind to 1,000 gold ahead. And then positive and very positive are mirrored with the negative and very negative buckets. Then, the result, csdiffat25, and xpdiffat25 columns are all averaged to see what's going on.

|   golddiffat25_binned |    result |   csdiffat25 |   xpdiffat25 |
|----------------------:|----------:|-------------:|-------------:|
| Very Negative         | 0.0517241 |     -52.7069 |    -7415.12  |
| Negative              | 0.178571  |     -32.2381 |    -3422.32  |
| Neutral               | 0.476923  |      -3.4    |     -244.692 |
| Postive               | 0.730159  |      14.754  |     2593.74  |
| Very Positive         | 0.957447  |      44.7021 |     6994.47  |

Overall, the results are as expected, you can see that as you get a better gold diff, all the other variables increase as well.


