sepadd -- SEPA Direct Debit XML
===============================

.. image:: https://travis-ci.org/raphaelm/python-sepadd.svg?branch=master
   :target: https://travis-ci.org/raphaelm/python-sepadd

.. image:: https://codecov.io/gh/raphaelm/python-sepadd/branch/master/graph/badge.svg
   :target: https://codecov.io/gh/raphaelm/python-sepadd

.. image:: http://img.shields.io/pypi/v/sepadd.svg
   :target: https://pypi.python.org/pypi/sepadd

This is a python implementation to generate SEPA direct debit XML files.

For now, this is basically a properly packaged, python 3 tested version 
of the `PySepaDD`_ implementation that was released by The Congressus under the MIT license.
Thanks for your work!

Limitations
-----------

Supported standards:

* SEPA PAIN.008.001.02
* SEPA PAIN.008.002.02
* SEPA PAIN.008.003.02

Usage
-----

Example:

.. code:: python

    from sepadd import SepaDD
    import datetime

    config = {
        "name": "Test von Testenstein",
        "IBAN": "NL50BANK1234567890",
        "BIC": "BANKNL2A",
        "batch": True,
        "creditor_id": "DE26ZZZ00000000000",  # supplied by your bank or financial authority
        "currency": "EUR"  # ISO 4217
    }
    sepa = SepaDD(config, schema="pain.008.002.02")

    payment = {
        "name": "Test von Testenstein",
        "IBAN": "NL50BANK1234567890",
        "BIC": "BANKNL2A",
        "amount": 5000,  # in cents
        "type": "RCUR",  # FRST,RCUR,OOFF,FNAL
        "collection_date": datetime.date.today(),
        "mandate_id": "1234",
        "mandate_date": datetime.date.today(),
        "description": "Test transaction"
    }
    sepa.add_payment(payment)

    print(sepa.export())


Credits and License
-------------------

Maintainer: Raphael Michel <mail@raphaelmichel.de>

Original Author: Congressus

License: MIT

.. _PySepaDD: https://github.com/congressus/PySepaDD
