Types of meal
#############

Description of XML schema
=========================

A request for a list of types of meals is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/MealResponse.xsd``

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/meal``

Response, MealResponse
----------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Meals>
            <Meal id="...">...</Meal> - list of types of meal
        </Meals>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+---------+-------------+---------------------------------------+
| Name    | Mandatory   | Description                           |
+=========+=============+=======================================+
| Meals   | Yes         | Contains full list of types of meal   |
+---------+-------------+---------------------------------------+

Meals item
----------

Contains full list of types of meal.

**Attributes:** no.

**A child item:**

+----------+-----------+------------------------------------------------------+
| Name     | Mandatory | Description                                          |
+==========+===========+======================================================+
| Meal     | No        | Meal name                                            |
|          |           |                                                      |
|          |           | Attributes:                                          |
|          |           |                                                      |
|          |           | -  ``id`` - id of type of meal                       |
+----------+-----------+------------------------------------------------------+