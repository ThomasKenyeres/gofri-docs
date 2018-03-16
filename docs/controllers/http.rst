HTTP request handling
=====================

Configuration
-------------

Configuration with `conf.xml <../getting_started/config.html#http>`__

HTTP controllers
----------------

HTTP controllers are modules which are responsible for receiving requests and sending responses to a client through HTTP connection.

.. tip::
     It's recommended to separate some request handler functions into more controllers to avoid too big, messy files.

:Generate a controller:

    The common way to create a controller is using `generate.py <../getting_started/generator.html>`_ for this purpose: \

    ``$ python3 generate.py generate controller <name>``


Decorator usage
---------------

The basic gofri HTTP decorators are in the ``gofri.lib.decorate.http`` module, \
and they are responsible for route management. They are ``GET``, ``POST``, ``PUT``, ``HEAD`` and ``DELETE`` \
depending on what request method do you want to accept on the endpoint.

.. code-block:: python

    from gofri.lib.decorate.http import GET, POST, PUT, HEAD, DELETE




This is the first (positional) argument, which is always required:

    * ``path``
        Defines the url path of the given endpoint, you can also define path variables: ``path="/people/<person_id>"``, \
        which have to be the first arguments of the decorated function (They are positional arguments of the function).

        Example usage with ``@GET``:

        .. code-block:: python

            @GET(path="people/<person_id>")
            def get_person(person_id):
                return person_service.get(person_id)

The remaining variables are strings which contain the names of the request part attributes seperated by semicolons(``;``).
Example usage: ``header='username;password'``. The decorated function expects arguments with the defined names, \
so avoid using the same names even in different decorator values!

    * ``params``
        The variables defined here are the path parameters of a request, e.g. ``/search?keyword=house&where=images`` \
        so the function's arguments would be ``keyword`` and ``where``.
    * ``headers``
        The request header parameters are defined in this string.



:@GET: \

    .. code-block:: python
        :emphasize-lines: 1

        @GET("/people")
        def get_people():
            return [Person("Jane"), Person("Jack")]


    .. code-block:: python
        :emphasize-lines: 1

        @GET(path="/person", params="person_id")
        def get_person(person_id):
            return person_service.get(person_id)



    Example: ``<host>/person?person_id=1``

:@POST: \

    ``@POST`` has additional input values like:

        * body
            Contains the request body.

            .. code-block:: python
                :emphasize-lines: 1

                @POST(path="/add", body="name;age")
                def add_person(name, age):
                    person_service.add(Person(name, age))



        * json
            Contains the request body if it's in ``application/json`` format:

            .. code-block:: python
                :emphasize-lines: 1

                @POST(path="/add_more", json="people")
                def add_people(people):
                    person_service.add_more(people)

            Request body (``application/json``):

            .. code-block:: json

                {
                    "people": [
                        {"name": "John", "age": 23},
                        {"name": "Jane", "age": 18},
                        {"name": "Jack", "age": 34}
                    ]
                }


    ``headers`` example:

    .. code-block:: python
        :emphasize-lines: 1

        @POST(path="/auth", headers="name;password")
        def auth(name, password):
            return service.auth()




    You can also use more request part decorator value at once:

    .. code-block:: python
        :emphasize-lines: 1

        @POST(path="/library/<room_id>", json="books", params="note"):
        def add_books(room_id, books, note):
            library.rooms[room_id].add_books(books, note)



:More:

    ``@HEAD``, ``@PUT`` and ``@DELETE`` is also available, they work the same way as ``@POST``.

.. note::
    The big advantage of ``Gofri``'s HTTP decorators is that you don't have to read different request parts \
    inside the function because you have them as parameters.
    If you want to use request parts differently, do as you would do it in ``Flask``.