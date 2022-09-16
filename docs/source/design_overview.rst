Design Overview
===============

Xforecast can predict the data points for a given time period of a metric. It learns from the past data points of that metric. 
We will be using pre-trained models for this purpose.

Architecture
------------

    .. image:: images/architec.jpeg
        :width: 400
        :align: center
        :alt: xforecast architecture diagram

Components of xforecast are as below,

    1. Datastore
    2. Visualizer
    3. Forecaster

Datastore
---------

    .. image:: images/datastore.png
        :width: 350
        :align: center
        :alt: datastore logo

    

Datastore is a time-series database. We support Influxdb and Prometheus as our datastores.
The forecaster will be reading and writing data to the datastore.

Visualizer
----------

    .. image:: images/grafana.jpg
            :width: 200
            :align: center
            :alt: Grafana image

We use Grafana to plot the graph against the actual data points and forecasted data points of the metrics. This can be the same grafana that the engineers already have.
Grafana can be used to set alerts to remediate the issue proactively with automated or manual means.

Forecaster
----------

    .. image:: images/python.png
        :width: 150
        :align: center
        :alt: python Logo

Forecaster is an always-running asynchronous application written in Python. It reads the configurations such as the datastore URL, metric name, 
hours of training data, etc. from the config file. Once the training is completed, 
it will start predicting the data points for x period every y mins. Here x and y are loaded from the configuration. 
the predicted data points will be written back to the datastore.

ML model
--------

    .. image:: images/prophet.png
        :width: 250
        :align: center
        :alt: prophet Logo

We currently only support the Prophet library which is an open-source library designed for making forecasts for
univariate time series datasets. It is easy to use and designed to automatically find a good set of hyperparameters for the model in an effort to make skillful forecasts for
data with trends and seasonal structure by default.
We will have support for additional ML/Statistical models which will fit varieties of use cases.