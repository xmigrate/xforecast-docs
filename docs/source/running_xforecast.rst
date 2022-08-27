Running Xforecast
=================

Xforecast can be run easily using the container image from xforecast docker registry. We recommend to
run the application with the docker-compose file which is provided in the application repo.
You can change the configuration in the ``config.yaml`` file.

Running with docker-compose
---------------------------
Pre-requisites
~~~~~~~~~~~~~~
    * docker and docker-compose

Execute the below commands to start xforecast application

.. code-block:: bash

    git clone https://github.com/xmigrate/xforecast.git
    cd xforecast
    docker-compose up -d

Running from source
-------------------
Pre-requisites
~~~~~~~~~~~~~~
    * python 3.7 or higher
    * connectivity with prometheus

install the required dependency by executing the code below

.. code-block:: bash

    pip3 install -r requirements.txt

Then run the app with below command. It looks for ``config.yaml`` in the same directory level of ``main.py``

.. code-block:: bash

    python3 main.py

Deployment using helm
-------------------
Pre-requisites
~~~~~~~~~~~~~~
    * helm 3
    * connectivity with prometheus
    * connectivity with kubernetes cluster
    
Execute the below commands to start xforecast application

.. code-block:: bash

    git clone https://github.com/xmigrate/xforecast.git
    cd xforecast/xforecast-helm

Then make necessary changes in ``values.yaml`` file. Add xforecast configuration in  ``values.yaml`` file under ``config`` section.

.. code-block:: bash

    helm install xforecast .