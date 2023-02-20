###############################################################################
                             TASK TRACKER SERVICE
###############################################################################

This project is done in addition to the `Python training course`_.
It demonstrates the abilities of the `Django`_ web framework.

.. _Django: https://djangoproject.com/
.. _Python training course: https://github.com/shorodilov/python-course/

And yes... This is another training todo-app in the internet.

Getting started
===============

#. Download the code repository to your local machine
#. Install all dependencies required by this project
#. Set up environment variables required by this project``
#. Run the project

The dependencies are listed in formats suitable for `pip`_ and `poetry`_
package managers.

.. _pip: https://pip.pypa.io/
.. _poetry: https://python-poetry.org/

Installing dependencies
-----------------------

To install the dependencies using pip do:

.. code-block::

    pip install -r requirements.txt

To do the same via poetry do:

.. code-block::

    poetry install

Setting up environment
----------------------

To set an environment variable use commands:

.. code-block::

    export VARIABLE=value  # Linux and MacOS
    set VARIABLE=value     # Windows

+-----------------------+-----------------------------------------------------+
| Variable name         | Description                                         |
+=======================+=====================================================+
| ``DJANGO_SECRET_KEY`` | The secret key is required by Django security       |
|                       | middleware. For the security reasons this can not   |
|                       | be shared across the internet, and should be setup  |
|                       | for each project individual instance separately.    |
|                       | Here is a good service to get it:                   |
|                       | https://djecrety.ir/                                |
+-----------------------+-----------------------------------------------------+

Running the project
-------------------

The development server may be run using the administrative script ``manage.py``
(this is the common way to run Django server for developers). Simply do:

.. code-block::

    python manage.py runserver

The output should look like:

::

    Django version 4.1.5, using settings 'tasktracker.settings'
    Starting development server at http://127.0.0.1:8000/
    Quit the server with CTRL-BREAK.

Visit the printed out address in your web browser to see the running Django
web site.

Project structure
=================

::

    /
    |- tasktracker
    |- tasks
    |- users

The *tasktracker* directory is the core of the project. It contains all general
settings and entry points (WSGI and ASGI).

The *tasks* directory is the home of the application responsible for tasks
management and visualization.

The *users* directory (application) maintains all work around user
representations.

Using Docker Compose
====================

**Prerequisites**:

- docker engine installed
- docker compose installed

This project comes with a docker compose file to deploy services recommended
for the Django training. If you are not familiar with docker compose, it is
a tool for containers management.

`Docker compose office docs <https://docs.docker.com/compose/>`_.

The installation process is described
`here <https://docs.docker.com/compose/install/>`_.

The compose file defines a minimalistic set of database server and GUI client
running in individual containers. You need to map ports from your machine to
docker containers to get things working well. Default mapped ports are:

- 5432 for the postgres service
- 5050 for the pgadmin service

You can change these values by modifying ``POSTGRES_PORT`` and/or
``PGADMIN_PORT`` environment variables.

The containers management is simple as:

.. code-block::

    docker compose up -d  # start all containers
    docker compose down   # stop all containers

PostgreSQL
----------

The ``db`` service will run the PostgreSQL server container. It exposes
5432-port to the host machine, so you can use it just as if you got postgres
running on your own system. The default ports mapping is "5432:5432".
In case you have already 5432-port occupied by other software, you may set up
any available port via ``POSTGRES_PORT`` environment variable.

The pre-defined credentials are:

:*username*: postgres
:*password*: postgres

You can run this service separately from other services defined in the compose
file by:

.. code-block::

    docker compose up -d db

pgAdmin
-------

pgAdmin is one of the most famous PostgreSQL clients. From the version 4.x it
uses a web-based UI running in your web browser. The pgAdmin container exposes
its 80-port to the host machine. By default, this port is mapped to 5050. In
case you have already 5050-port occupied by other software, you may set up any
available port by using ``PGADMIN_PORT`` environment variable. After running
the pgAdmin visit http://localhost:5050 in your web browser (adjust the port
number in case of need).

The pre-defined credentials to connect pgAdmin are:

:*email*:    pgadmin@pgadmin.org
:*password*: pgadmin

While connecting to the PostgreSQL server via pgAdmin the alias for the db
container is "postgresql-server". This connection is already defined in the
"pgadmin.config.json" file.

Note this may take some time to set up container and run internal server.
