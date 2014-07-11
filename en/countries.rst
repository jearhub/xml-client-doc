Country list
############

Description of XML schema
=========================

A request for a list of countries is formed through URL (using GET method)

XSD-schema response :

-  :download:`www/xsd/dict/geo/CountriesResponse.xsd <../themes/hotelbook/static/xsd/dict/geo/CountriesResponse.xsd>`

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
            <Country id="..." [region="..."] [iso_code="..."] [sng="..."] [shengen="..."] [flag_url="..."]>...</Country> - full list of countries
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

Country item
-----------------

**Attributes:**

+------------+-----------+----------------------+------------------------------+
| Attribute  | Type		 |  Mandatory           | Description                  |
+============+===========+======================+==============================+
| id         | Число     |  Да                  | identifier                   |
+------------+-----------+----------------------+------------------------------+
| region     | Число     |  Нет                 | region                       |
+------------+-----------+----------------------+------------------------------+
| iso_code   | Строка    |  Нет                 | ISO-code                     |
+------------+-----------+----------------------+------------------------------+
| sng        | Число     |  Нет                 | SNG                          |
+------------+-----------+----------------------+------------------------------+
| shengen    | Число     |  Нет                 | shengen                      |
+------------+-----------+----------------------+------------------------------+
| flag_url   | Строка    |  Нет                 | flag url                     |
+------------+-----------+----------------------+------------------------------+