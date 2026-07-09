# IPL First Innings Score Prediction

Predicts the first innings score in an IPL cricket match using historical match data (2008–2017).

## Dataset
- `ipl.csv` — 76,014 rows, 15 columns (match id, date, venue, teams, batsman/bowler, runs, wickets, overs, runs/wickets in last 5 overs, total).

## Workflow
1. **Data Cleaning**
   - Dropped irrelevant columns (`mid`, `venue`, `batsman`, `bowler`, `striker`, `non-striker`)
   - Kept only 8 consistent IPL teams
   - Removed first 5 overs of each innings (unstable early data)
   - Converted `date` to datetime
2. **Data Preprocessing**
   - One-hot encoded `bat_team` and `bowl_team`
   - Train/test split by season: train = 2008–2016, test = 2017
3. **Model Building** — compared:
   - Linear Regression ✅ (best performer)
   - Decision Tree Regression
   - Random Forest Regression
   - AdaBoost (with Linear Regression as base) — no significant improvement
4. **Final Model**: Linear Regression, used for predictions

## Prediction Function
```python
predict_score(batting_team, bowling_team, overs, runs, wickets, runs_in_prev_5, wickets_in_prev_5)
```
Returns a predicted final score (used as `score-10` to `score+5` range).

## Sample Results
Tested on 2018–2019 IPL matches; predicted ranges closely matched actual final scores (e.g., predicted 159–174 vs actual 169).

## Requirements
```
pandas
numpy
scikit-learn
matplotlib
seaborn
```

## Note
IPL scores are inherently volatile — predictions are estimates, not guarantees.
