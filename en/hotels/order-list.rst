List of orders
##############

Description of XML schema
=========================

XSD-schema request:

-  ``www/xsd/OrderListRequest.xsd``

XSD-schema response:

-  ``www/xsd/OrderListResponse.xsd``

Request
-------

Request path: ``/xml/order_list``

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderListRequest>
        [<CheckInFrom>...</CheckInFrom>]
        [<CreatedFrom>...</CreatedFrom>]
        [<CreatedTo>...</CreatedTo>]
        [<ChangedFrom>...</ChangedFrom>]
        [<ChangedTo>...</ChangedTo>]
    </OrderListRequest>

OrderListRequest item
---------------------

Parent item.

**Attributes:** no.

**Child items:**

+---------------+------------------------------+-------------+---------------------------------------------+
| Name          | Type                         | Mandatory   | Description                                 |
+===============+==============================+=============+=============================================+
| CheckInFrom   | Date, pattern "YYYY-MM-DD"   | No          | Hotels with check in date, from this        |
+---------------+------------------------------+-------------+---------------------------------------------+
| CreatedFrom   | Date, pattern "YYYY-MM-DD"   | No          | Hotels with creation date, from this        |
+---------------+------------------------------+-------------+---------------------------------------------+
| CreatedTo     | Date, pattern "YYYY-MM-DD"   | No          | Hotels with creation date, to this          |
+---------------+------------------------------+-------------+---------------------------------------------+
| ChangedFrom   | Date, pattern "YYYY-MM-DD"   | No          | Hotels with changes, which date from this   |
+---------------+------------------------------+-------------+---------------------------------------------+
| ChangedTo     | Date, pattern "YYYY-MM-DD"   | No          | Hotels with changes, which date to this     |
+---------------+------------------------------+-------------+---------------------------------------------+

Response, OrderListResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderListResponse>
     [<Errors>
        <Error code="..." description="..."> - list of errors
      </Errors>]
      <OrderList>
        <Orders agent="..."> - list of orders
          <Order id="..." state="..." via_xml_gate="true|false"> - list of items
            <HotelItem id="..." state="...">
              <HotelId>...</HotelId>
              <CheckIn>...</CheckIn>
              <Duration>...</Duration>
              <Created>...</Created>
            </HotelItem>
          </Order>
        </Orders>
      </OrderList>
    </OrderListResponse>

OrderListResponse item
----------------------

Parent item.

**Attributes:** No.

**Child items:**

+-------------+-------------+------------------+
| Name        | Mandatory   | Description      |
+=============+=============+==================+
| Errors      | No          | List of errors   |
+-------------+-------------+------------------+
| OrderList   | No          | List of orders   |
+-------------+-------------+------------------+

Errors item
-----------

List of errors.

**Attributes:** No.

**Child items:**

+-------+-----------+---------------------------------------+
| Name  | Mandatory | Description                           |
+=======+===========+=======================================+
| Error | Yes       | Error description.                    |
|       |           |                                       |
|       |           | Attributes:                           |
|       |           |                                       |
|       |           | - ``code`` - error code               |
|       |           | - ``description`` - error description |
+-------+-----------+---------------------------------------+

OrderList item
--------------

List of orders.

**Attributes:** No.

**Child items:**

+----------+-------------+------------------+
| Name     | Mandatory   | Description      |
+==========+=============+==================+
| Orders   | Yes         | List of orders   |
+----------+-------------+------------------+

Orders item
-----------

List of orders (agent orders).

**Attributes:**

+---------+----------+-------------+---------------+
| Name    | Type     | Mandatory   | Description   |
+=========+==========+=============+===============+
| agent   | String   | Yes         | Agent name    |
+---------+----------+-------------+---------------+

**Child items:**

+---------+-------------+-----------------------------------+
| Name    | Mandatory   | Description                       |
+=========+=============+===================================+
| Order   | Yes         | List of items (HotelItem items)   |
+---------+-------------+-----------------------------------+

Orders/Order item
-----------------

List of items.

**Attributes:**

+------------------+----------------+-------------+-----------------------------+
| Name             | Type           | Mandatory   | Description                 |
+==================+================+=============+=============================+
| Id               | Numeric        | Yes         | Order id                    |
+------------------+----------------+-------------+-----------------------------+
| state            | String         | Yes         | Order status                |
+------------------+----------------+-------------+-----------------------------+
| via\_xml\_gate   | true / false   | Yes         | true - order via xml gate   |
+------------------+----------------+-------------+-----------------------------+

 **Child items:**

+-------------+-------------+----------------------------------------+
| Name        | Mandatory   | Description                            |
+=============+=============+========================================+
| HotelItem   | Yes         | Item description (hotel description)   |
+-------------+-------------+----------------------------------------+

Orders/Order/HotelItem item
---------------------------

Item description.

**Attributes:**

+---------+-----------+-------------+-----------------+
| Name    | Type      | Mandatory   | Description     |
+=========+===========+=============+=================+
| Id      | Numeric   | Yes         | Hotel item id   |
+---------+-----------+-------------+-----------------+
| state   | String    | Yes         | Item status     |
+---------+-----------+-------------+-----------------+

**Child items:**

+------------+------------------------------+-------------+---------------------+
| Name       | Type                         | Mandatory   | Description         |
+============+==============================+=============+=====================+
| HotelId    | Numeric                      | Yes         | Hotel id            |
+------------+------------------------------+-------------+---------------------+
| CheckIn    | Date, pattern "YYYY-MM-DD"   | Yes         | Check in date       |
+------------+------------------------------+-------------+---------------------+
| Duration   | Numeric                      | Yes         | Duration (nights)   |
+------------+------------------------------+-------------+---------------------+
| Created    | Date                         | Yes         | Date create         |
+------------+------------------------------+-------------+---------------------+

Orders/Order/HotelItem/Logs item
--------------------------------

History of order item.

**Attributes:** нет

**Child items:**

+--------+----------+-------------+---------------------------------------+
| Name   | Type     | Mandatory   | Description                           |
+========+==========+=============+=======================================+
| Log    | String   | No          | History record (action description)   |
+--------+----------+-------------+---------------------------------------+

Orders/Order/HotelItem/Logs/Log item
------------------------------------

History record of order item.

**Attributes:**

+--------+-----------------+-------------+-------------------------------------------------------------------------------------+
| Name   | Type            | Mandatory   | Description                                                                         |
+========+=================+=============+=====================================================================================+
| date   | Date and time   | Yes         | Date and time of action, which describe in this history record                      |
+--------+-----------------+-------------+-------------------------------------------------------------------------------------+
| user   | String          | Yes         | Login of user, who make described action (or 'system', if action maked by system)   |
+--------+-----------------+-------------+-------------------------------------------------------------------------------------+
