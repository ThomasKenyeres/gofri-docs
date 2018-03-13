Generator
=========

Each generated project has a ``generate.py`` in the root package.
It's a tool for rapid module generation for your project.

Main features:

Command: generate

Generate custom module:

.. code-block:: none

    generate
        module <name> <path>


Generate predefined modules:

.. code-block:: none

    generate
        controller <name>
        service <name>
        model <name>
        entity <name> [column names separated with space]


Example usage:

.. code-block:: none

    python3 generate.py generate entity dog name breed birth_year