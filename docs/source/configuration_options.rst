Configuration options
=====================
Xforecast takes configuration parameters from ``config.yaml`` file.
The ``config.yaml`` file contains:

Config yaml
-----------

``name`` - Name of the metric

``datastore`` - Definition for the datastore to be used

  ``name`` - Datastore name, influxdb or prometheus

  ``url`` - Datastore url (Prometheus requires port specified in the url, eg. http://<ip>:9090)

  ``port`` - Datastore port, only required for influxdb

  ``user`` - Username, only required for influxdb

  ``pass`` - Password, only required for influxdb

  ``db_name`` - Database name, only required for influxdb

  ``measurement`` - Measurement name of the metric, only required for influxdb

``start_time`` - Start time in UTC

``end_time`` - End time in UTC

``query`` - Datastore query

``forecast_every`` - At what interval the app should do the predictions in seconds

``forecast_basedon`` - Forecast based on past how many seconds of data points

``write_back_metric`` - Measurement name to be used for storing the forecasted metrics

``models`` - Definition for the ML model which will be used

    ``model_name`` - Name of the model to be used for this metric, available value is now only prophet

    ``hyperparameters`` - The parameters and values used for tuning the model (The parameters below are for the prophet model)

      ``changepoint_prior_scale`` - Determines the flexibility of the trend changes

      ``seasonality_prior_scale`` - Determines the flexibility of the seasonality changes

      ``holidays_prior_scale`` - Determines the flexibiity to fit the holidays

      ``changepoint_range`` - Specifies the proportion of history where the trend changes are applied

      ``seasonality_mode`` - Specifies the mode of seasonality applied during the model training

Here is an example of the configuration file:

.. code-block:: bash

    metrics:
  - name: cpu_usage  #metric name in influxdb
    data_store : 
      name : influxdb   
      url: localhost
      port: 8086
      user : admin
      pass : admin
      db_name : telegraf
      measurement : cpu
    start_time: '2022-09-14 11:19:00'
    end_time: '2022-09-14 11:20:00'
    query: SELECT mean("usage_idle") *-1 +100 FROM "autogen"."cpu" WHERE ("host" = 'host') AND time >= '2022-09-14 11:19:00' AND time <= '2022-09-14 11:20:00' GROUP BY time(10s) 
    forecast_every: 60 #At what interval the app do the predictions 
    forecast_basedon: 60 #Forecast based on past how many data points
    write_back_metric: forecast_cpu_use #Where should it write back the metrics
    models : 
      model_name: prophet
      hyperparameters:
        changepoint_prior_scale : 0.05 #determines the flexibility of the trend changes
        seasonality_prior_scale : 10 #determines the flexibility of the seasonality changes
        holidays_prior_scale : 10 #determines the flexibiity to fit the holidays
        changepoint_range : 0.8 #proportion of the history where the trend changes are applied
        seasonality_mode : additive #whether the mode of seasonality is additive or multiplicative
  - name: memory_usage  #metric name in prometheus
    data_store : 
      name : prometheus  
      url: http://localhost:9090
    start_time: '2022-09-14 11:19:00'
    end_time: '2022-09-14 11:20:00'
    query: 100 - ((node_memory_MemAvailable_bytes{instance="node-exporter:9100"} * 100) / node_memory_MemTotal_bytes{instance="node-exporter:9100"})
    forecast_every: 60 #At what interval the app do the predictions 
    forecast_basedon: 60 #Forecast based on past how many data points
    write_back_metric: forecast_mem_usage #Where should it write back the metrics
    models : 
      model_name: prophet
      hyperparameters:
        changepoint_prior_scale : 0.5 #determines the flexibility of the trend changes
        seasonality_prior_scale : 0.1 #determines the flexibility of the seasonality changes
        holidays_prior_scale : 10 #determines the flexibiity to fit the holidays
        changepoint_range : 0.95 #proportion of the history where the trend changes are applied
        seasonality_mode : multiplicative #whether the mode of seasonality is additive or multiplicative



