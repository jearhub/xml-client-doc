Types of rooms
################

Description of XML schema
==========================

A request for a list of types is formed through URL (using GET method)

XSD-schema response :

- :download:`www/xsd/dict/room/RoomTypesResponse.xsd <../../themes/hotelbook/static/xsd/dict/room/RoomTypesResponse.xsd>`

Request
--------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/room_type``

Response, RoomTypesResponse
----------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <RoomTypes>
            <RoomType id="..." name="...">...</RoomType> - List of room types
        </RoomTypes>
    </Response>

Response item
----------------

Parent item.

**Attributes:** no.

**Child items:**

+---------------+--------------+------------------------------+
| Name          | Mandatory    | Description                  |
+===============+==============+==============================+
| RoomTypes     | Yes          | List of room types           |
+---------------+--------------+------------------------------+

RoomTypes item.
------------------

Contains full list of room types.

**Attributes:** no.

**A child item:**

+----------+--------------+-----------------------------------------------------------------------------+
| Name     | Mandatory    | Description                                                                 |
+==========+==============+=============================================================================+
| RoomType | No           | room type name                                                              |
+----------+--------------+-----------------------------------------------------------------------------+

RoomType item
---------------------

**Attributes:**

+------------+-----------+----------------------+------------------------------+
| Name       | Type		 |  Mandatory           | Description                  |
+============+===========+======================+==============================+
| id         | Numeric   |  Yes                 | room type id                 |
+------------+-----------+----------------------+------------------------------+
| name       | String    |  Yes                 | type name                    |
+------------+-----------+----------------------+------------------------------+