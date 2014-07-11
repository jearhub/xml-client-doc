List of the vehicle classes
###########################

Description of XML schema
=========================

A request for a list of transfer vehicles is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/vehicle/VehicleClassesResponse.xsd <../../themes/hotelbook/static/xsd/dict/vehicle/VehicleClassesResponse.xsd>`

Request
-------

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/vehicle_classes``

Response, VehicleClassesResponse
--------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <VehicleClasses>
            <VehicleClass id="..." name_ru="..." name_en="...">...</VehicleClass> - vehicle class
        </VehicleClasses>
    </Response>

Response item
-------------

Parent item.

**Attributes:** No.

**Child items:**

+----------------+-----------+-----------------------------+
| Name           | Mandatory | Description                 |
+================+===========+=============================+
| VehicleClasses | Yes       | List of the vehicle classes |
+----------------+-----------+-----------------------------+

VehicleClasses item
-------------------

List of the vehicle classes

**Attributes:** No.

**Child items:**

+--------------+-----------+---------------+
| Name         | Mandatory | Description   |
+==============+===========+===============+
| VehicleClass | No        | Vehicle class |
+--------------+-----------+---------------+

VehicleClass item
-----------------

Name (english) of the vehicle class.

- Not Mandatory item

**Attributes:**

+---------+--------------+-----------+--------------------------------------+
| Name    | Type         | Mandatory | Description                          |
+=========+==============+===========+======================================+
| id      | string [A-Z] | Yes       | id of the vehicle class              |
+---------+--------------+-----------+--------------------------------------+
| name_ru | string       | Yes       | Name (russian) of the vehicle class. |
+---------+--------------+-----------+--------------------------------------+
| name_en | string       | Yes       | Name (english) of the vehicle class. |
+---------+--------------+-----------+--------------------------------------+

**Child items:** No.