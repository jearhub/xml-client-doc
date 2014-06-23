Hotel description
#################

Description of XML schema
=========================

A request is formed through URL (using GET method) XSD-schema response :

-  ``www/xsd/HotelDetailResponse.xsd``

Request
-------

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..). You must pass one of the mandatory parameters:

-  ``?hotel_id=id``
-  ``?hotel_name=name``

The name and id of the hotel you can get from the list of available
hotels (/xml/hotel\_list request).

Request path: ``/xml/hotel_detail``

Response, HotelDetailResponse
-----------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        [<Errors><Error code="..." desctiption="error text"></Errors>]
        <HotelDetail id="..." name="hotel name">
            <Country id="...">country name</Country>
            <City id="...">city name</City>
            <Cat id="...">category (stars)</Cat>
            <Locations>
                <Location id="...">location name</Location>
            </Locations>
            <Address>hotel address</Address>
            <Phone>phone</Phone>
            <Fax>fax</Fax>
            <Email>email</Email>
            <WWW>web-site</WWW>
            <Latitude>latitude</Latitude>
            <Longitude>longitude</Longitude>
            <BuiltIn>building year</BuiltIn>
            <BuildingType>building type</BuildingType>
            <NumberLifts>number of lifts</NumberLifts>
            <NumberFloors>number of floors</NumberFloors>
            <Conference>number of conference-rooms</Conference>
            <Voltage>voltage</Voltage>
            <ChildAgeFrom>minimum age of child</ChildAgeFrom>
            <ChildAgeTo>maximum age of child</ChildAgeTo>
            <Classification>classification</Classification>
            <EarlestCheckInTime>earliest check in time</EarlestCheckInTime>
            <RoomServiceFrom>room service from time</RoomServiceFrom>
            <RoomServiceTo>room service to time</RoomServiceTo>
            <RoomService24h>room service 24 hours</RoomService24h>
            <PorterageFrom>porterage from time</PorterageFrom>
            <PorterageTo>porterage to time</PorterageTo>
            <Porterage24h>porterage 24 hours</Porterage24h>
            <IndoorPool>number of indoor pools</IndoorPool>
            <OutdoorPool>number of outdoor pools</OutdoorPool>
            <ChildrensPool>number of children's pool</ChildrensPool>
            <Description>hotel description</Description>
            <Distances>distance to objects</Distances>
            <HotelFacility>
                <Facility id="...">facility name</Facility> - list of hotel facilities
            </HotelFacility>
            <RoomAmenity>
                <Amenity id="...">amenity name</Amenity> - list of room amenities
            </RoomAmenity>
            <HotelType>
                <Type id="..">hotel type</Type>
            </HotelType>
            <Images> - list of hotel photos
                <Image>
                    <Info>photo description</Info>
                    <Small width="..." height="...">thumbnail url</Small>
                    <Large width="..." height="...">image url</Large>
                </Image>
            </Images>
            <GTAHotelCode>hotel code</GTAHotelCode>
            <GTACityCode>city code</GTACityCode>
            <Updated>date update</Updated>
        </HotelDetail>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+---------------+-------------+---------------+
| Name          | Mandatory   | Description   |
+===============+=============+===============+
| HotelDetail   | Yes         | Information   |
+---------------+-------------+---------------+

HotelDetail item
----------------

Contains hotel details.

**Attributes:**

+--------+-----------+-------------+---------------+
| Name   | Type      | Mandatory   | Description   |
+========+===========+=============+===============+
| id     | Numeric   | Yes         | hotel id      |
+--------+-----------+-------------+---------------+
| name   | String    | Yes         | hotel name    |
+--------+-----------+-------------+---------------+

**Child items:**

+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Name               | Type                                                             | Mandatory | Description                                        |
+====================+==================================================================+===========+====================================================+
| Country            | String                                                           | Yes       | Country name Attributes: id - country id           |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| City               | String                                                           | Yes       | City name Attributes: id - city id                 |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Cat                | String                                                           | Yes       | Hotel category name Attributes: id - category id   |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Locations          | Nested                                                           | Yes       | List of locations                                  |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Address            | String                                                           | Yes       | Hotel address                                      |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Phone              | String                                                           | Yes       | Hotel phone                                        |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Fax                | String                                                           | Yes       | Fax                                                |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Email              | String                                                           | Yes       | Email                                              |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| WWW                | String                                                           | Yes       | Web-site                                           |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Latitude           | String                                                           | Yes       | Latitude                                           |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Longitude          | String                                                           | Yes       | Longitude                                          |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| BuildIn            | Numeric                                                          | Yes       | Building year. 0 - unknown                         |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| BuildingType       | traditional, historic, modern                                    | Yes       | Building type                                      |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| NumberLifts        | Numeric                                                          | Yes       | Number of lifts                                    |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| NumberFloors       | Numeric                                                          | Yes       | Number of floors                                   |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Conference         | Numeric                                                          | Yes       | Number of conference-rooms                         |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Voltage            | Numeric                                                          | Yes       | Voltage                                            |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| ChildAgeFrom       | Numeric                                                          | Yes       | Minimum age of child                               |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| ChildAgeTo         | Numeric                                                          | Yes       | Maximum age of child                               |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Classification     | First, Super First, Tourist, Super Tourist, Deluxe, Super Deluxe | Yes       | GTA classification                                 |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| EarlestCheckInTime | Time, pattern "H:i:s"                                            | Yes       | Earliest Check In Time                             |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| RoomServiceFrom    | Time, pattern "H:i:s"                                            | Yes       | Room service from time                             |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| RoomServiceTo      | Time, pattern "H:i:s"                                            | Yes       | Room service to time                               |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| RoomService24h     | YES or NO                                                        | Yes       | Room service 24 hours                              |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| PorterageFrom      | Time, pattern "H:i:s"                                            | Yes       | Porterage from time                                |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| PorterageTo        | Time, pattern "H:i:s"                                            | Yes       | Porterage to time                                  |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Porterage24h       | YES or NO                                                        | Yes       | Porterage 24 hours                                 |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| IndoorPool         | Numeric                                                          | Yes       | Number of indoor pools                             |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| OutdoorPool        | Numeric                                                          | Yes       | Number of outdoor pools                            |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| ChildrensPool      | Numeric                                                          | Yes       | Number of children's pool                          |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Description        | String                                                           | Yes       | Hotel description                                  |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Distances          | String                                                           | Yes       | List of distance to objects (airport, beach, etc.) |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| HotelFacility      | Nested                                                           | Yes       | Hotel facilities                                   |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| RoomAmenity        | Nested                                                           | Yes       | Room amenities                                     |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| HotelType          | Nested                                                           | Yes       | Hotel type                                         |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Images             | Nested                                                           | Yes       | Hotel photos                                       |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| GTAHotelCode       | String                                                           | Yes       | GTA Hotel code                                     |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| GTACityCode        | String                                                           | Yes       | GTA City code                                      |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+
| Updated            | Date, pattern "Y-m-d H:i:s"                                      | Yes       | Last update                                        |
+--------------------+------------------------------------------------------------------+-----------+----------------------------------------------------+

HotelDetail/Locations item
--------------------------

Locations near the hotel.

Attributes: no.

Child items:

+----------+--------+-----------+-----------------------------------------------+
| Name     | Type   | Mandatory | Description                                   |
+==========+========+===========+===============================================+
| Location | String | Yes       | Location name Attributes: id - id of location |
+----------+--------+-----------+-----------------------------------------------+

HotelDetail/HotelFacility item
------------------------------

List of hotel facilities.

Attributes: no.

Child items:

+----------+--------+-----------+---------------------------------------------------------+
| Name     | Type   | Mandatory | Description                                             |
+==========+========+===========+=========================================================+
| Facility | String | Yes       | Name of the facility Attributes: id - hotel facility id |
+----------+--------+-----------+---------------------------------------------------------+

HotelDetail/RoomAmenity item
----------------------------

List of room amenities.

Attributes: no.

Child items:

+---------+--------+-----------+-------------------------------------------------+
| Name    | Type   | Mandatory | Description                                     |
+=========+========+===========+=================================================+
| Amenity | String | Yes       | Name of the amenity Attributes: id - amenity id |
+---------+--------+-----------+-------------------------------------------------+

HotelDetail/HotelType id
------------------------

Hotel type.

Attributes: no.

Child items:

+------+--------+-----------+----------------------------------------------------+
| Name | Type   | Mandatory | Description                                        |
+======+========+===========+====================================================+
| Type | String | Yes       | Name of the type of hotel Attributes: id - type id |
+------+--------+-----------+----------------------------------------------------+

HotelDetail/Images item
-----------------------

List of hotel photos.

Attributes: no.

Child items:

+-------+--------+-----------+-------------+
| Name  | Type   | Mandatory | Description |
+=======+========+===========+=============+
| Image | Nested | Yes       | Information |
+-------+--------+-----------+-------------+

HotelDetail/Images/Image item
-----------------------------

Image name.

Attributes: no.

Child items:

+-------+--------+-----------+---------------------------+
| Name  | Type   | Mandatory | Description               |
+=======+========+===========+===========================+
| Info  | String | Yes       | Photo description         |
+-------+--------+-----------+---------------------------+
| Small | String | Yes       | Thumbnail URL             |
|       |        |           |                           |
|       |        |           | Attributes:               |
|       |        |           |                           |
|       |        |           | * width - numeric,        |
|       |        |           | * px height - numeric, px |
+-------+--------+-----------+---------------------------+
| Large | String | Yes       | URL                       |
|       |        |           |                           |
|       |        |           | Attributes:               |
|       |        |           |                           |
|       |        |           | * width - numeric, px     |
|       |        |           | * height - numeric, px    |
+-------+--------+-----------+---------------------------+
