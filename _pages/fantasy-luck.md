---
layout: archive
title: "Fantasy Statistics"
permalink: /fantasy/
author_profile: true
---

## Aggregate Matchup Probabilities

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

<iframe id = "myFrame" src = "../files/fantasy/probabilities_1.html" width = "100%" height = "500" frameborder = "0" style = "border: none; display: block;"></iframe>

<script>
  function changeFrame() {
    document.getElementById('myFrame').src = document.getElementById('pageSelector').value;
  }
</script>

## Cumulative Schedule Luck

While playing fantasy, you may have had the misfortune of having a stellar week where you beat everyone in the league except for the team that you actually matched up against. Converseley, you may have had a horrible week, where every possible thing went wrong, but you happened to matchup up against the only other team performing worse than you. Both of these scenarios are extreme forms of **schedule luck**, i.e. how the "when you play who" aspect of fantasy affects your performance over an entire season. The easiest way to disentangle schedule luck from your fantasy performance is to compare the number of categories you won in a given week against your *actual* matchup, to the number of categories that you win *on average* against the rest of the players that you *don't* matchup against that week. If your matchup allows you to win more categories than you should be winning on average, that's schedule luck. The natural variance in player performance week-by-week guarantees that some weeks will be lucky, and others unlucky. That's fine, but over an entire season, we should expect this luck to wash out, and we then use the surplus (or deficit) of luck to brand teams as lucky and unlucky.

The plot below displays this concept for every team, and charts the evolution of this luck over the entire fantasy season. We can keep track of a team's actual performance over the entire season, i.e. the total (cumulative) number of categories won, and the corresponding position that they hold in the league standings. We can also do this by using the *expected* values, i.e. the averages per week, and chart the total (cumulative) *expected* number of categories won and the *expected* league position for a team over the entire season.

That's great, but how do I read this plot for my specific team? To simplify things, let's first use the magnifying button in the top right corner to zoom into the panel that corresponds to your team. There are multiple angles that we can view this plot by:

1. Categories Won -- For every week, i.e. vertical cross-section, you can compare the actual/realized category data point (green) to the expected data point (red). Each point has a delta value and a sigma value. The delta value tells you the week-over-week change , or simply put, the number of categories you won that week. The sigma value keeps track of your *cumulative* number of categories won up to and including this week. The difference between the delta values in red and green is your schedule luck for that week. You are lucky if your actual value is greater than the expected value (red > green), and unlucky in the opposite case (green > red). The difference between the sigma values in red and green is your schedule luck over the *entire season* up to and including that week. If you notice the shaded between the red and green lines is green and growing, then you are lucky and it surprisingly isn't washing out (hence the luck). The opposite is true if the region is shaded red and growing. 

2. League Position -- Another angle to approach the plot by is to look at your actual league position (solid line) and compare it to your league position if you were to sum up your *expected* categories instead (dotted line). Your expected league position is a strong indicator of how your team really ranks against the rest of the league, purging any week-to-week variation. If you have a keen eye, you may have noticed that when the gap between the expected and realized categories is green (realized > expected), then your solid line exceeds your dotted line. In that sense, you are overperforming your expected league position. The opposite is true when the gap is red (expected > realized), and your dotted line exceeds your solid line. Then, you are underperforming your expected league position.

<iframe src = "../files/fantasy/cumulative_luck.html" width = "100%" height = "500" frameborder = "0" style = "border: none; display: block;"></iframe>