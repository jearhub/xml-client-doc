Room amenities
##############

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET method)

XSD-schema response :

- :download:`www/xsd/dict/room/RoomAmenityResponse.xsd <../../themes/hotelbook/static/xsd/dict/room/RoomAmenityResponse.xsd>`

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/room_amenity``

Response, RoomAmenityResponse
-----------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <RoomAmenities>
            <Amenity id="...">...</Amenity> - list of room amenities
        </RoomAmenities>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+-----------------+-------------+--------------------------+
| Name            | Mandatory   | Description              |
+=================+=============+==========================+
| RoomAmenities   | Yes         | List of room amenities   |
+-----------------+-------------+--------------------------+

RoomAmenities item
------------------

Contains full list of room amenities.

**Attributes:** no.

**A child item:**

+----------+-----------+------------------------------------------------------+
| Name     | Mandatory | Description                                          |
+==========+===========+======================================================+
| Amenity  | No        | Room amenity name                                    |
|          |           |                                                      |
|          |           | Attributes:                                          |
|          |           |                                                      |
|          |           | -  ``id`` - room amenity id                          |
+----------+-----------+------------------------------------------------------+