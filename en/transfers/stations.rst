List of stations
################

Description of XML schema
=========================

A request for a list of stations is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/geo/StationsResponse.xsd <../../themes/hotelbook/static/xsd/dict/geo/StationsResponse.xsd>`

Request
-------

You can pass optional parameter ``country_id`` or ``resort_id`` or ``city_id`` (limit the list of stations by specified country or resort or city) Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/stations``

Response, StationsResponse
--------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Stations>
            <Station id="..." country="..." resort="..." city="..." name_ru="...">...</Station> - full list of stations
        </Stations>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+----------+-----------+------------------+
| Name     | Mandatory | Description      |
+==========+===========+==================+
| Stations | Yes       | List of stations |
+----------+-----------+------------------+

Stations item
-------------

Contain full list of stations.

**Attributes:** no.

**A child item:**

+---------+-----------+--------------+
| Name    | Mandatory | Description  |
+=========+===========+==============+
| Station | No        | Station name |
+---------+-----------+--------------+

Station item
------------

Contains the name of the station (English, French, German, Italian, etc.).

Optional item (absent if no station found).

**Attributes:**

+---------+---------+-----------+----------------------------------------------+
| Name    | Type    | Mandatory | Description                                  |
+=========+=========+===========+==============================================+
| id      | Numeric | Yes       | Station id                                   |
+---------+---------+-----------+----------------------------------------------+
| country | Numeric | Yes       | country id (which is located station)        |
+---------+---------+-----------+----------------------------------------------+
| resort  | Numeric | Yes       | resort id                                    |
+---------+---------+-----------+----------------------------------------------+
| city    | Numeric | Yes       | city id                                      |
+---------+---------+-----------+----------------------------------------------+
| name_ru | String  | Yes       | The station's name in Russian (may be empty) |
+---------+---------+-----------+----------------------------------------------+

**Child items:** no.
