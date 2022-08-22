Running Xforecast
=================

Xforecast can be run easily using the container image from xforecast docker registry. We recommend to
run the application with docker-compose file which is provided in the application repo.
You can change the configuration in the ``config.yaml`` file.

Execute the below commands to start xforecast application

.. code-block:: bash

    git clone https://github.com/xmigrate/xforecast.git
    cd xforecast
    docker-compose up -d

Requirements
------------
    * python 3.7 or higher
    * python-snappy
    * pytest
    * pandas
    * pystan
    * prophet==1.0.1
    * pyyaml
    * requests
    * datetime
    * protobuf==3.20.0

**Or** install the required packages by executing the code below

.. code-block:: bash

    pip3 install -r requirements.txt
