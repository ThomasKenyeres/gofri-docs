HTTP request handling
=====================

The usage of http decorators and other tools.


Configuration
-------------

HTTP configuration is available in `conf.xml <../getting_started/config.html#http>`__

HTTP controllers
----------------

Generate a controller (explained `here <../getting_started/generator.html>`_).


Decorator usage
---------------

Use the ``gofri.lib.decorate.http`` module.

.. code-block:: python

    from gofri.lib.decorate.http import GET, POST


:@GET: \

    .. code-block:: python
        :emphasize-lines: 1

        @GET(path="/people")
        def get_people():
            return [Person("Jane"), Person("Jack")]


    .. code-block:: python
        :emphasize-lines: 1

        @GET(path="/person")
        def get_person(person_id):
            return person_service.get(person_id)


    Requires request parameter: ``<host>/person?person_id=1``

:@POST: \
    ``@POST`` works the same way as ``@GET`` in ``v1.0.1``, and all kind of request data can be accessed as in Flask.

:More:

    ``@HEAD``, ``@PUT`` and ``@DELETE`` is also available, currently they work the same way as ``@POST``.