HTTP
====

The usage of http decorators and other tools.


Configuration
-------------

Host configuration is available in conf.xml:

.. code-block:: xml
    :emphasize-lines: 6, 7

    <configuration>
    <project>
        <app-path>example.app</app-path>
    </project>
    <hosting>
        <host></host>
        <port>8080</port>
    </hosting>

If you leave ``<host>`` empty, the default is 127.0.0.1.

HTTP controllers
----------------

Generate a controller (explained `here <Generator_>`__).


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