Configuration options
=====================
Xforecast takes configuration parameters from ``config.yaml`` file.
The ``config.yaml`` file contains:

Config yaml
-----------

``name`` - Name of the metric

``datastore`` - Dictionary containing the datastore details

  ``name`` - Datatsore name 

  ``url`` - Datastore url (Prometheus requires port specified in the url.)

  ``port`` - Datastore port (The below options are only required for influxdb.)

  ``user`` - Username

  ``pass`` - Password

  ``db_name`` - Database name

  ``measurement`` - Measurement name

``start_time`` - Start time in UTC

``end_time`` - End time in UTC

``query`` - Datastore query

``forecast_every`` - At what interval the app should do the predictions in seconds

``forecast_basedon`` - Forecast based on past how many seconds of data points

``write_back_metric`` - The name of the metric to write the predicted data points


Here is an example of the configuration file:

.. code-block:: bash

    metrics:
  - name: cpu_usage  #metric name in prometheus
    data_store : 
      name : influxdb   
      url: 192.168.1.9
      port: 8086
      user : admin
      pass : admin
      db_name : telegraf
      measurement : cpu
    start_time: '2022-09-14 11:19:00'
    end_time: '2022-09-14 11:20:00'
    query: SELECT mean("usage_idle") *-1 +100 FROM "autogen"."cpu" WHERE ("host" = 'ip-172-31-31-81') AND time >= '2022-09-14 11:19:00' AND time <= '2022-09-14 11:20:00' GROUP BY time(10s) 
    training_interval: 1h #amount of data should be used for training
    forecast_duration: 5m #How data points should be predicted, here it will predict for 5 mins
    forecast_every: 60 #At what interval the app do the predictions 
    forecast_basedon: 60 #Forecast based on past how many data points
    write_back_metric: forecast_cpu_use #Where should it write back the metrics
  - name: memory_usage  #metric name in prometheus
    data_store : 
      name : prometheus  
      url: http://192.168.1.9:9090
    start_time: '2022-09-14 11:19:00'
    end_time: '2022-09-14 11:20:00'
    query: 100 - ((node_memory_MemAvailable_bytes{instance="node-exporter:9100"} * 100) / node_memory_MemTotal_bytes{instance="node-exporter:9100"})
    training_interval: 1h #amount of data should be used for training
    forecast_duration: 5m #How data points should be predicted, here it will predict for 5 mins
    forecast_every: 60 #At what interval the app do the predictions 
    forecast_basedon: 60 #Forecast based on past how many data points
    write_back_metric: forecast_mem_usage #Where should it write back the metrics




