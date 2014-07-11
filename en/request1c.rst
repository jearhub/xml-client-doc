Request for invoice 1C
######################

Description of XML schema
=========================

A request for invoice is formed through URL (using GET method).

XSD-schema response:

:download:`www/xsd/Request1CResponse.xsd <../themes/hotelbook/static/xsd/Request1CResponse.xsd>`

Request
-------

A request with a single parameter ``order_id`` (id of order). Request is
passed via the URL with credentials (``login``, ``password``,
``checksum``,..).

Request path: ``/xml/request_1c?order_id=``

Response, Request1CResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Success>true</Success>
    </Response>

If successful the query returns an element of ``Success``. Otherwise -
the error in the ``Errors``. After the invoice in order, account
information will be available in the request ``OrderInfo``
(``Account_1C`` item).

Errors item
-----------
View :doc:`Error page <../errors>`