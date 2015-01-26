============
Dependencies
============

With something that is as security-sensitive as Jana, it is important to
carefully consider all third-party dependencies that are included.  So, in
addition to the existing Python standard library, the following libraries
are included.

`Flask`_
    Flask is a small web framework. One of the things going for it, and the
    reason it was chosen, is that it is very small, and therefore has limited
    functionality.

`Flask-Restless`_
    This library provides basic RESTfun API functionality.

`structlog`_
    While the standard library's `logging module`_ is sufficient for many
    applications, in this situation it was critical to be able to have very
    structured logging. This library was written specifically to allow for
    flexible, yet structured, logging. It is well tested.

`jsonschema`_
    Provides validation of `JSON Schema`_ descriptions of all REST calls.
    This allows us to ensure that nothing goes in or out of the system that
    isn't approved.

.. _structlog: https://pypi.python.org/pypi/structlog
.. _logging module: https://docs.python.org/3.4/library/logging.html
.. _Flask: http://flask.pocoo.org/
.. _jsonschema: https://pypi.python.org/pypi/jsonschema
.. _Flask-Restless: http://flask-restless.readthedocs.org/
.. _JSON Schema: http://json-schema.org/
