List of locations
#################

Description of XML schema
=========================

A request for a list of locations is formed through URL (using GET method)

XSD-schema response :

- :download:`www/xsd/dict/geo/LocationResponse.xsd <../../themes/hotelbook/static/xsd/dict/geo/LocationResponse.xsd>`

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/location``

Response, LocationResponse
--------------------------

::

    <?xml version="1.0" encoding="utf-8"?> 
    <Response>
        <Locations>
            <Location id="..." city="..." is_gobal="0|1">...</Location> - full list of locations
        </Locations>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+-----------+-----------+---------------------------------+
| Name      | Mandatory | Description                     |
+===========+===========+=================================+
| Locations | Yes       | Contains full list of locations |
+-----------+-----------+---------------------------------+

Locations item
--------------

Contains full list of locations.

**Attributes:** no.

**A child item:**

+----------+-----------+---------------+
| Name     | Mandatory | Description   |
+==========+===========+===============+
| Location | No        | Location name |
+----------+-----------+---------------+

Location item
-------------

Contains name of location.

Optional item (absent if no location found).

**Attributes:**

+-----------+---------+-----------+---------------------------------------------------------------+
| Name      | Type    | Mandatory | Description                                                   |
+===========+=========+===========+===============================================================+
| id        | Numeric | Yes       | location id                                                   |
+-----------+---------+-----------+---------------------------------------------------------------+
| city      | Numeric | Yes       | city id(which is contains location)                           |
+-----------+---------+-----------+---------------------------------------------------------------+
| is_global | 0 or 1  | Yes       | if is_global=1, then the location is applicable to all cities |
+-----------+---------+-----------+---------------------------------------------------------------+

**Child items:** no.