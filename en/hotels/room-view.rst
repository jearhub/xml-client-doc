Views from the rooms of hotels
################

Description of XML schema
==========================

A request for a list of types is formed through URL (using GET method)

XSD-schema response :

- :download:`www/xsd/dict/room/RoomViewsResponse.xsd <../../themes/hotelbook/static/xsd/dict/room/RoomViewsResponse.xsd>`

Request
---------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/room_view``

Response, RoomViewsResponse
----------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <RoomViews>
            <RoomView id="..." name="...">...</RoomView > - list views
        </RoomViews>
    </Response>

Response item
----------------

Parent item.

**Attributes:** no.

**Child items:**

+---------------+--------------+------------------------------+
| Name          | Mandatory    | Description                  |
+===============+==============+==============================+
| RoomViews     | Yes          | list views from the room     |
+---------------+--------------+------------------------------+

RoomViews item
---------------------

Contains full list views from the rooms of hotels.

**Attributes:** no.

**A child item:**

+----------+--------------+-----------------------------------------------------------------------------+
| Name     | Mandatory    | Description                                                                 |
+==========+==============+=============================================================================+
| RoomView | No           | view from the room                                                          |
+----------+--------------+-----------------------------------------------------------------------------+

RoomView item
---------------

**Attributes:**

+------------+-----------+----------------------+------------------------------+
| Name       | Type		 |  Mandatory           | Description                  |
+============+===========+======================+==============================+
| id         | Numeric   |  Yes                 | identifier                   |
+------------+-----------+----------------------+------------------------------+
| name       | String    |  Yes                 | name of the species          |
+------------+-----------+----------------------+------------------------------+