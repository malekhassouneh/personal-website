---
layout: archive
title: "Fantasy Statistics"
permalink: /fantasy/
author_profile: true
---

## Aggregate Matchup Probabilities

Want to check how your team fairs against the rest of the league? Use this tool below. To start, use the dropdown menu to pick a category that you want to compare your team in. Any of the 9 categories will do, or you can look at the binary outcome of whether you beat another team. You'll see a heatmap (matrix) that contains team names on the left side and on the bottom. Find your team on the left hand side of the matrix. Your team name comes with two pieces of summary statistics: how you rank overall in that category, and the proportion of times you beat everyone else in that category (imagine a hypothetical scenario where everyone plays everyone else every week, and there aren't specific head-to-head matchups). Of course, the higher the rank the better your team performs, and the proportion should just be interpreted as you do a probability, that ranges in value from 0 to 1. Interested in how your team fairs against a specific other team? Just find the name of that opponent on the bottom axis, and find the cell that corresponds to that matchup. In that cell you'll see three pieces of information: the proportion of the times that you beat that other team, and the average value of the specific category for your team and the other team. The average value for the binary win category is the number of categories you win on average. Naturally, the more dominant you are in a specific matchup, the larger the difference between the two average values, and the higher the probability of you winning. Visually, the color gradient should help you identify how well you fair without looking at any specific numbers. Green = Good, and Red = Bad (obviously).

Ok cool, but how do I make use of this information? A couple of initial thoughts:

1. Inform Trades -- Looking at how your team performs in a certain category, and more crucially the magnitude in which you win/lose each week informs you of whether you have a surplus or deficit in a certain category. You don't need to beat everyone in points scored each week by 100 points, you just need to have enough to beat the second best team, and that locks in the category for you. You can also identify the categories in which you perform the best in, and identify those you want to throw/tank.

2. Strategic Playoffs -- I won't advocate for this, but come the end of the league portion of fantasy, you might want to think strategically about who you'll matchup against in the first round of playoffs. If you are tied at 5th place with 6th, and your matchup as a 6th seed (3rd) is better than the 5th seed (4th), you might want to make sure that you get that seed locked in. Of course, thinking strategically about playoffs may backfire (your placement relies on results elsewhere going a specific way), so tread with caution.

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

## Cumulative Schedule Luck

You may have had the misfortune of having a stellar week where you beat everyone in the league except for the team that you actually matched up against. Converseley, you may have had a horrible week, where every possible thing went wrong, but you happened to matchup up against the only other team performing worse than you. Both of these scenarios are extreme forms of **schedule luck**, i.e. how the "when you play who" aspect of fantasy affects your performance over an entire season. The easiest way to disentangle schedule luck from your fantasy performance is to compare the number of categories you won in a given week against your *actual* matchup, to the number of categories that you win *on average* against the rest of the players that you *don't* matchup against that week. If your matchup allows you to win more categories than you should be winning on average, that's schedule luck. The natural variance in player performance week-by-week guarantees that some weeks will be lucky, and others unlucky. That's fine, but over an entire season, we should expect this luck to wash out, and we then use the surplus (or deficit) of luck to brand teams as lucky and unlucky.

The plot below displays this concept for every team, and charts the evolution of this luck over the entire fantasy season. We can keep track of a team's actual performance over the entire season, i.e. the total (cumulative) number of categories won, and the corresponding position that they hold in the league standings. We can also do this by using the *expected* values, i.e. the averages per week, and chart the total (cumulative) *expected* number of categories won and the *expected* league position for a team over the entire season.

That's great, but how do I read this plot for my specific team? To simplify things, let's first use the magnifying button in the top right corner to zoom into the panel that corresponds to your team. There are multiple angles that we can view this plot by:

1. Categories Won -- For every week, i.e. vertical cross-section, you can compare the actual/realized category data point (green) to the expected data point (red). Each point has a delta value and a sigma value. The delta value tells you the week-over-week change , or simply put, the number of categories you won that week. The sigma value keeps track of your *cumulative* number of categories won up to and including this week. The difference between the delta values in red and green is your schedule luck for that week. You are lucky if your actual value is greater than the expected value (red > green), and unlucky in the opposite case (green > red). The difference between the sigma values in red and green is your schedule luck over the *entire season* up to and including that week. If you notice the shaded between the red and green lines is green and growing, then you are lucky and it surprisingly isn't washing out (hence the luck). The opposite is true if the region is shaded red and growing. 

2. League Position -- Another angle to approach the plot by is to look at your actual league position (solid line) and compare it to your league position if you were to sum up your *expected* categories instead (dotted line). Your expected league position is a strong indicator of how your team really ranks against the rest of the league, purging any week-to-week variation. If you have a keen eye, you may have noticed that when the gap between the expected and realized categories is green (realized > expected), then your solid line exceeds your dotted line. In that sense, you are overperforming your expected league position. The opposite is true when the gap is red (expected > realized), and your dotted line exceeds your solid line. Then, you are underperforming your expected league position.

<iframe src = "../files/fantasy/cumulative_luck.html" width = "100%" height = "800" frameborder = "0" style = "border: none; display: block;"></iframe>