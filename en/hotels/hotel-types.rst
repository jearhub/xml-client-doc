Types of hotels
###############

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/HotelTypeResponse.xsd``

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/hotel_type``

Response, HotelTypeResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <HotelTypes>
            <Type id="...">...</Type> - list of types of hotels
        </HotelTypes>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+--------------+-------------+-----------------+
| Name         | Mandatory   | Description     |
+==============+=============+=================+
| HotelTypes   | Yes         | List of types   |
+--------------+-------------+-----------------+

HotelTypes item
---------------

Contains full list of types of hotels.

**Attributes:** no.

**A child item:**

+------+-----------+------------------------+
| Name | Mandatory | Description            |
+======+===========+========================+
| Type | No        | Name of type           |
|      |           |                        |
|      |           | Attributes:            |
|      |           |                        |
|      |           | -  ``id`` - id of type |
+------+-----------+------------------------+
