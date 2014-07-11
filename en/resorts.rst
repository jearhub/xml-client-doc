List of resorts
###############

Description of XML schema
=========================

A request for a list of resorts is formed through URL (using GET
method)

XSD-schema response :

-  :download:`www/xsd/dict/geo/ResortsResponse.xsd <../themes/hotelbook/static/xsd/dict/geo/ResortsResponse.xsd>`

Request
-------

You can pass optional parameter ``country_id`` (limit the list of
resorts by specified country). Contains no parameters. Request is passed
via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/resorts``

Response, ResortsResponse
-------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Resorts>
            <Resort id="..." country="...">...</Resort> - full list of resorts
        </Resorts>

    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+-----------+-------------+-------------------+
| Name      | Mandatory   | Description       |
+===========+=============+===================+
| Resorts   | Yes         | List of resorts   |
+-----------+-------------+-------------------+

Resorts item
------------

Contains full list of resorts

**Attributes:** no.

**A child item:**

+--------+-----------+------------------------------------------------------+
| Name   | Mandatory | Description                                          |
+========+===========+======================================================+
| Resort | No        | Resort name Attributes:                              |
|        |           |                                                      |
|        |           | -  ``id`` - resort id                                |
|        |           | -  ``country`` - country id(which is located resort) |
+--------+-----------+------------------------------------------------------+




