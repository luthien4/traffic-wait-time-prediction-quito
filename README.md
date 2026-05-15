# Traffic Waiting Time Prediction in Quito

Regression project focused on predicting how long taxi passengers are likely to remain completely stopped in traffic during a trip in Quito, Ecuador.

## Business Problem

A taxi app wants to estimate traffic waiting time more accurately so passengers can better anticipate delays and the company can better understand trips affected by congestion.

The target variable is `wait_sec`, measured in seconds. It represents the time a taxi was completely stationary during a trip.

## Project Highlights

- Cleaned taxi trip data using Quito geographic bounds and physically meaningful trip rules.
- Treated unrealistic trip-estimate outliers using implied estimated speed.
- Engineered temporal, route, distance, and speed-based features.
- Explored geographic trip patterns with static plots and an interactive Folium map.
- Compared multiple regression models.
- Tuned the best model family with `RandomizedSearchCV`.
- Saved the final model pipeline and generated test predictions.

## Final Model

The final selected model is a tuned `HistGradientBoostingRegressor` inside a scikit-learn pipeline.

| Dataset | MAE | RMSE | R2 |
|---|---:|---:|---:|
| Validation set | 147.20 sec | 227.96 sec | 0.377 |
| External holdout set | 145.55 sec | 216.76 sec | 0.389 |

The model predicts typical traffic waiting time with an average error of about 2.4 minutes.

## Key Predictors

Permutation importance showed that the most important predictors were:

- estimated trip duration
- pickup longitude
- estimated speed
- dropoff longitude
- pickup day of week
- pickup latitude
- dropoff latitude
- longitude displacement
- pickup hour
- distance

These results suggest that traffic waiting time is influenced by trip scale, geography, route characteristics, and temporal context.

## Repository Structure

```text
traffic-wait-time-prediction-quito/
  data/
    data_train.csv
    features_test.csv
    features_aim.csv
    target_aim.csv
    Traffic Volume - Description.pdf
  notebooks/
    01_traffic_wait_time_prediction_quito.ipynb
  models/
    traffic_wait_time_model.pkl
  reports/
    quito_trip_locations_map.html
    traffic_wait_time_predictions.csv
    figures/
  README.md
  requirements.txt
```

## Main Notebook

The full analysis is available in:

[notebooks/01_traffic_wait_time_prediction_quito.ipynb](notebooks/01_traffic_wait_time_prediction_quito.ipynb)

## Map Attribution

**Map attribution:** Interactive maps were created with Folium using CARTO basemap tiles and OpenStreetMap data. Map attribution is displayed directly on the interactive map.

## Possible Next Improvements

- Add external traffic, weather, or event data.
- Engineer distance to airport or distance to city center.
- Use map-based clustering of pickup and dropoff areas.
- Test time-based validation instead of random validation.
- Build prediction intervals to communicate uncertainty.
- Deploy the model in a small Streamlit demo.
