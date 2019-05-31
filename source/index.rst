.. TradeSafe API User Guide master file, created by
   sphinx-quickstart on Fri Feb 10 10:58:03 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

TradeSafe API User Guide
========================

The `TradeSafe`_ API User Guide outlines the steps needed to start using our API
in your business.

The source code for the Documentation is `available on GitHub`_ and we welcome
contributions.

.. _TradeSafe: https://www.tradesafe.co.za
.. _available on GitHub: https://github.com/tradesafe/api-guide

.. _user-docs:

.. toctree::
    :maxdepth: 2
    :glob:
    :caption: User Documentation:

    getting_started
    create_key
    callback

.. _api-docs:

.. toctree::
    :maxdepth: 2
    :glob:
    :caption: API - Users

    validate_user
    create_user
    link_account


.. toctree::
    :maxdepth: 2
    :glob:
    :caption: API - Contracts

    validate_trade
    create_trade
    retrieve_trade
    complete_trade
    complete_milestone

.. _var-docs:

.. toctree::
    :maxdepth: 2
    :glob:
    :caption: API - Variables:

    get_constants
    variables
