====
Jana
====

.. image:: https://badge.fury.io/py/jana.png
    :target: http://badge.fury.io/py/jana

.. image:: https://travis-ci.org/petrilli/jana.png?branch=master
        :target: https://travis-ci.org/petrilli/jana

.. image:: https://pypip.in/d/jana/badge.png
        :target: https://pypi.python.org/pypi/jana


RESTful manager of secrets

* Free software: BSD license
* Documentation: https://jana.readthedocs.org.

Overview
--------

Jana enables developers, sysadmins, and users to store secrets in a trusted
system. If those secrets represent cryptographic keys, then Jana allows them
to be used to perform cryptographic operations within Jana. For secrets,
Jana supports the storage of individual secrets up to 8KiB. For cryptographic
keys, multiple key types and algorithms are supported.

Jana's individual "vaults" may contain a mix of keys and secrets, and
access control for the two types of object is independently controlled.


Elements
--------

Jana's architecture is composed of several elements:

* Users
* Vaults
* Secrets
* Keys
* Applications

Users are the top-level of the system. One or more users have access to manage
individuals vaults. Vaults are the overall container for secrets and keys.
Finally, applications are granted access to a vault.


Features
--------

Features can best be described as the actions one can do with various things
within the system. Users, assuming authorization, may:

* Manage keys using import, update, rotate, and delete operations;
* Manage secrets using get, set, and delete operations.

Keys are effectively specialized versions of secrets, where the metadata
associated with the secret is focused on that associated with cryptographic
algorithms.

In addition, the following are special areas of focus for the design and
implementation:

* Full auditing of all activities, both internally, and with optional remote
  storage.
* Careful validation of all input and output. Any instance of suspicious
  activity or input is immediately dropped and audit trails generated.


Limitations
-----------

* Currently, all authentication and authorization is self-contained within
  Jana. Whether this changes in the future is subject to consideration.
  Opening up is also increasing the threat model to encompass other systems.
* Many, many missing features.


Future Plans
------------

There are a lot of future plans, but the high-level ones are:

* Implement cryptographic operations that can be performed inside Jana so that
  keys never need to be disclosed.
* Cryptographicly-strong key generation.


Name
----

The name comes from Jana, the Etruscan goddess and consort of Janus.
Mythology says that she was the keeper of secrets, mysteries, and hidden
things. Her name, along with that of Janus, would pass on into Roman
mythology as so many things did.
