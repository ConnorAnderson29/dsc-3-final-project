##  Pitch DS - Baseball Analytics | Connor Anderson, Werlindo Mangrobang 

## Presentation Slides
You may view a high-level summary of our project [here](
https://docs.google.com/presentation/d/1J-Z5fk1yK_eDGFtXMvaUAYLYH8LSZaeo9yV3E9rfO3g/edit?usp=sharing).


## Executive Summary
We identified opportunities to leverage public baseball metrics to identify classes of baseball pitches, based on their characteristics. We explore two specific business cases: 1. Identifying pitches based primarily on its physical characteristics, e.g., spin rate, velocity, among others. 2. Identifying what the forthcoming pitch would be, based on the game situation. For the former, we were able to achieve a classification accuracy of >85%. For the 2nd case, we were only able to achieve accuracy ~60%, though have ideas on supplemental data and analyses that may help improve.

## Methodology

### Business Understanding
Baseball is a sport with a rich culture of data analytics, and unsurprisingly much data is publicly available. With our interest in leveraging that data to explore a classification problems, we identified the following:
We explore two specific business cases:
1. Identifying pitches based primarily on its physical characteristics, e.g., spin rate, velocity, among others. The predicted classes were specific pitches: e.g., Four-Seam Fastball, Slider, Curveball, et al.
    - While major broadcast media already has this feature, there is an opportunity to enhance local broadcasts with real-time pitch identification for consumer consumption.
2. Identifying what the forthcoming pitch would be, based on the game situation. For this, we simplified our pitch classes to be rolled up into their respective 'families': Fastball, Changeup, and Breaking Ball.
    - Examples of value from being able to identify the forthcoming pitch include improved batting performance for the team at-bat, as well as entertainment opportunities, such as real-time gambling.

Given the above, we framed ourselves as consultants pitching potential products based on the above to Root Sports, the local broadcast partner for the Seattle Mariners.

### Data Understanding
We obtained data primarily from the Major League Baseball Stats API [http://statsapi.mlb.com/](http://statsapi.mlb.com/). We access the API exclusively through an open-source python wrapper `MLB-StatsAPI`.

### Data Preparation
To focus on our business case, we limited our dataset to the following parameters:
- Seattle Mariners games
- 2018 Regular Season games
- Individual play-by-play pitch level data

To the end of classifying pitches, we removed any data where pitch information was missing.

### Modeling
We explored various classification algorithms, including:
- Decision Tree
- Random Forest
- Gradient Boosted Trees
- XGBoost


### Evaluation
We tracked the following metrics to evaluate our training models:
- Accuracy
- F1 Score
- AUC

We used K-Fold Cross Validation (k=5) to evaluate versus our test data.

We also set aside a holdout dataset to assess our candidate model (Aug-Sept of the 2018 season).

### Work to Date and Future Work
Results:
1. Pitch Classification   
    -  We were able to achieve accuracy rates >85%, with our most successful model being gradient boosted trees-based.
2. Next Pitch Identification
    - At this time, we were able to achieve ~60% accuracy rate. Our next avenues of exploration into improving this include:  
        - **Incorporating hitter hot/code zones.** We know anecdotally that individual skill of the batter influences pitching strategy. There were _some_ pre-calculated hot/cold zone data in the API feed, but it was not consistently populated enough for our purposes. One potential task is to build our own hot/cold dataset.
        - **Pitcher Cluster.** Incorporating individual pitchers as features is way too granular an approach, but we theorized that classes of pitchers (e.g., starters, closers), have similar repertoires, and thus potentially similar pitching strategies. One way to label these classes may be to perform clustering on pitchers.
        
