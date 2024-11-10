# sandbox
This repo contains our approaches and solutions for the [Jane Street Real-Time Market Data Forecasting](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/overview) competition.

You can find following items:
- mono_model solutions
- multi_model solutions
- example submission notebook

## Testing sumission API locally

In this [discussion](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/discussion/542022#3026394), the host of the competition explains how to test evaluation API directly:

- Reformat a subset of the train data into local copies of `test.parquet` and `lags.parquet`, partitioned by `date_id`.
- Update the data paths passed to `inference_server.run_local_gateway`.

Here is an example:
```py
import kaggle_evaluation.jane_street_inference_server

inference_server = kaggle_evaluation.jane_street_inference_server.JSInferenceServer(predict)

inference_server.run_local_gateway(
    (
        'test.parquet', # replaced by our custom test-set
        'lags.parquet',
    )
)
```
