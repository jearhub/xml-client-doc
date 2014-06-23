List of hotels
##############

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/HotelListResponse.xsd``

Request
-------

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..). You can pass optional parameters:

-  ``?country_id=id``, list of hotel in the country;
-  ``?city_id=id``, list of hotel in the city;
-  ``?update="Y-m-d H:i:s"`` list of hotels updated after specified date.

One of the ``country_id`` or ``city_id`` is MANDATORY

Request path: ``/xml/hotel_list``

Response, HotelListResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?> 
    <Response>
        <HotelList>
            <Hotel name="..." id="..." city="..." cat="..." updated="..." date_create="..." assoc="0|1"> - full list of hotels
        </HotelList>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+-------------+-------------+------------------+
| Name        | Mandatory   | Description      |
+=============+=============+==================+
| HotelList   | Yes         | List of hotels   |
+-------------+-------------+------------------+

HotelList item
--------------

Contains full list of hotels.

**Attributes:** no.

**Child items:**

+---------+-------------+---------------+
| Name    | Mandatory   | Description   |
+=========+=============+===============+
| Hotel   | No          | Hotel         |
+---------+-------------+---------------+

Hotel item
----------

Optional item (absent if no hotels found).

**Attributes:**

+----------------+---------------------------------------------+-----------+------------------------------------------+
| Name           | Type                                        | Mandatory | Description                              |
+================+=============================================+===========+==========================================+
| name           | String                                      | Yes       | Hotel name                               |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| id             | Numeric                                     | Yes       | Hotel id                                 |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| city           | Numeric                                     | Yes       | City id (which is located hotel)         |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| cat            | Numeric from 1 to 5                         | Yes       | Hotel category id (from /xml/hotel\_cat) |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| updated        | unix time                                   | Yes       | Last update                              |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| date_create    | unix time                                   | Yes       | Date added                               |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| modifying type | 'add' or 'delete' or 'change' or 'undelete' | Yes       | Type of last modification                |
+----------------+---------------------------------------------+-----------+------------------------------------------+
| assoc          | 0 or 1                                      | Yes       | Has any association with providers       |
+----------------+---------------------------------------------+-----------+------------------------------------------+

**Hotel items:** no.