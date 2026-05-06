.. _elhaz-generate-aws-config:

``elhaz generate-aws-config``
=============================

Synopsis
--------

.. code-block:: text

   elhaz generate-aws-config [OPTIONS]

Description
-----------

Print an AWS config file for all elhaz configs.  Each config becomes a
``[profile <name>]`` block whose ``credential_process`` points at this elhaz
installation.  Configs that fail to parse are skipped with a warning written
to stderr.

Region is determined per config: ``STS.region_name`` takes priority over
``Session.region_name``.  If neither is set, the ``region`` line is omitted
from that profile.

The ``credential_process`` command embeds the ``--socket-path`` value active
at generation time.  If you later run the daemon at a different socket path,
regenerate the file.

Options
-------

``--help``
   Show help message and exit.

Examples
--------

Write an AWS config file from all configured elhaz profiles:

.. code-block:: bash

   elhaz generate-aws-config > ~/.aws/config

Use a non-default socket path (e.g. inside a container):

.. code-block:: bash

   elhaz --socket-path /tmp/elhaz.sock generate-aws-config > ~/.aws/config

Preview output without overwriting the existing config:

.. code-block:: bash

   elhaz generate-aws-config
