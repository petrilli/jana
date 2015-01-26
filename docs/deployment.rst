==========
Deployment
==========

Proper deployment configuration is critical to a secure solution.  This
chapter contains detailed deployment recommendations.


Database
========

While it would have been possible to make Jana work with other databases,
there is only a single one supported: `PostgreSQL`_. In order to deploy Jana,
the following steps need to be followed.  Unlike most instructions, these will
guide you through using the `psql`_ command-line interface (CLI), rather than
the administrative commands.

Initial Setup
-------------

First, you need to create two distinct users in PostgreSQL. The easiest way
to do this is to launch ``psql`` as a `database superuser`_::

    $ psql -U postgres
    psql (9.4.0)
    Type "help" for help.

    postgres=#

From here, we can `create the users`_ we need::

    CREATE USER jana_admin WITH LOGIN ENCRYPTED PASSWORD '<something>';
    CREATE USER jana WITHLOGIN ENCRYPTED PASSWORD '<somethingdifferent>';

In each case, you should replace the ``<something>`` or ``<somethingdifferent>``
with the actual passwords.  These should be as strong as possible and not
guessable.

Next, we need to `create the database`_::

    CREATE DATABASE jana ENCODING 'UTF8';

This will create a UTF-8 encoded database. This allows us to safely store
strings with non-ASCII characters in them.


Table Migration
---------------

The schema for Jana is managed through controlled migrations. These reflect
incremental changes to the database that mirror the underlying code
development. They are managed using the `Alembic`_ library.


Permissions Management
----------------------

One of the things you should do once the initial tables are created is adjust
the permissions. Unfortunately, the standard migrations and table creation
scripts assume a single user with full access to the database. This isn't the
best way to handle things from a security perspective. Instead, we want to
remove some permissions from certain tables from the normal "session" user,
``jana``. Once again, at a superuser prompt for ``psql``, we want to `revoke`_
permissions::

    REVOKE ALL PRIVILEGES ON TABLE audit FROM jana;

Now, we want to `restore`_ just the permissions we want the user to have::

    GRANT SELECT ON TABLE audit TO jana;
    GRANT INSERT ON TABLE audit TO jana;


.. _PostgreSQL: http://www.postgresql.org/
.. _psql: http://www.postgresql.org/docs/9.4/static/app-psql.html
.. _database superuser: http://www.postgresql.org/docs/9.4/static/app-createuser.html
.. _create the users: http://www.postgresql.org/docs/9.4/static/sql-createrole.html
.. _create the database: http://www.postgresql.org/docs/9.4/static/sql-createdatabase.html
.. _Alembic: https://pypi.python.org/pypi/alembic
.. _restore: http://www.postgresql.org/docs/9.4/static/sql-grant.html
.. _revoke: http://www.postgresql.org/docs/9.4/static/sql-revoke.html
