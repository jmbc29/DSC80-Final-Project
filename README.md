**INTRODUCTION**

The dataset I have chosen is the League of Legends dataset from Oracle’s Elixir, which is stored in a CSV containing data from professional League of Legends competitive matches from 2014 to 2025. For this project, I decided to specifically on data from the 2022 season, as it contains a large number of recorded matches which will give me more data to analyze for my topic. Since the League of Legends gameplay environment changes significantly from year to year due to different strategies and popular game play metas, data from different seasons were not combined in this analysis.


**Questions I have about the dataset:**

1. What are some common attributes of winning teams?
2. Which position is most likely to accumulate the most gold?
3. How closely related are team kills and winning?
4. How important is placing wards when it comes to winning?
5. Do teams that achieve certain match objectives (firstdragon, firsttower, firstbaron) tend to win more often?
6. Can you predict a game's duration based on other features?
7. Can you predict what position someone played by other features?


I will investigate the relationship between vision control and gold advantage during a League of Legends match. While there are many interacting components that influence the outcome of a game, vision control is a strategic element that is often discussed qualitatively but less frequently analyzed quantitatively. Vision control refers to the management of map visibility through the placement of wards and the removal of enemy wards, allowing teams to track opponent movements and make informed strategic decisions. Effective vision control can enable safer farming, better objective control, and more efficient rotations, all of which may contribute to a team’s overall economic advantage.

Through my exploration of this dataset, I aim to answer the following question:

**Is vision advantage associated with higher gold advantage during a League of Legends match?**



**Dataset Description**

The dataset consists of ranked League of Legends match data, where each row corresponds to a player in a single match. Key features include:

visionscore: Contribution to team vision

wardsplaced: Number of wards placed

earnedgold: Total gold earned

position: Player role

split: Game patch / time period

win: Match outcome (target variable)

Missingness and feature distributions were carefully analyzed prior to modeling.



**Exploratory Data Analysis**
Vision Score Distribution

The distribution of vision score is right-skewed, indicating that while most players contribute moderate vision, a smaller group contributes significantly more.

<iframe src="assets/vision-score.html" width="750" height="550"></iframe>



**Wards Placed Distribution**

Ward placement is a key driver of vision. Most players place a relatively small number of wards, with fewer players placing very high amounts.

<iframe src="assets/wards-placed.html" width="750" height="550"></iframe>



**Missingness Analysis**

To determine whether missing data was random, Total Variation Distance (TVD) permutation tests were conducted.

Split Missingness Test

This test examines whether missingness depends on the game split.

<iframe src="assets/tvd-split.html" width="750" height="550"></iframe>

Conclusion:
The observed TVD falls within the permutation distribution, suggesting missingness is consistent with randomness.




**Position Missingness Test**

This test examines whether missingness depends on player position.

<iframe src="assets/tvd-position.html" width="750" height="550"></iframe>

Conclusion:
The observed TVD is significantly larger than expected under randomness, indicating missingness is not completely random with respect to position.




**Hypothesis Testing: Vision and Gold Advantage**
**Question**

Do players with higher vision contribute to greater gold advantages?

**Method**

Players were split into high-vision and low-vision groups, and a permutation test was used to evaluate the difference in mean gold advantage.

<iframe src="assets/gold-diff-permutation.html" width="750" height="550"></iframe>
**Result**

The observed difference lies in the extreme tail of the permutation distribution, producing a statistically significant p-value.

**Conclusion:**
Higher vision contribution is associated with greater gold advantage.




**Prediction Modeling**
**Baseline Model**

A baseline Random Forest classifier was trained to predict match outcomes using gameplay features.

**Final Model**

The final model incorporated:

Feature scaling

One-hot encoding for categorical variables

Hyperparameter tuning via cross-validation

Performance was evaluated using:

Precision

F1 score

Confusion matrix analysis

The tuned model significantly outperformed the baseline.




**Fairness Analysis**

To assess fairness, model precision was compared across low-gold and high-gold player groups using a permutation test.

Conclusion:
The model demonstrates measurable differences in performance across gold contexts, indicating potential fairness concerns that warrant further investigation.
