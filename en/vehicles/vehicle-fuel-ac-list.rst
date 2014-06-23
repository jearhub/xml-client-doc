List of the vehicle types, according to the fuel policy
#######################################################

Description of XML schema
=========================

A request for a list of transfer vehicles is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/VehicleFuelACListResponse.xsd``

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/vehicle_fuel_ac``

Response, VehicleFuelACListResponse
-----------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <VehicleFuelACList>
            <VehicleFuelAC 
                    id="..." 
                    name_ru="..." 
                    name_en="..."
                    ac="0|1"                 
            >...</VehicleFuelAC> - fuel policy
        </VehicleFuelACList>
    </Response>

Response item
-------------

Parent item.

**Attributes:** No.

**Child items:**

+-------------------+-----------+---------------------------------------+
| Name              | Mandatory | Description                           |
+===================+===========+=======================================+
| VehicleFuelACList | Yes       | List of the vehicle fuel policy types |
+-------------------+-----------+---------------------------------------+

VehicleFuelACList item
----------------------

List of the vehicle fuel policy types

**Attributes:** No.

**Child items:**

+---------------+-----------+-------------------------+
| Name          | Mandatory | Description             |
+===============+===========+=========================+
| VehicleFuelAC | No        | Type of the fuel policy |
+---------------+-----------+-------------------------+

VehicleFuelAC item
------------------

Type of the fuel policy

- Not Mandatory item

**Attributes:**

+------------+----------------+-------------+-------------------------------------------------+
| Name       | Type           | Mandatory   | Description                                     |
+============+================+=============+=================================================+
| id         | string [A-Z]   | Yes         | id of the type fuel policy                      |
+------------+----------------+-------------+-------------------------------------------------+
| name_ru    | string         | Yes         | Name (russian) of the type fuel policy.         |
+------------+----------------+-------------+-------------------------------------------------+
| name_en    | string         | Yes         | Name (english) of the type fuel policy.         |
+------------+----------------+-------------+-------------------------------------------------+
| ac         | 0 \| 1         | Yes         | Availability air conditioning in the vehicle.   |
+------------+----------------+-------------+-------------------------------------------------+

**Child items:** No.
