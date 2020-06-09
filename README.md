# Capstone - Rising Tennis Star Predictor for Sponsor Companies

**Problem Statement: **

Are there any indicative match statistics that can forecast a rising tennis star between the ages of 17 and 23?

---

## Overview

For this project, I analyzed 2017 data from the Association of Tennis Professionals (ATP). The data consisted of match scores, player statistics, and player rankings. I thoroughly explored the data to identify any trends or common statistics between players of different skill levels and rankings and determined that the three major differentiating features between players are 1st serves, returns, and mental strength. Deliverables include a list of players forecasted to be next generation tennis stars. A player’s ability to make first serve and win their service games defined whether a player would be very successful in professional tennis. However, building on top of that, a player’s ability to also neutralize the opponent’s serve success, increasing their return success, defined whether a player would be considered as a world-class elite athlete.

---

## Model features

|**Feature**|**Type**|**Description**|
|---|---|---|
|**first_serve_pct**|_float_|Averge 1st serve made during player’s service games|
|**first_serve_win_pct**|_float_|Average percentage of points won when point started by player’s 1st serve|
|**rank_change**|_float_|Ranking difference for each player between start and end of the year|
|**cluster_rank**|_int_|Feature that assigns more weight to higher ranked players|
|**second_serve_win_pct**|_float_|Average percentage of points won when point started by player’s 2nd serve|
|**first_return_win_pct**|_float_|Average percentage of points won by player when returning opponent’s 1st serve|
|**second_return_win_pct**|_float_|Average percentage of points won by player when return opponent’s 2nd serve|
|**matches_played**|_int_|Amount of matches played for each player throughout the year|
|**climb_rate**|_float_|Average amount of ranking spots that a player climbs or drops per match|

---

### Procedure / Methodology

	For this project, I began by using three datasets from datahub.io that are comprised of player rankings, statistics, and match scores for ATP players in 2017. I started first by cleaning the rankings dataset as it contained ranking information from 1973-2017. I filtered out all years other than 2017 and engineered the `rank_change` feature that holds the difference in a player’s ranking from the beginning and end of the year. After that I focused on the match scores and stats datasets, dropping irrelevant columns, such as url extensions and tournament orders. 

### EDA

	Analysis began by looking at the difference in first serve percentage, first serve win percentage, second serve win percentage, first serve return win percentage, and second serve return win percentage between the winner and losers of each match throughout the year. This analysis led me to believe that between two players in a match, the winner performed on average about 10% better than their opponent. However, one caveat is that these statistics do not take into account ranking. This means that these stats might be skewed by highly ranked players easily winning against lower ranked players.
	After analyzing the difference in player stats between winners and losers of a match, I analyzed the statistics of players who had failed to win a match throughout the entire year. This analysis led me to believe that players who had not won all year were general statistical outliers since previously I found that players who lost a match performed about 10% worse on average. For this analysis, statistics between players who had won and players who had never won deviated by about 20-30%.
	I then decided to analyze the difference in averages between players in the top 20 rankings and all other players. For this, I found that stats only favored players in the top 20 by about 1-2%. This was interesting because, one might assume that players in the top 20 would be performing substantially better than everybody else, which does not seem to be the case.

	I used a K-mean clustering algorithm with 3 clusters — elite, very good, average. After clustering, I analyzed the difference in stats between the all three clusters. My results were surprising in that, again, elite players were only about 1-2% better than everyone else. 
	One initial result that was very surprising was that players in the very good category had higher service percentage numbers than elite players, but lower winning serve percentage numbers. This means that very good players were making more first serves but not winning as many of them. This result hinted at the fact that returns are a major differentiating factor between elite and very good players. Due to prior domain knowledge and the fact that very good players had higher second serve win percentage numbers indicated that very good players encompassed “big servers” who rely on their powerful serves as their main weapons. However, for these players to reach the next level, they would have to improve on their return games since the elite players are able to neutralize powerful serve with their return games. 
	This sentiment is emphasized in the similarities between elite and average players’ serving statistics, which were roughly the same. However, elite players had a 2% higher first serve return winning percentage. This indicated that average players had neither the firepower of the big servers nor then returning prowess of the elite players, putting them at a big disadvantage.
	All of that being said, one major factor affecting analysis is the inner game side of tennis. It is no surprise that confidence and mental strength is a major determining factor in the outcome of tennis matches. This is evident in that elite players are only 1-2% better than everyone else on average. However, this kind of data is not available and near impossible to measure, but were that not the case, perhaps there would be substantially greater statistical differences between the three groups of players.

### Modeling and Results
	Model resulted in 3 clusters: Elite, Talented, and Average. Overall elite players had a 2% advantage over talented and average players in first serve win percentage, service game win percentage, first serve return win percentage, and second serve return win percentage. However, Talented players had a 2% advantage over all other players in percentage of first serves in play. These results confirmed that first serves are one of the major determining factors for a player’s ranking/skill-level and differentiated the average players from everybody else. These results also confirmed that returns were the other major determining factor for player’s ranking/skill-level. A good return game would allow a player to neutralize the effect of a great server, serving at the main key differentiator between the Elite and Talented groups.
	Finally, the model itself produced terrific results in predicting future tennis stars. The model returned a list of 10 players in the ranking range of 39-120, who all reflected Elite level stats. Out of these players, currently 90% of them are in the top 50, 60% are in the top 20, and 30% are in the top 10. Given all of this, the model was a success and answers the problem statement that service percentages and return percentages are two key statistical families that give great insight into which players have the potential to be future tennis stars.


