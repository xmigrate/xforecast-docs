Logging and Troubleshooting
===========================

Execute the below command to see the logs from xforecast app

.. code-block:: bash

    docker-compose -f xforecast

logs 
----
The log file shows whether the app is performing properly. By default, xforecast uses a simple basic logging configuration to print log messages to standard error. 
The output of the log file might look like this:

.. code-block:: bash

    19-Aug-22 17:50:02 - Reading configuration
    19-Aug-22 17:50:02 - Fetching data from prometheus
    19-Aug-22 17:50:02 - Fetching data from prometheus - Succes
    19-Aug-22 17:50:02 - Training ML model
    19-Aug-22 17:50:04 - n_changepoints greater than number of observations. Using 3.
    19-Aug-22 17:50:07 - Predicting future data points
    19-Aug-22 17:50:07 - Writing data to prometheus
    19-Aug-22 17:50:07 - <Response [204]>
    19-Aug-22 17:50:07 - Writing data to prometheus
    19-Aug-22 17:50:07 - <Response [204]>
    19-Aug-22 17:50:07 - Writing data to prometheus
    19-Aug-22 17:50:07 - <Response [204]>
    19-Aug-22 17:51:07 - Fetching data from prometheus

Below are some sample log messages:

``Reading configuration``: This means that the app is reading configuration parameters from the configuration file 

``Fetching data from prometheus``: This means that the data is fetched from prometheus 

``Training ML model``: ML model is trained for the first time when the app runs

``Retraining ML model``: This means that it retrained the existing model using new data

``<Response [204]>``: This means that the predicted data is successfully written to prometheus

``<Response [404]>``: This means that the data failed to write to prometheus

Known Errors
------------

``some error: data`` occurs when there's a problem with the prometheus or prometheus query used

``some error: yhat`` occurs when the data fetched from prometheus is too less or there is no data at all

``<Response [404]>`` occurs when the writing is failed. This can happen if the time you are writing is too far to the past or to the future
 

