List of the types of vehicle trasmission
########################################

Description of XML schema
=========================

A request for a list of transfer vehicles is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/vehicle/VehicleTransmissionsResponse.xsd <../../themes/hotelbook/static/xsd/dict/vehicle/VehicleTransmissionsResponse.xsd>`

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/vehicle_transmissions``

Response, VehicleTransmissionsResponse
--------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <VehicleTransmissions>
            <VehicleTransmission 
                    id="..." 
                    name_ru="..." 
                    name_en="..."
                    auto="0|1"                 
            >...</VehicleTransmission> - type of the vehicle transmission
        </VehicleTransmissions>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+------------------------+-------------+---------------------------------------------+
| Name                   | Mandatory   | Description                                 |
+========================+=============+=============================================+
| VehicleTransmissions   | Yes         | List of the types of vehicle transmission   |
+------------------------+-------------+---------------------------------------------+

VehicleTransmission item
------------------------

List of the types of vehicle transmission

**Attributes:** No.

**Child items:**

+-----------------------+-------------+-----------------------------+
| Name                  | Mandatory   | Description                 |
+=======================+=============+=============================+
| VehicleTransmission   | No          | Vehicle type transmission   |
+-----------------------+-------------+-----------------------------+

VehicleTransmission item
------------------------

Name of the vehicle type transmission.

- Not Mandatory item

**Attributes:**

+------------+----------------+-------------+----------------------------------------------------+
| Name       | Type           | Mandatory   | Description                                        |
+============+================+=============+====================================================+
| id         | string [A-Z]   | Yes         | id of the vehicle type transmission                |
+------------+----------------+-------------+----------------------------------------------------+
| name\_ru   | string         | Yes         | Name (russian) of the vehicle type transmissio.    |
+------------+----------------+-------------+----------------------------------------------------+
| name\_en   | string         | Yes         | Name (english) of the vehicle type transmission.   |
+------------+----------------+-------------+----------------------------------------------------+
| auto       | 0 \| 1         | Yes         | the vehicle type transmission (auto / manual).     |
+------------+----------------+-------------+----------------------------------------------------+

**Child items:** No.