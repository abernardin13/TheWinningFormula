# TheWinningFormula
Repository for Data Analytics project
TheWinningFormula consists of the 'Baseball' dataset in CSV form, pulled from https://www.kaggle.com/datasets/wduckett/moneyball-mlb-stats-19622012. It contains data on batting average, slugging, on-base percentage, runs for and against, win-loss record, opponents' on-base percentage, opponents' slugging for each Major League Baseball team from 1962 to 2012 and whether a team made the playoffs in those years.

The first ste

The first step is to identify whether the dataset is normally distributed. Histograms in Baseball.ipynb show this to be the case, regardless of the variable. However, when a Shapiro-Wilk test is performed on the dataset, the results indicate that the dataset is not normally distributed as the p-value is equal to 0.0.

