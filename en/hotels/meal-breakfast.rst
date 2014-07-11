Types of breakfast
##################

Description of XML schema
=========================

A request for a list of types of breakfasts is formed through URL (using GET method)

XSD-schema response :

- :download:`www/xsd/dict/meal/MealBreakfastResponse.xsd <../../themes/hotelbook/static/xsd/dict/meal/MealBreakfastResponse.xsd>`

Request
-------

Contains no parameters. Request is passed via the URL with credentials (``login``, ``password``, ``checksum``,..).

Request path: ``/xml/meal_breakfast``

Response, MealBreakfastResponse
-------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Breakfasts>
            <Breakfast id="...">...</Breakfast> - list of types of breakfast
        </Breakfasts>
    </Response>

Response item
-------------

Parent item.

**Attributes:** no.

**Child items:**

+--------------+-------------+--------------------------------------------+
| Name         | Mandatory   | Description                                |
+==============+=============+============================================+
| Breakfasts   | Yes         | Contains full list of types of breakfast   |
+--------------+-------------+--------------------------------------------+

Breakfasts item
---------------

Contains full list of types of breakfast.

**Attributes:** no.

**A child item:**

+-----------+-----------+------------------------------------------------------+
| Name      | Mandatory | Description                                          |
+===========+===========+======================================================+
| Breakfast | No        | Breakfast name                                       |
|           |           |                                                      |
|           |           | Attributes:                                          |
|           |           |                                                      |
|           |           | -  ``id`` - id of type of breakfast                  |
+-----------+-----------+------------------------------------------------------+