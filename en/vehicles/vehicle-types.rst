List of the vehicle types
#########################

Description of XML schema
=========================

A request for a list of transfer vehicles is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/vehicle/VehicleTypesResponse.xsd <../../themes/hotelbook/static/xsd/dict/vehicle/VehicleTypesResponse.xsd>`

Request
-------

Request is passed via the URL with credentials (``login``, ``password``,``checksum``,..).

Request path: ``/xml/vehicle_types``

Response, VehicleTypesResponse
------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <VehicleTypes>
            <VehicleType 
                    id="..." 
                    name_ru="..." 
                    name_en="..."
                    description_ru="..." 
                    description_en="..."
            >...</VehicleType> - vehicle type
        </VehicleTypes>
    </Response>

Response item
-------------

Parent item.

**Attributes:** No.

**Child items:**

+----------------+-------------+-----------------------------+
| Name           | Mandatory   | Description                 |
+================+=============+=============================+
| VehicleTypes   | Yes         | List of the vehicle types   |
+----------------+-------------+-----------------------------+

VehicleTypes item
-----------------

List of the vehicle types

**Attributes:** No.

**Child items:**

+---------------+-------------+----------------+
| Name          | Mandatory   | Description    |
+===============+=============+================+
| VehicleType   | No          | Vehicle type   |
+---------------+-------------+----------------+

VehicleType item
----------------

Name (english) of the vehicle type.

- Not Mandatory item

**Attributes:**

+-------------------+----------------+-------------+----------------------------------------------+
| Name              | Type           | Mandatory   | Description                                  |
+===================+================+=============+==============================================+
| id                | string [A-Z]   | Yes         | id of the vehicle type.                      |
+-------------------+----------------+-------------+----------------------------------------------+
| name\_ru          | string         | Yes         | Name (russian) of the vehicle type.          |
+-------------------+----------------+-------------+----------------------------------------------+
| name\_en          | string         | Yes         | Name (english) of the vehicle type.          |
+-------------------+----------------+-------------+----------------------------------------------+
| description\_ru   | string         | Yes         | Description (russian) of the vehicle type.   |
+-------------------+----------------+-------------+----------------------------------------------+
| description\_en   | string         | Yes         | Description (english) of the vehicle type.   |
+-------------------+----------------+-------------+----------------------------------------------+

**Child items:** No.