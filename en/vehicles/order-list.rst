List of orders
##############

Description of XML schema
=========================

XSD-schema request:

:download:`www/xsd/order/OrderListRequest.xsd <../../themes/hotelbook/static/xsd/order/OrderListRequest.xsd>`

XSD-schema response:

:download:`www/xsd/order/OrderListResponse.xsd <../../themes/hotelbook/static/xsd/order/OrderListResponse.xsd>`

Request, OrderListRequest
-------------------------

Request path: ``/xml/order_list``

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderListRequest>
        [<CheckInFrom>...</CheckInFrom>]
        [<CheckInTo>...</CheckInTo>]
        [<CreatedFrom>...</CreatedFrom>]
        [<CreatedTo>...</CreatedTo>]
        [<ChangedFrom>...</ChangedFrom>]
        [<ChangedTo>...</ChangedTo>]
        [<Agents>
          <Agent>...<Agent>
        </Agents>]
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
| CheckInTo     | Date, pattern "YYYY-MM-DD"   | No          | Check in to                                 |
+---------------+------------------------------+-------------+---------------------------------------------+
| CreatedFrom   | Date, pattern "YYYY-MM-DD"   | No          | Hotels with creation date, from this        |
+---------------+------------------------------+-------------+---------------------------------------------+
| CreatedTo     | Date, pattern "YYYY-MM-DD"   | No          | Hotels with creation date, to this          |
+---------------+------------------------------+-------------+---------------------------------------------+
| ChangedFrom   | Date, pattern "YYYY-MM-DD"   | No          | Hotels with changes, which date from this   |
+---------------+------------------------------+-------------+---------------------------------------------+
| ChangedTo     | Date, pattern "YYYY-MM-DD"   | No          | Hotels with changes, which date to this     |
+---------------+------------------------------+-------------+---------------------------------------------+
| Agents        | Nested                       | No          | Agents                                      |
+---------------+------------------------------+-------------+---------------------------------------------+

Response, OrderListResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderListResponse>
     [<Errors>
        <Error code="..." description="..."> - errors
      </Errors>]
      <OrderList>
        <Orders agent="..."> - list of te orders (may be more one)
          <Order id="..." state="..." via_xml_gate="true|false"> - list of the order items (may be more one)
            <VehicleItem id="..." state="...">          
              <Created>...</Created>
              <PickUpDate>...</PickUpDate>
              <DropOffDate>...</DropOffDate>
              <PointType>...</PointType>
              <PickUpPoint>...</PickUpPoint>
              <DropOffPoint>...</DropOffPoint>
              <PickUpStation>...</PickUpStation>
              <DropOffStation>...</DropOffStation>
              <ACRISS>...</ACRISS>
              <CompanyName>...</CompanyName>
              <Logs>
                  <Log>...</Log>
              </Logs>
            </VehicleItem>
          </Order>
        </Orders>
      </OrderList>
    </OrderListResponse>

item OrderListResponse
----------------------

Корневой item.

**Attributes:** no.

**Child items:**

+--------------------+---------------------------------------+----------------------------+
| Name               | Mandatory                             | Description                |
+====================+=======================================+============================+
| OrderListRequest   | No                                    | Request                    |
+--------------------+---------------------------------------+----------------------------+
| Errors             | No                                    | List of errors             |
+--------------------+---------------------------------------+----------------------------+
| OrderList          | No                                    | List of orders             |
+--------------------+---------------------------------------+----------------------------+

item Errors
-----------

View :doc:`Error page <../errors>`

OrderList item
--------------

List of orders.

**Attributes:** no.

**Child items:**

+----------+-------------+---------------------------------+
| Name     | Mandatory   | Description                     |
+==========+=============+=================================+
| Orders   | Yes         | List of orders (agent orders)   |
+----------+-------------+---------------------------------+

Orders item
-----------

List of orders (agent orders).

**Attributes:**

+---------+----------+-------------+---------------+
| Name    | Type     | Mandatory   | Description   |
+=========+==========+=============+===============+
| agent   | string   | Yes         | Name agent    |
+---------+----------+-------------+---------------+

**Child items:**

+---------+-------------+-----------------+
| Name    | Mandatory   | Description     |
+=========+=============+=================+
| Order   | Yes         | List of items   |
+---------+-------------+-----------------+

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
| tag              | String         | No          | order reference             |
+------------------+----------------+-------------+-----------------------------+

 **Child items:**

+-------------+-----------+---------------------+
| Name        | Mandatory | Description         |
+=============+===========+=====================+
| VehicleItem | Yes       | vehicle description |
+-------------+-----------+---------------------+

item Orders/Order/VehicleItem
-----------------------------

Vehicle description.

**Attributes:**

+---------+-----------+-------------+-----------------+
| Name    | Type      | Mandatory   | Description     |
+=========+===========+=============+=================+
| Id      | Numeric   | Yes         | Hotel item id   |
+---------+-----------+-------------+-----------------+
| state   | String    | Yes         | Item status     |
+---------+-----------+-------------+-----------------+
| stateId | Numeric   | No          | State id        |
+---------+-----------+-------------+-----------------+

**Child items:**

+----------------+--------------------------+-----+-----------------------------------------------------------------+
| Created        | Yesта                    | Yes | creation date                                                   |
+================+==========================+=====+=================================================================+
| PickUpDate     | date (YY-mm-dd)          | Yes | pick up date                                                    |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| DropOffDate    | date (YY-mm-dd)          | Yes | drop off date                                                   |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| PointType      | string ( city, airport ) | Yes | type point                                                      |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| PickUpPoint    | numeric                  | Yes | id of the pick up point (city od airport, depending PonitType)  |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| DropOffPoint   | numeric                  | Yes | id of the drop off point (city od airport, depending PonitType) |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| PickUpStation  | numeric                  | Yes | id of the pick up station                                       |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| DropOffStation | numeric                  | Yes | id of the drop off station                                      |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| ACRISS         | string                   | Yes | ACRISS code (vehicle)                                           |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| CompanyName    | string                   | no  | name of the company servise                                     |
+----------------+--------------------------+-----+-----------------------------------------------------------------+
| Logs           | Список itemов Log        | no  | History of order item.                                          |
+----------------+--------------------------+-----+-----------------------------------------------------------------+

item Orders/Order/VehicleItem/Logs
----------------------------------

History of order item.

**Attributes:** no

**Child items:**

+------+--------+-----------+-------------------------------------+
| Name | Type   | Mandatory | Description                         |
+======+========+===========+=====================================+
| Log  | string | no        | History record (action description) |
+------+--------+-----------+-------------------------------------+

item Orders/Order/VehicleItem/Logs/Log
--------------------------------------

History record.

**Attributes:**

+------+--------------+-----------+---------------------------------------------------------------+
| Name | Type         | Mandatory | Description                                                   |
+======+==============+===========+===============================================================+
| date | date и время | Yes       | date and time of the actions described in this record history |
+------+--------------+-----------+---------------------------------------------------------------+
| user | string       | Yes       | User who committed the described action (or system)           |
+------+--------------+-----------+---------------------------------------------------------------+