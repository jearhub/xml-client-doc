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

+-------------+----------------------------+-----------+----------------------------------------------+
| Name        | Type                       | Mandatory | Description                                  |
+=============+============================+===========+==============================================+
| CheckInFrom | Date, pattern "YYYY-MM-DD" | No        | Transfers with check in date, from this      |
+-------------+----------------------------+-----------+----------------------------------------------+
| CreatedFrom | Date, pattern "YYYY-MM-DD" | No        | Transfers with creation date, from this      |
+-------------+----------------------------+-----------+----------------------------------------------+
| CreatedTo   | Date, pattern "YYYY-MM-DD" | No        | Transfers with creation date, to this        |
+-------------+----------------------------+-----------+----------------------------------------------+
| ChangedFrom | Date, pattern "YYYY-MM-DD" | No        | Transfers with changes, which date from this |
+-------------+----------------------------+-----------+----------------------------------------------+
| ChangedTo   | Date, pattern "YYYY-MM-DD" | No        | Transfers with changes, which date to this   |
+-------------+----------------------------+-----------+----------------------------------------------+

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
        <TransferItem id="..." state="...">
          <Date>...</Date>
          <Created>...</Created>
          <FromCity>...</FromCity>
          <ToCity>...</ToCity>
          <FromLocation>...</FromLocation>
          <ToLocation>...</ToLocation>
          <Description>...</Description>
          <Logs>
              <Log>...</Log>
          </Logs>
        </TransferItem>
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

+-------+-----------+----------------------------------------+
| Name  | Mandatory | Description                            |
+=======+===========+========================================+
| Error | Yes       | Description.                           |
|       |           |                                        |
|       |           | Attributes:                            |
|       |           |                                        |
|       |           | -  ``code`` - error code               |
|       |           | -  ``description`` - error description |
+-------+-----------+----------------------------------------+





OrderList item
--------------

List of orders.

**Attributes:** No.

**Child items:**

+--------+-----------+----------------+
| Name   | Mandatory | Description    |
+========+===========+================+
| Orders | Yes       | List of orders |
+--------+-----------+----------------+

Orders item
-----------

List of orders (agent orders).

**Attributes:**

+-------+--------+-----------+-------------+
| Name  | Type   | Mandatory | Description |
+=======+========+===========+=============+
| agent | String | Yes       | Agent name  |
+-------+--------+-----------+-------------+

**Child items:**

+-------+-----------+---------------+
| Name  | Mandatory | Description   |
+=======+===========+===============+
| Order | Yes       | List of items |
+-------+-----------+---------------+

Orders/Order item
-----------------

List of items.

**Attributes:**

+--------------+--------------+-----------+---------------------------+
| Name         | Type         | Mandatory | Description               |
+==============+==============+===========+===========================+
| Id           | Numeric      | Yes       | Order id                  |
+--------------+--------------+-----------+---------------------------+
| state        | String       | Yes       | Order status              |
+--------------+--------------+-----------+---------------------------+
| via_xml_gate | true / false | Yes       | true - order via xml gate |
+--------------+--------------+-----------+---------------------------+

**Child items:**

+--------------+-----------+-----------------------------------------+
| Name         | Mandatory | Description                             |
+==============+===========+=========================================+
| TransferItem | Yes       | Item description (transfer description) |
+--------------+-----------+-----------------------------------------+

Orders/Order/TransferItem item
------------------------------

Item description.

**Attributes:**

+-------+---------+-----------+------------------+
| Name  | Type    | Mandatory | Description      |
+=======+=========+===========+==================+
| Id    | Numeric | Yes       | Transfer item id |
+-------+---------+-----------+------------------+
| state | String  | Yes       | Item status      |
+-------+---------+-----------+------------------+

**Child items:**

+--------------+----------------------------+-----------+----------------------+
| Name         | Type                       | Mandatory | Description          |
+==============+============================+===========+======================+
| Date         | Date, pattern "YYYY-MM-DD" | Yes       | Transfer date        |
+--------------+----------------------------+-----------+----------------------+
| Created      | Date                       | Yes       | Date create          |
+--------------+----------------------------+-----------+----------------------+
| FromCity     | Numeric                    | Yes       | Pick up city id      |
+--------------+----------------------------+-----------+----------------------+
| ToCity       | Numeric                    | Yes       | Drop off city id     |
+--------------+----------------------------+-----------+----------------------+
| FromLocation | String                     | Yes       | Pick up point type   |
+--------------+----------------------------+-----------+----------------------+
| ToLocation   | string                     | Yes       | Drop off point type  |
+--------------+----------------------------+-----------+----------------------+
| Description  | string                     | Yes       | Transfer description |
+--------------+----------------------------+-----------+----------------------+

Orders/Order/TransferItem/Logs item
-----------------------------------

History of order item.

**Attributes:** нет

**Child items:**

+------+--------+-----------+-------------------------------------+
| Name | Type   | Mandatory | Description                         |
+======+========+===========+=====================================+
| Log  | String | No        | History record (action description) |
+------+--------+-----------+-------------------------------------+

Orders/Order/TransferItem/Logs/Log item
---------------------------------------

History record of order item.

**Attributes:**

+------+---------------+-----------+-----------------------------------------------------------------------------------+
| Name | Type          | Mandatory | Description                                                                       |
+======+===============+===========+===================================================================================+
| date | Date and time | Yes       | Date and time of action, which describe in this history record                    |
+------+---------------+-----------+-----------------------------------------------------------------------------------+
| user | String        | Yes       | Login of user, who make described action (or 'system', if action maked by system) |
+------+---------------+-----------+-----------------------------------------------------------------------------------+
