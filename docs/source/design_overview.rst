Design Overview
===============

Xforecast is a predictive analytics tool which could learn from historical datapoints, understand the seasonality or pattern in the data so that it could predict the datapoints in future.
We will be using opensource ML models as well as custom ML models for this purpose.

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

    

Datastore can be a timeseries metricstore. Currently we support Influxdb and Prometheus.
The forecaster will be connected to the metricstore so that it can read and write data to the metricstore.

Visualizer
----------

    .. image:: images/grafana.jpg
            :width: 200
            :align: center
            :alt: Grafana image

We use Grafana to plot the graph against the actual data points and forecasted data points of the metrics. This can be the same grafana that the engineers already have in there environment.
Grafana can be used to set alerts to remediate the issue proactively with automated or manual means. It also doesn't mean that xforecast is tightly coupled to Grafana. The user have the freedom
to choose any data visualisation tool of his choice.

Forecaster
----------

    .. image:: images/python.png
        :width: 150
        :align: center
        :alt: python Logo

Forecaster is an always-running asynchronous application written in Python. It reads the definition for the metric forcasting from the config file. Such as the datastore url, metric name, 
hours of training data, etc. Once the training is completed, it will start predicting the data points for x period at every y mins. Here x and y are loaded from the configuration. 
The predicted data points will be written back to the datastore.

ML model
--------

    .. image:: images/prophet.png
        :width: 250
        :align: center
        :alt: prophet Logo

We currently only support the Prophet library which is an open-source ML library designed for making forecasts for time series datasets. It is easy to use and designed with tuneable hyperparameters
in order for the user to be able to find the best set of parameters for each model. We will have support for additional ML/Statistical models which will fit varieties of use cases.
