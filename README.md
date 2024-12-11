# sandbox
This repo contains our approaches and solutions for the [Jane Street Real-Time Market Data Forecasting](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/overview) competition.

You can find following items:
- mono_model solutions
  - model_init
- multi_model solutions
  - model_init
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

## Best models list

#### mono-model

LightGBM trained with all datasets (excepts for 7). The loss is RMSE. More details can be found in the [notebook](./mono_model/pipeline_LGBM_baseline.ipynb).

The best model is avaiable [here](./mono_model/model_init/jane_lgbm_baseline.txt).

The R2 score is 0.008053.


#### hybrid-model

The second best one is a GRU trained with all datasets (excepts for 7). The loss is RMSE (R2 score cannot converge). More details can be found in the [notebook](./hybrid_model/LGBM_GRU_low_mem.ipynb).

The best model is avaiable [here](./hybrid_model/model_init/jane_gru_layer_2_rmse).

The R2 score is -0.00103.

---------

The second best one is a MLP trained with all datasets (excepts for 7). The loss is RMSE (R2 score cannot converge). More details can be found in the [notebook](./hybrid_model/LGBM_MLP_low_mem.ipynb).

The best model is avaiable [here](./hybrid_model/model_init/jane_mlp_hidden_32_epoch_30.ckpt).

The R2 score is -0.00287.