Hotel categories
################

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET
method)

XSD-schema response :

-  ``www/xsd/HotelCatResponse.xsd``

Request
-------

Contains no parameters. Request is passed via the URL with credentials
(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/hotel_cat``

Response, HotelCatResponse
--------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <HotelCategories>
            <Category id="...">...</Category> - list of hotel categories
        </HotelCategories>
    </Response>

Response item
-------------

Parent item.

**Attributes:**no.

**A child item:**

+-------------------+-------------+------------------------------------+
| Name              | Mandatory   | Description                        |
+===================+=============+====================================+
| HotelCategories   | Yes         | Contains full list of categories   |
+-------------------+-------------+------------------------------------+

HotelCategories item
--------------------

Contains full list of categories.

**Attributes:** no.

**A child item:**


+----------+-----------+------------------------------------------------------+
| Name     | Mandatory | Description                                          |
+==========+===========+======================================================+
| Category | No        | Category name                                        |
|          |           |                                                      |
|          |           | Attributes:                                          |
|          |           |                                                      |
|          |           | -  ``id`` - category id                              |
+----------+-----------+------------------------------------------------------+