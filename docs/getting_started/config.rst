Configuration file
==================

The main configuration file is ``conf.xml`` and it's in the root package.


HTTP
----

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

        ...

    </configuration>

If you leave ``<host>`` empty, the default is 127.0.0.1.


Dependencies
------------

.. code-block:: xml

    <configuration>
        <dependencies>
            <dependency>matplotlib</dependency>
            <dependency>pygame</dependency>
        </dependencies>

        ...

    </configuration>

This is how you can specify project dependencies in current version.
There will be more effective solutions for this purpose.

.. note::

    Dependencies are automatically installed at startup, if they are not installed yet.