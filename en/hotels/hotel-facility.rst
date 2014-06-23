Hotel facilities
################

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/HotelFacilityResponse.xsd``

Request
-------

Contains no parameters. Request is passed via the URL with credentials
(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/hotel_facility``

Response, HotelFacilityResponse
-------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <HotelFacilities>
            <Facility id="...">...</Facility> - list of hotel facilities
        </HotelFacilities>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+-------------------+-------------+----------------------------+
| Name              | Mandatory   | Description                |
+===================+=============+============================+
| HotelFacilities   | Yes         | List of hotel facilities   |
+-------------------+-------------+----------------------------+

HotelFacilities item
--------------------

Contains full list of hotel facilities.

**Attributes:** no.

**A child item:**

+----------+-----------+------------------------------------------------------+
| Name     | Mandatory | Description                                          |
+==========+===========+======================================================+
| Facility | No        | Hotel facility name                                  |
|          |           |                                                      |
|          |           | Attributes:                                          |
|          |           |                                                      |
|          |           | -  ``id`` - id of hotel facility                     |
+----------+-----------+------------------------------------------------------+
