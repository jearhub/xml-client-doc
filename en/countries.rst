Country list
############

Description of XML schema
=========================

A request for a list of countries is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/CountryResponse.xsd``

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/countries``

Response, CountriesResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Countries>
            <Country id="...">...</Country> - full list of countries
        </Countries>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+-------------+-------------+-----------------------------------+
| Name        | Mandatory   | Description                       |
+=============+=============+===================================+
| Countries   | Yes         | Contains full list of countries   |
+-------------+-------------+-----------------------------------+

Countries item
--------------

Contains full list of countries.

**Attributes:** no.

**A child item:**

+---------+-----------+----------------------------------------------+
| Name    | Mandatory | Description                                  |
+=========+===========+==============================================+
| Country | No        | Country name Attributes: ``id`` - country id |
+---------+-----------+----------------------------------------------+

