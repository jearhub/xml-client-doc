List of languages
#################

Description of XML schema
=========================

A request for a list of languages is formed through URL (using GET method)

XSD-schema response :

:download:`www/xsd/dict/LanguagesResponse.xsd <../../themes/hotelbook/static/xsd/dict/LanguagesResponse.xsd>`

Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/languages``

Response, LanguagesResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Languages>
            <Language id="..." name_ru="...">...</Language> - full list of languages
        </Languages>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**A child item:**

+-----------+-----------+-------------------+
| Name      | Mandatory | Description       |
+===========+===========+===================+
| Languages | Yes       | List of languages |
+-----------+-----------+-------------------+

Languages item
--------------

Contain full list of languages.

**Attributes:** no.

**A child item:**

+----------+-----------+---------------+
| Name     | Mandatory | Description   |
+==========+===========+===============+
| Language | No        | Language name |
+----------+-----------+---------------+

Language item
-------------

Contains the name of the language in English.

Optional item

**Attributes:**

+---------+---------+-----------+-----------------------------------------------+
| Name    | Type    | Mandatory | Description                                   |
+=========+=========+===========+===============================================+
| id      | Numeric | Yes       | Language id                                   |
+---------+---------+-----------+-----------------------------------------------+
| name_ru | String  | Yes       | The language's name in Russian (may be empty) |
+---------+---------+-----------+-----------------------------------------------+

**Child items:** no.