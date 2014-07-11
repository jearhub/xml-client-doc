List of the companies (vehicle)
###############################

Description of XML schema
=========================

A request for a list of transfer vehicles is formed through URL (using
GET method)

XSD-schema response :

:download:`www/xsd/dict/vehicle/VehicleCompaniesResponse.xsd <../../themes/hotelbook/static/xsd/dict/vehicle/VehicleCompaniesResponse.xsd>`

Request
-------

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/vehicle_companies``

Response, VehicleCompaniesResponse
----------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <VehicleCompanies>
            <VehicleCompany id="..." logo_url="...">...</VehicleCompany> - company
        </VehicleCompanies>
    </Response>

Response item
-------------

Parent item.

**Attributes:** No.

**Child items:**

+------------------+-----------+-----------------------+
| Name             | Mandatory | Description           |
+==================+===========+=======================+
| VehicleCompanies | Yes       | List of the companies |
+------------------+-----------+-----------------------+

VehicleCompanies item
---------------------

List of the companies.

**Атрибуты:** No.

**Child items:**

+----------------+-----------+-----------------+
| Name           | Mandatory | Description     |
+================+===========+=================+
| VehicleCompany | No        | Vehicle company |
+----------------+-----------+-----------------+

VehicleCompany item
-------------------

Name (english) of the company.

- Not Mandatory item

**Атрибуты:**

+----------+--------------+-----------+-------------------------+
| Name     | Type         | Mandatory | Description             |
+==========+==============+===========+=========================+
| id       | string [A-Z] | Yes       | id of the company       |
+----------+--------------+-----------+-------------------------+
| logo_url | string       | Yes       | url of the logo company |
+----------+--------------+-----------+-------------------------+

**Child items:** No.