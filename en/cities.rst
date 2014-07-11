List of cities
##############

Description of XML schema
=========================

A request for a list of cities is formed through URL (using GET method)

XSD-schema response :

-  :download:`www/xsd/dict/geo/CitiesResponse.xsd <../themes/hotelbook/static/xsd/dict/geo/CitiesResponse.xsd>`

Request
-------

You can pass optional parameter ``country_id`` or ``resort_id`` (limit
the list of cities by specified country or resort) Request is passed via
the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/cities``

Response, CitiesResponse
------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Cities>
            <City id="..." country="..." resort="..." name_ru="...">...</City> - full list of cities
        </Cities>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+--------+-----------+----------------+
| Name   | Mandatory | Description    |
+========+===========+================+
| Cities | Yes       | List of cities |
+--------+-----------+----------------+

Cities item
-----------

Contain full list of cities.

**Attributes:** no.

**A child item:**

+--------+-------------+---------------+
| Name   | Mandatory   | Description   |
+========+=============+===============+
| City   | No          | City name     |
+--------+-------------+---------------+

City item
---------

Contains the name of the city (English, French, German, Italian, etc.).

Optional item (absent if no city found).

**Attributes:**

+------------------+-----------+-------------+---------------------------------------------+
| Name             | Type      | Mandatory   | Description                                 |
+==================+===========+=============+=============================================+
| id               | Numeric   | Yes         | city id                                     |
+------------------+-----------+-------------+---------------------------------------------+
| country          | Numeric   | Yes         | country id (which is located city)          |
+------------------+-----------+-------------+---------------------------------------------+
| resort           | Numeric   | Yes         | resort id                                   |
+------------------+-----------+-------------+---------------------------------------------+
| has_vehicle_rent | Numeric   | No          | car rental                                  |
+------------------+-----------+-------------+---------------------------------------------+
| hotel_count      | Numeric   | No          | Count of hotels                             |
+------------------+-----------+-------------+---------------------------------------------+
| name_ru          | String    | Yes         | The city's name in Russian (may be empty)   |
+------------------+-----------+-------------+---------------------------------------------+

**Child items:** no.