List of transfer locations
##########################

Description of XML schema
=========================

A request for a list of transfer locations is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/transfer/TransferLocationsResponse.xsd <../../themes/hotelbook/static/xsd/dict/transfer/TransferLocationsResponse.xsd>`

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/transfer_locations``

Response, TransferLocationsResponse
-----------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <TransferLocations>
            <TransferLocation id="..." name_ru="...">...</TransferLocation> - full list of transfer locations
        </TransferLocations>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+-------------------+-----------+----------------------------+
| Name              | Mandatory | Description                |
+===================+===========+============================+
| TransferLocations | Yes       | List of transfer locations |
+-------------------+-----------+----------------------------+

TransferLocations item
----------------------

Contain full list of transfer locations.

**Attributes:** no.

**A child item:**

+------------------+-----------+-----------------------+
| Name             | Mandatory | Description           |
+==================+===========+=======================+
| TransferLocation | No        | TransferLocation name |
+------------------+-----------+-----------------------+

TransferLocation item
---------------------

Contains the name of the transfer location in English.

- Optional item

**Attributes:**

+---------+---------+-----------+--------------------------------------------------------+
| Name    | Type    | Mandatory | Description                                            |
+=========+=========+===========+========================================================+
| id      | Numeric | Yes       | TransferLocation id                                    |
+---------+---------+-----------+--------------------------------------------------------+
| name_ru | String  | Yes       | The transfer location's name in Russian (may be empty) |
+---------+---------+-----------+--------------------------------------------------------+

**Child items:** no.
