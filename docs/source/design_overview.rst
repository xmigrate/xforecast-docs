Design Overview
===============

Xforecast helps to predict the data points for a given time period of a metric. It learns from the past data points of that metric. We will be using pre-trained models for this purpose.

Architecture
------------

    .. image:: images/architecture.png
        :width: 400
        :align: center
        :alt: xforecast architecture diagram

Xforecast has the following components,

    1. Datastore
    2. Visualizer
    3. Forecaster

Datastore
---------

    .. image:: images/Prometheus.png
        :width: 150
        :align: center
        :alt: Prometheus Logo


We will be using prometheus as the supported datastore initially since the majority of the engineers uses this tool for 
collecting metrics from k8s cluster. Datastore will be used to query the datapoints of the metrics to be predicted by the forecaster. 
Datastore will be used by the forecaster to write the forecasted data points of that metrics.

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

Forecaster is an always-running application written Python. It reads the configurations such as the datastore url, metric name, 
training data hrs etc. from the config file. This config can be loaded as a configmap. Once the training is completed, 
it will start predicting the data points for x period in every y mins. Here x and y are loaded from the configuration. 
the predicted data points will be written back to the datastore.

ML model
--------

    .. image:: images/prophet.png
        :width: 250
        :align: center
        :alt: prophet Logo

The Prophet library is an open-source library designed for making forecasts for
univariate time series datasets. It is easy to use and designed to automatically find agood set of hyperparameters for the model in an effort to make skillful forecasts for
data with trends and seasonal structure by default