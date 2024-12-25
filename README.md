# sandbox
This repo contains our approaches and solutions for the [Jane Street Real-Time Market Data Forecasting](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/overview) competition.

You can find following items:
- mono_model solutions
  - model_init
- multi_model solutions
  - model_init
- submission
  - example submission notebook

All the trained models and models for initialization are saved at `model_init`.

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

## Best models list

#### mono-model

LightGBM trained with all datasets (excepts for 3 and 7). The loss is RMSE. More details can be found in the [notebook](./best_model/lgbm_mono.ipynb).

The best model is avaiable [here](./best_model/jane_lgbm_baseline.txt).

The R2 score is 0.0037


#### hybrid-model

The best NN model is a MLP trained with all datasets . The loss is RMSE (R2 score cannot converge). More details can be found in the [notebook](./best_model/mlp_hybrid_low_mem.ipynb).

The best model is avaiable [here](./best_model/mlp_hidden_256_layer_2_rmse_lr_1e5_batch_norm_dropout.ckpt).

Here is a brief summary of its parameters:

|  | Name      | Type    | Params | Mode |
|- | -         | -       | -      | -    |
|0 | model     | Sequential | 87.0 K | train|
|1 | criterion | MSELoss    | 0      | train|

The R2 score is 0.0063.