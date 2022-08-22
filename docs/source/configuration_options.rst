Configuration options
=====================

Xforecast can be configured by editing the ``config.yaml`` file. The config.yaml file contains:

config.yaml
-----------

``prometheus_url`` - The url of prometheus 

``name`` - The metric name

``start_time`` - Start time in epoch format

``end_time`` - End time in epoch format

``query`` - Prometheus query used in http api

``forecast_every`` - At what interval the app should do the predictions in seconds

``forecast_basedon`` - Forecast based on past how many data points in seconds

``write_back_metric`` - Name given to the predicted metric

Here is an example of the configuration file:

.. code-block:: bash

    prometheus_url: http://localhost:9000

    metrics:
    - name: windows_cpu_time_total  
      start_time: '2022-08-08T09:57:00.000Z'
      end_time: '2022-08-08T09:58:00.000Z'
      query: avg+by(instance)+(windows_cpu_time_total{mode="idle"})
      forecast_every: 60 
      forecast_basedon: 60 
      write_back_metric: forecast_cpu_time 



