---
layout: archive
title: "Fantasy Statistics"
permalink: /fantasy/
author_profile: true
---

# 1 Aggregate Matchup Probabilities

## 1.1 Basic Introduction

Part of managing your fantasy team requires a coarse understanding of how well your team performs against other teams, also known as **matchup-specificity**, and how well your team performs in specific categories, say **category-specificity**. The more adept you are at approximating these specificities, i.e. zeroing in on your strengths and weaknesses, the likelier you are to make well-informed decisions (trades, waiver pick-ups, etc.) The difficulity is trying to keep track of how well you perform across all of these dimensions on a week-by-week basis. Tabulating this information goes a long way in overcoming this.

The goal is to simply keep track of the binary outcomes for each category of interest and the matchup result for every week. We can then find the *proportion* of times a team beats another team along a specific dimension. Over a wider window weeks, as the season progresses, these proportions or frequencies can be interpreted as **aggregate probabilities**. These probabilities are quite representative, and can be used to infer a team's best (worst) matchup and best (worst) performing categories. 

## 1.2 Graphical Representation

### 1.2.1 How do I read off my probabilities?

To start, use the dropdown menu to pick a category that you want to compare your team in. Any of the 9 categories will do, or you can look at the binary outcome of whether you beat another team. You'll see a heatmap (matrix) that contains team names on the left side and on the bottom. Find your team on the left hand side of the matrix. Your team name comes with two summary statistics: 

1. **Team Rank** -- How you rank overall, across all other teams, in that specific category.

2. **Proportion of Wins** -- The proportion of times you beat everyone else in that specific category (in a hypothetical scenario where everyone plays everyone else every week, and there aren't specific head-to-head matchups).

Interested in how your team fairs against a specific other team? Just find the name of that opponent on the bottom axis, and find the cell that corresponds to that matchup in your specific row. In that cell you'll see two (or three) main pieces of information: 

1. **Proportion** -- Precisely the proportion of times that you beat that other team in that specific category so far.

2. **Team Averages** -- The average value of that specific category for your team and the other team so far. For the matchup outcome variable, the averages represent the number of categories that you and your opponent win on average. 
 
Naturally, the more dominant you are in a specific matchup, the larger the difference between the two average values, and the higher the probability of you winning. Visually, the color gradient should help you identify how well you fair without looking at any specific numbers.

<select id = "pageSelector" onchange = "changeFrame()" style = "display: block; margin: 0 auto; color: #000000;">
  <option value = "../files/fantasy/probabilities_1.html">Matchup Win</option>
  <option value = "../files/fantasy/probabilities_2.html">Field Goals Percentage (FG%)</option>
  <option value = "../files/fantasy/probabilities_3.html">Free Throws Percentage (FT%)</option>
  <option value = "../files/fantasy/probabilities_4.html">3-Point Shots Made (3PTM)</option>
  <option value = "../files/fantasy/probabilities_5.html">Points Scored (PTS)</option>
  <option value = "../files/fantasy/probabilities_6.html">Rebounds (REB)</option>
  <option value = "../files/fantasy/probabilities_7.html">Assists (AST)</option>
  <option value = "../files/fantasy/probabilities_8.html">Steals (ST)</option>
  <option value = "../files/fantasy/probabilities_9.html">Blocks (BLK)</option>
  <option value = "../files/fantasy/probabilities_10.html">Turnovers (TO)</option>
</select>

<iframe id = "myFrame" src = "../files/fantasy/probabilities_1.html" width = "100%" height = "600" frameborder = "0" style = "border: none; display: block;"></iframe>

<script>
  function changeFrame() {
    document.getElementById('myFrame').src = document.getElementById('pageSelector').value;
  }
</script>

### 1.2.1 How do I make use of this information?

A couple of initial thoughts on how this information could be helpful in specific contexts:

1. **Informing Trades** -- Looking at how your team performs in a certain category, and more crucially the magnitude in which you win/lose on average, informs you of whether you have a surplus or deficit in a certain category. For example, you don't need to beat everyone in points scored each week by 100 points, you just need to have enough to beat the second best team, and that locks in the category for you. You can also identify the categories in which you actually perform the best in, and identify those you want to throw/tank, which might contradict our heurestic understandings sometimes.

2. **Matchup Hunting** -- While this could possibly end up backfiring, there is a plausible argument for strategically *losing* matchups towards the end of the league portion of the fantasy season, in hopes of getting a better first round matchup. If you are tied at 5th place with the team currently in 6th, and your matchup as a 6th seed (3rd) is better than the 5th seed (4th), you might want to make sure that you get that seed locked in. Of course, your placement relies on results elsewhere going a specific way, so tread with caution.

<!-- ## 1.3 Mathematical Representation

What follows below is an attempt at a formal exposition of the concepts explored above, but in mathematical terms. While formal notation may seem excessive, this allows for greater tractability of the objects of interest in other related analyses:

<details>
<summary>More Details</summary>

Let $\text{Pr}(X)$

</details> -->

# 2 Cumulative Schedule Luck

## 2.1 Basic Introduction

Have you ever had the misfortune of having your team perform amazingly and beating everyone in the league except for the one team that you actually matched up against? Converseley, you may have had a horrible week, where every possible thing went wrong (underperformance, injuries etc.), but you happened to matchup up against the only other team performing worse than you. Both of these scenarios are extreme forms of **schedule luck**, i.e. how the "when you play who" aspect of fantasy affects your performance over an entire season. Of course, the first scenario above is an example where your schedule luck is positive (lucky), and the second where your schedule luck is negative (unlucky).
 
The easiest way to disentangle schedule luck from your fantasy performance is to compare the number of categories you won in a given week against your *actual* matchup, to the number of categories that you win *on average* against the rest of the players that you *don't* matchup against that week. If your matchup allows you to win more categories than you should be winning on average that week, that's schedule luck at play. The natural variance in player performance week-by-week guarantees that some weeks will be lucky, and others unlucky. That's fine, but over an entire season, we should expect this luck to wash out, i.e. the lucky and unlucky weeks cancel out. Any surplus (or deficit) of luck that remains at the end of the season is then used to brand teams as "lucky" and "unlucky", along this dimension at least.

## 2.2 Graphical Representation

### 2.2.1 What is each line plotting?

The plot below displays this concept for every team, and charts the evolution of schedule luck over the entire fantasy season. We can keep track of a team's actual (realized) performance over the entire season, i.e. the total (cumulative) number of categories won, and the corresponding position that they hold in the league standings. We can also do this by using the *expected* values instead, i.e. the averages per week, and chart the total (cumulative) *expected* number of categories won and the *expected* league position for a team over the entire season.

Let's breakdown the plot line-by-line to simplify it's interpretation. First, use the magnifying glass button in the top right corner to highlight and zoom into the panel that corresponds to your team. Looking at the legend, there are 4 main series that we're charting the trajectory of at every week, i.e. vertical cross section, namely:

1. **Realized Categories** -- For every week, we keep note of the number of categories that your team won in its specific matchup. We call this "realized" as this is the number of categories that you actually won, i.e. not a counterfactual (hypothetical) that we construct. The plot simply adds up these values for each week, and all weeks that occured before it, so a cumulative sum/total. This is the solid green line.

2. **Expected Categories** -- Alternatively, we can take the number of categories that your team won, assuming it played everyone else that week, and average them. This would give us the "expected" number of categories that you should have won that week. Think of this as a midpoint that smooths out any matchup-specific variance, i.e. a fair number of categories that you should be winning that week. This is the solid red line.

3. **Realized Position** -- If we take the realized categories, and rank teams based on that, we simply get the actual league standings table that we're used to seeing. Winning more categories gives you a higher placement. This is the solid black line.

4. **Expected Position** -- Alternatively, using the expected categories, we get a hypothetical league table that ranks teams based on the cumulative value of their expected categories. In theory, this should reflect the "true" league table, providing a stronger indicator of how a team really ranks against the rest of the league by purging any week-by-week variation induced by scheduled matchups. This is the dashed black line.

### 2.2.2 What information does each point contain?

Moreover, each point in the plot, when hovered over, displays some extra information that helps you understand the context behind the data point:

1. **Week & Opponent** -- Simply your opponent's name for that week, and the corresponding week number.

2. **Cumulative Sum** -- For categories, this is the total number of categories that you won up to and including that week, and for league position, this is the position in the standings that corresponds to your cumulative sum. This is labelled as a sigma value ($\Sigma$) because this is ultimately a running sum that includes your performance this week and everything before that week.

3. **Weekly Change** -- For categories, this is the number of categories that you won that week, and for league position, this is the change in your position in the standings. This is labelled as a delta value ($\Delta$) because this is equivalent to the change in your cumulative sum of categories, or your league position, from one week to another (week-over-week).

### 2.2.3 How do I read off my schedule luck?

Tying this back to the concept of schedule luck, we can look at how lucky (or unlucky) one's team was each week, or over the span of the entire season. Specifically:

1. **Weekly Luck** -- At any given week, take the two data points that correspond to a team's realized (green) and expected (red) number of categories won. The difference in the *delta* values of these two points encodes a team's luck for that week. While this is hard to see graphically, this is precisely the difference in the slopes of the green and and red lines, from one week to another. You are schedule-lucky if the difference between the two delta values is positive, and schedule-unlucky if the difference is negative.

2. **Cumulative Luck** -- At any given week, take the two data points that correspond to a team's realized (green) and expected (red) number of categories won. The difference in the *sigma* values of these two points encodes a team's luck up to and including that week. Graphically, this is precisely the vertical distance between the green and red lines. At any given week, when the shaded region between the lines is green, this means that the team is net-schedule-lucky, and has earned more categories than expected. Conversely, when it is red, this means that the team is net-schedule-unlucky, and has earned less categories than expected.

Notice that when the gap between the realized and expected categories is green (realized > expected), then your realized league position (solid line) exceeds your expected league position (dashed line). In that sense, you are overperforming your expected league position. The opposite is true when the gap is red (expected > realized), and your dashed line exceeds your solid line. Then, you are underperforming your expected league position.

<iframe src = "../files/fantasy/cumulative_luck.html" width = "100%" height = "800" frameborder = "0" style = "border: none; display: block;"></iframe>

## 2.3 Mathematical Representation

What follows below is an attempt at a formal exposition of the concepts explored above, but in mathematical terms. While formal notation may seem excessive, this allows for greater tractability of the objects of interest in other related analyses:

Consider the setting of a weekly "Head-to-Head Categories" fantasy league. Let $\mathcal{I}$ be the set of teams in the league (in a 12-team league, $\left|\mathcal{I}\right| = 12$), and let $\mathcal{C}$ be the set of categories scored each week (in a 9-category league, $\left|\mathcal{C}\right| = 9$). For every team, $i$, and week, $w$, we have $x_{i,w} = \left\{x^{c}_{i,w} \right\}_{c \in \mathcal{C}}$, namely the recorded statistics for each of the categories of interest. Given team $i$'s opponent in week $w$, team $i^\prime$, we define $X_{i, w} \equiv X_{(i, i^\prime), w}$ as the number of categories won by team $i$ that week, specifically:

```math
X_{i, w} = \sum_{c \in \mathcal{C}}{\left(I\left\{x^{c}_{i, w} > x^{c}_{i^\prime, w}\right\} + 0.5 \cdot I\left\{x^{c}_{i, w} = x^{c}_{i^\prime, w}\right\}\right)}
```

Note that we drop the opponent index $i^\prime$ in $X_{i, w}$ where necessary moving forward for ease of notation. Notice that $X_{i^\prime, w} = \left|\mathcal{C}\right| - X_{i, w}$, i.e. the residual number of categories, with $ 0 \leq X_{i, w} \leq \left|\mathcal{C}\right|$. Up to and including a specific week, say $\bar{w}$, we can define $\Sigma^{\bar{w}}_{i}$ as the cumulative sum of the number of categories won by team $i$, specifically: 

```math
\Sigma^{\bar{w}}_{i} = \sum_{w \leq \bar{w}}{X_{i, w}}
```

We then define the corresponding league standing position of that team at the end of week $\bar{w}$ as:

```math
\theta^{\bar{w}}_{i} = 1 + \sum_{i^\prime \in \mathcal{I}\setminus{\{i\}}}{\left(I\left\{\Sigma^{\bar{w}}_{i^\prime} > \Sigma^{\bar{w}}_{i}\right\} + 0.5 \cdot I\left\{\Sigma^{\bar{w}}_{i^\prime} = \Sigma^{\bar{w}}_{i}\right\}\right)}
```

As such, for each team $i$ and end-of-week $\bar{w}$ we are interested in the tuple $\left(\Sigma^{\bar{w}}_{i}, \theta^{\bar{w}}_{i}\right)$. Now consider the hypothetical scenario where, instead of a head-to-head format with single opponents each week, every team $i$ in a given week $w$, matches up against the *remainder* of the league, $\mathcal{I}\setminus{\{i\}}$. We then define $\tilde{X}_{i, w}$ as the *expected* number of categories won that week, a simple artihmetic average across all other teams, specifically:

```math
\tilde{X}_{i, w} = \frac{1}{\left|\mathcal{C}\right|}\sum_{i^\prime \in \mathcal{I}\setminus{\{i\}}}{X_{(i, i^\prime), w}}
```

It follows that we can define analogous *expected* objects, $\tilde{\Sigma}^{\bar{w}}_{i}$ and $\tilde{\theta}^{\bar{w}}_{i}$, as above but now using the *expected* number of categories won, $\tilde{X}_{i, w}$, in place of the *realized* number of categories won, $X_{i, w}$, in any given week $w$. Formally, we can now define one's **schedule luck** as the difference between their *realized* cumulative sum of categories won, and the *expected* cumulative sum of categories won, specifically: 

```math
\begin{aligned}
\mathcal{L}_{i}^{\Sigma} &= \Sigma^{\bar{w}}_{i} - \tilde{\Sigma}^{\bar{w}}_{i} \\
 &= \sum_{w \leq \bar{w}}{\left(X_{i,w} - \tilde{X}_{i,w}\right)} \\
 &= \sum_{w \leq \bar{w}}{\Delta^{w}_{i}}

\end{aligned}
```

Note that $\Delta^{w}_{i} = X_{i,w} - \tilde{X}_{i,w}$ corresponds to the week-specific schedule luck for team $i$ at week $w$. Now, the corresponding schedule luck in terms of league standings would then be defined as:

```math
\mathcal{L}_{i}^{\theta} = -1 \cdot \left(\theta^{\bar{w}}_{i} - \tilde{\theta}^{\bar{w}}_{i}\right)
```

Note that the sign of $\mathcal{L}^{\theta}$ must be reversed for an appropriate interpretation of luck, given the decreasing ordinal nature of league standings. $\mathcal{L}_{i}^{\Sigma}$ and $\mathcal{L}_{i}^{\theta}$ can then be interpreted naturally: for any two teams $i$ and $i^\prime$, we say that $i$ has greater schedule luck than $i^\prime$ if $\mathcal{L}_{i}^{\Sigma} \geq \mathcal{L}_{i^\prime}^{\Sigma}$, and similarly $\mathcal{L}_{i}^{\theta} \geq \mathcal{L}_{i^\prime}^{\theta}$.