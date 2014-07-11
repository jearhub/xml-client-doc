Room sizes
##########

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET method)

XSD-schema response :

- :download:`www/xsd/dict/room/RoomSizesResponse.xsd <../../themes/hotelbook/static/xsd/dict/room/RoomSizesResponse.xsd>`

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/room_size``

Response, RoomSizesResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <RoomSizes>
            <RoomSize id="..." name="..." pax="..." children="0|1" cots="0|1|2" search="0|1">...</RoomSize> - list of sizes
        </RoomSizes>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+-----------+-----------+--------------------+
| Name      | Mandatory | Description        |
+===========+===========+====================+
| RoomSizes | Yes       | List of room sizes |
+-----------+-----------+--------------------+

RoomSizes item
--------------

Contains full list of room sizes.

**Attributes:** no.

**A child item:**

+------------+-------------+------------------+
| Name       | Mandatory   | Description      |
+============+=============+==================+
| RoomSize   | No          | Room size name   |
+------------+-------------+------------------+

RoomSizes/RoomSize item
-----------------------

Room size name.

Optional item.

**Attributes:**

+------------+---------------+-------------+-----------------------------------------+
| Name       | Type          | Mandatory   | Description                             |
+============+===============+=============+=========================================+
| id         | Numeric       | Yes         | room size id                            |
+------------+---------------+-------------+-----------------------------------------+
| name       | String        | Yes         | Short name (SGL, DBL, DBL-SOLO, etc.)   |
+------------+---------------+-------------+-----------------------------------------+
| pax        | Numeric       | Yes         | Number of adults in the room            |
+------------+---------------+-------------+-----------------------------------------+
| children   | 0 or 1        | Yes         | Additional place for a child            |
+------------+---------------+-------------+-----------------------------------------+
| cots       | from 0 to 2   | Yes         | Number of cots in the room              |
+------------+---------------+-------------+-----------------------------------------+
| search     | 0 or 1        | Yes         | Can specify in search request           |
+------------+---------------+-------------+-----------------------------------------+

**Child items:** no.