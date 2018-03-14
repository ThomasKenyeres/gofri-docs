Filters
=======

What are these?
---------------

HTTP filters are tools for filtering requests and set different properties before the request handler functions run.
To setup a filter is very easy you just have to create a class with ``@GofriFilter()`` decorator.

.. code-block:: python



    @GofriFilter()
    class MyFilter(Filter):
        def filter(self, request, response):
            return self._continue(request, response)

.. tip::

    It's recommended to inherit your class from ``gofri.lib.http.filter.Filter``, but works anyway, so your IDE can easily recognize overrideable methods.

Methods of ``Filter`` class:

    * filter(request, response)
        The filtering logic should be implemented here, and to let the request go forward ``_continue(request, response)`` should be called.

    * _continue(request, response)
        When this method is called, the ``request`` and ``response`` is passed to the next filter or to a controller which has a method to handle requests on the specific url.


Filtering by urls
-----------------

By default a filter doesn't filter anything, it's configurable in the decorator ``GofriFilter()``.
The URLs which you want to filter are given in the decorator's ``urls`` value, which is a list with the given URLs in string format.

.. code-block:: python

    @GofriFilter(urls=["/vpost", "/send"])
    class MyFilter(Filter):
        def filter(self, request, response):
            return self._continue(request, response)


If you set ``@GofriFilter()`` decorator value ``filter_all`` to ``True``, the filter activates on all URL endpoints on the server.

.. code-block:: python

    @GofriFilter(filter_all=True)
    class MyFilter(Filter):
        def filter(self, request, response):
            return self._continue(request, response)




Specify order
-------------

You can configure that in which order do you want to make your filters work.
The lower the order value is, the sooner the filter works.

.. code-block:: python

    @GofriFilter(filter_all=True, order=1)
    class AFilter(Filter):
        ...

    @GofriFilter(filter_all=True, order=0)
    class BFilter(Filter):
        ...

In the example above, ``BFilter`` filters before ``AFilter``. The default order is ``0``.
If two filters has the same order, they are ranked by definition order in the code.

.. note::
    You don't have to specify the order of your filters strictly like ``0-1-2...``, it also works well with orders ``2-3-6``.