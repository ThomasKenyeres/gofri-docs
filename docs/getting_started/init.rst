Initializing a project
======================

``$ python3 -m gofri.generate_project <project-name>`` is the common way to create a project,
which will have the following structure


The following is a SQL statement.

.. code-block:: none

   My-First-Project
    my_first_project
        __init__.py
        start.py
        conf.xml
        modules.py
        generate.py
        back
            __init__.py
            controller
                __init__.py
                ...
            dao
                __init__.py
                ...
            ...
        web
            <web content if needed>