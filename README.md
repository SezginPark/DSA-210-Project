# DSA-210-Project

# Project Overview
This project aims to analyze how game updates and discount events influence the player count in both the short term and long term by analyzing user count data from steamcharts and discount and updates from individual game pages. This study will explore the patterns of player engagement before, during, and after major updates and discounts.

The aim of this project is whether updates and discounts can make lasting player growth or their impacts are temporary. This research will help in understanding how game developers can optimize their content strategies and pricing models to maximize player retention.

# Objectives 

- Analyze Short-Term vs. Long-Term Player Growth:
->Measure the immediate and long-term impact of updates and discounts on player numbers.

-  Evaluate Discount Effectiveness:
->Compare player count trends before and after discount periods.
->Identify if player retention increases or if numbers drop after the discount ends.

- Assess Update Impact: 
->Determine whether new content, patches, or expansions significantly boost player engagement.
->Analyze whether major updates have a stronger effect than minor balance patches.

- Compare Different Games & Genres: 
->Identify which types of games benefit the most from updates and discounts.
->Compare free-to-play vs. paid games in terms of player retention after events.

- Examine Seasonal Trends & External Factors:
->Identify whether certain months (e.g., holiday seasons) amplify the effect of discounts and updates.
->Analyze if certain pricing strategies are more effective depending on the time of year.

# Motivation
- Gaming industry trends: I want to explore how updates and discounts impact player engagement across different games and genres.
- Financial strategies: Understanding how pricing models affect long-term player retention can provide insights into effective revenue strategies.
- Data analysis: By examining historical player count data, I aim to identify patterns that help predict the success of updates and discounts.

  ## Hypotheses

### Hypothesis 1: Sale vs Non-Sale Player Counts  
- **H₀:** The mean monthly average players in sale months equals that in non-sale months.  
- **H₁:** The mean monthly average players in sale months is greater than in non-sale months.

---

### Hypothesis 2: Sale-Month vs Previous Month  
- **H₀:** The mean difference `(avg_players_sale − avg_players_prev_month)` is zero.  
- **H₁:** The mean difference `(avg_players_sale − avg_players_prev_month)` is not zero.

---

### Hypothesis 3: Indie vs AAA Percent Gain  
- **H₀:** The median percent gain during sales for Indie titles equals that for AAA titles.  
- **H₁:** The median percent gain during sales for Indie titles is greater than that for AAA titles.

---

### Hypothesis 4: Price Elasticity  
- **H₀:** The correlation between a game’s list price and its percent gain during sales is zero.  
- **H₁:** The correlation between a game’s list price and its percent gain during sales is non-zero.  
*(Alternatively, if you expect pricier games to gain more, use “greater than zero” for H₁.)*

---

### Hypothesis 5: Update-Driven Spikes  
- **H₀:** The mean month-over-month percent change in average players for update months is zero.  
- **H₁:** The mean month-over-month percent change in average players for update months is greater than zero.


# Dataset
- Player count : monthly active player .
- Discounts : time duration and percentage.
- Updates : type of update.
- Monetization : how does the developers aim to make money of off the game.
- External sources : major gaming events, holidays, new relaises.

# Data Sources
- (https://steamcharts.com) for active player data.
- Official Game Websites for updates, discounts and event data.
  

