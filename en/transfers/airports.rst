List of airports
===================================

Description of XML schema
=========================

**Contents**

`Request <#h-1>`_

`Response, AirportsResponse <#h-2>`_

`Response item <#h-2-1>`_

`Airports item <#h-2-2>`_

`Airport item <#h-2-3>`_

 A request for a list of airports is formed through URL (using GET
method)
 XSD-schema response :

:download:`www/xsd/dict/geo/AirportsResponse.xsd <../../themes/hotelbook/static/xsd/dict/geo/AirportsResponse.xsd>`

Request
-------

You can pass optional parameter ``country_id`` or ``resort_id`` or
``city_id`` (limit the list of airports by specified country or resort
or city) Request is passed via the URL with credentials (``login``,
``password``, ``checksum``,..).
 Request path: ``/xml/airports``

Response, AirportsResponse
--------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Airports>
            <Airport id="..." iata="..." country="..." resort="..." city="..." name_ru="..." gta="...">...</Airport> - full list of airports
        </Airports>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+------------+-------------+--------------------+
| Name       | Mandatory   | Description        |
+============+=============+====================+
| Airports   | Yes         | List of airports   |
+------------+-------------+--------------------+

Airports item
-------------

Contain full list of airports.

**Attributes:** no.

**A child item:**

+-----------+-------------+----------------+
| Name      | Mandatory   | Description    |
+===========+=============+================+
| Airport   | No          | Airport name   |
+-----------+-------------+----------------+

Airport item
------------

Contains the name of the airport (English, French, German, Italian,
etc.).

Optional item (absent if no airport found).

**Attributes:**

+------------+-----------+-------------+------------------------------------------------+
| Name       | Type      | Mandatory   | Description                                    |
+============+===========+=============+================================================+
| id         | Numeric   | Yes         | Airport id                                     |
+------------+-----------+-------------+------------------------------------------------+
| iata       | Numeric   | Yes         | Airport IATA code                              |
+------------+-----------+-------------+------------------------------------------------+
| gta        | Numeric   | Yes         | communications supplier GTA                    |
+------------+-----------+-------------+------------------------------------------------+
| country    | Numeric   | Yes         | country id (which is located airport)          |
+------------+-----------+-------------+------------------------------------------------+
| resort     | Numeric   | Yes         | resort id                                      |
+------------+-----------+-------------+------------------------------------------------+
| city       | Numeric   | Yes         | city id                                        |
+------------+-----------+-------------+------------------------------------------------+
| name\_ru   | String    | Yes         | The airport's name in Russian (may be empty)   |
+------------+-----------+-------------+------------------------------------------------+

**Child items:** no.
