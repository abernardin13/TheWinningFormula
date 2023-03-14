# TheWinningFormula
Repository for Data Analytics project
TheWinningFormula consists of the 'Baseball' dataset in CSV form, pulled from https://www.kaggle.com/datasets/wduckett/moneyball-mlb-stats-19622012. It contains data on batting average, slugging, on-base percentage, runs for and against, win-loss record, opponents' on-base percentage, opponents' slugging for each Major League Baseball team from 1962 to 2012 and whether a team made the playoffs in those years. The purpose of this project is to identify how many wins it takes to make the playoffs by assessing by how much a team needs to outscore their opponents and how On-Base Percentage and Slugging factor into run differential.

# Assessing the Data

The data types within the Baseball dataset are as follows along with the quantity:

Object = 2
int 64 = 7
float64 = 7

Four variables contain NA's:

RankSeason = 988
RankPlayoffs = 988
OOBP = 812
OSLG = 812

# How Are NA's Treated?

NA's within the dataset are all contained within four variables: RankSeason, RankPlayoffs, OOBP, and OSLG. NA's in RankSeason and RankPlayoffs will be converted to zeros (0) as they don't necessarily pertain to whether a team made the playoffs in this case. Teams with a ranking in RankPlayoffs are teams that made the playoffs. And only teams that made the playoffs were givin a ranking in RankSeason.

NA's in OOBP (Opponent's On-Base Percentage) and OSLG (Opponents Slugging) will be predicted using a linear regression model. It is believed that OOBP and OSLG contribute to RA (Runs Against), a key factor in calculating RD (Run Differential).

# Distribution

Histograms of the variables appear to show the data is normally distributed. The variables shown are Wins, Run Differential, Runs Scored, Runs Against, On-Base Percentage, Slugging, Opponents On-Base Percentage, and Opponents Slugging. However, a Shaprio-Wilk test gives a very different result, with a p-value of 0.0. This would suggest that the data set is not normally distributed.

# Correlation

We can use a correlation matrix to determine the correlation between the variables. The variables with the highest correlation with making the playoffs are Wins, RD, OBP, SLG, and BA. OOBP and OSLG both have negative correlations with making the playoffs. This makes sense because high percentages in these areas should mean more runs against, which should mean more losses. However, initially there are NA's within four variables: RankSeason, RankPlayoffs, OOBP, and OSLG. After removing RankSeason and RankPlayoffs as they are not needed, and predicting the NAs for OOBP and OSLG, correlation between Playoffs and OOBP and OSLG increases, though the correlation is still negative.

#Can Machine Learning Predict Important Variables?

We can use wrapper-based, filter-based and embedded feature selection technique to determine how well machine learning can predict the important variables. For each we will show the scores for 8 variables

From wrapper-based techniques, Forward Elimination and Backward Elimination techniques we can use both K-Nearest Neighbors and Linear Regression. For Forward Elimination Linear Regression, the highest score comes from RS, RA, W, OBP, SLG, BA, OOBP, and OSLG. This is also true for Backward Elimination Linear Regression. Forward Elimination KNN gave all groupings a score of 1.0 while in Backward Elimination KNN, the grouping of W, OBP, BA, and SLG had the highest score. Generally, Forward Elimination Linear Regression appears on the right track, though with only a score of 0.400552

For Filter-Based techniques, we use the ANOVA filter method. ANOVA is used because we are predicting for the Playoffs, which is a categorical variable. Setting the threshold at 40%, ANOVA gives us RS, OBP and OOBP as the most important variables. If we drop Year, Team, League, RankSeason, RankPlayoffs, and G, then we only get OOBP as the most important, suggesting that keeping opponents off bases as most important. Drop to a 30% threshold and you get RA, OOBP, BA, SLG, and RS as the important variables.

For Embedded Techniques, we can compare Lasso to Random Forest. Lasso doesn't appear to perform well given the scope of this project. It doesn't tell me much other than Wins are important. Random Forest, however, shows Wins being the most important while RS and RA being the next most important. 

# Determining Whether OBP and SLG Are Playoff Predictors

When plotting Wins versus RS, RA, RD, OBP, SLG, OOBP, and OSLG, we see there is a strong positive correlation between Wins and Run Differential. Wins and Runs Scored, OBP and SLG also have positive correlations, though less so. We also see somewhat strong negative correlations between Wins and Runs Against, OOBP and OSLG. Linear Regression formulas in other projects have shown that Runs Scored and Runs Against can be predicted using OBP aand SLG for Runs Scored, and OOBP and OSLG for Runs Against. Linear Regression on RD (Run Differential = RS - RA) in these projects have also shown that this can be a predictor for the number of games a team wins. Using the same methods, we will see if we can prove that these formulas predict Run Differential, Wins, and Playoff Appearances for three teams. The data for the three teams are already in the Baseball dataset for comparison. 
