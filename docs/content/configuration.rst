Configuration
=============

.. _configuration:


Configuration file
~~~~~~~~~~~~~~~~~~

Example

Here is minimal configuration file required:

.. code-block:: javascript

    {
      "projects": [
        {
          "name": "development",
          "secret": "secret",
          "namespaces": []
        }
      ]
    }


Description:

- **projects** - array of registered projects

There is also a possibility to override default SockJS-Tornado settings using Centrifuge
configuration file. Example:

.. code-block:: javascript

    {
        ...,
        "sockjs_settings": {
            "sockjs_url": "https://cdn.jsdelivr.net/sockjs/1.0/sockjs.min.js"
        }
    }


Here I set custom ``sockjs_url`` option, list of all available options can be found in sockjs-tornado source code: `show on Github <https://github.com/mrjoes/sockjs-tornado/blob/master/sockjs/tornado/router.py#L14>`_

Centrifuge runs a `tornado HTTPServer <http://www.tornadoweb.org/en/stable/httpserver.html#http-server>`_ under the hood. If you want to configure it you can do so via the ``tornado_settings``. Please note that the ``io_loop`` argument is not supported for now. Example:

.. code-block:: javascript

    {
        ...,
        "tornado_settings": {
            "xheaders": true
        }
    }

Centrifuge also allows to collect and export various metrics into Graphite.
You can configure metric collecting and exporting behaviour using ``metrics``
object in configuration JSON.

In example below I enable logging metrics, and export into https://www.hostedgraphite.com/ service
providing prefix, host and port to send metrics via UDP.

.. code-block:: javascript

    {
        ...,
        "metrics": {
            "log": true,
            "graphite": true,
            "graphite_host": "carbon.hostedgraphite.com",
            "graphite_port": 2003,
            "graphite_prefix": "MY_HOSTED_GRAPHITE_KEY.centrifuge",
            "interval": 30
        }
    }

Metrics will be aggregated in a 30 seconds interval and then will be sent into log and into Graphite.

At moment Centrifuge collects for each node:

* broadcast - time in milliseconds spent to broadcast messages (average, min, max, count of broadcasts)
* connect - amount and rate of connect attempts to Centrifuge
* transport - counters for different transports (websocket, xhr_polling etc)
* messages - amount and rate of messages published
* channels - amount of active channels
* clients - amount of connected clients
* unique_clients - amount of unique clients connected
* api - count and rate of admin API calls


Command-line options
~~~~~~~~~~~~~~~~~~~~

Centrifuge has several command line arguments.

``--config`` - path to configuration json file, by default ``config.json``

``--debug`` - run Centrifuge in Tornado debug mode - server will be reloaded when code changes.

``--port`` - port to bind (default ``8000``)

``--address`` - address to bind to

``--name`` - unique node name (optional) - will be used in web interface metric table or in graphite data path

``--web`` - optional path to serve Centrifuge web interface single-page application

Some other command line options come with engine - explore them using ``--help``, for example:

.. code-block:: bash

    CENTRIFUGE_ENGINE=redis centrifuge --help







