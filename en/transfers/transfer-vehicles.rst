List of transfer vehicles
#########################

Description of XML schema
=========================

A request for a list of transfer vehicles is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/transfer/TransferVehiclesResponse.xsd <../../themes/hotelbook/static/xsd/transfer/TransferVehiclesResponse.xsd>`

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/transfer_vehicles``

Response, TransferVehiclesResponse
----------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <TransferVehicles>
            <TransferVehicle id="..." name_ru="...">...</TransferVehicle> - full list of transfer vehicles
        </TransferVehicles>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+------------------+-----------+---------------------------+
| Name             | Mandatory | Description               |
+==================+===========+===========================+
| TransferVehicles | Yes       | List of transfer vehicles |
+------------------+-----------+---------------------------+

TransferVehicles item
---------------------

Contain full list of transfer vehicles.

**Attributes:** no.

**A child item:**

+-----------------+-----------+----------------------+
| Name            | Mandatory | Description          |
+=================+===========+======================+
| TransferVehicle | No        | TransferVehicle name |
+-----------------+-----------+----------------------+

TransferVehicle item
--------------------

Contains the name of the transfer vehicle in English.

Optional item

**Attributes:**

+---------+---------+-----------+-------------------------------------------------------+
| Name    | Type    | Mandatory | Description                                           |
+=========+=========+===========+=======================================================+
| id      | Numeric | Yes       | TransferVehicle id                                    |
+---------+---------+-----------+-------------------------------------------------------+
| name_ru | String  | Yes       | The transfer vehicle's name in Russian (may be empty) |
+---------+---------+-----------+-------------------------------------------------------+

**Child items:** no.