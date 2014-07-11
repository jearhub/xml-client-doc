List of orders
##############

Description of XML schema
=========================

XSD-schema request:

- :download:`www/xsd/order/OrderListRequest.xsd <../../themes/hotelbook/static/xsd/order/OrderListRequest.xsd>`

XSD-schema response:

- :download:`www/xsd/order/OrderListResponse.xsd <../../themes/hotelbook/static/xsd/order/OrderListResponse.xsd>`

Request
-------

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
     [<OrderListRequest>...</OrderListRequest>] - Request for this response
     [<Errors>
        <Error code="..." description="..."> - list of errors
      </Errors>]
      <OrderList>
        <Orders agent="..."> - список заказов (может быть много)
          <Order id="..." state="..." via_xml_gate="true|false"> - list of orders
            <HotelItem id="..." state="...">
              <HotelId>...</HotelId>
              [<HotelName>...</HotelName>]
              [<CheckIn>...</CheckIn>]
              [<Duration>...</Duration>]
              [<Created>...</Created>]
              [<Price></Price>]
              [<Currency></Currency>]
              [<Currency></Currency>]
              [<Rooms>
                <Room roomSizeId=".." roomTypeId=".." roomViewId=".." cots="...">
                  <Paxes>
                    <Pax>
                      [<Title>...</Title>]
                      [<FirstName>...</FirstName>]
                      [<LastName>...</LastName>]
                    </Pax>
                  </Paxes>
                </Room>
              </Rooms>]
              [<Logs></Logs>]
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

+--------------------+---------------------------------------+----------------------------+
| Name               | Mandatory                             | Description                |
+====================+=======================================+============================+
| OrderListRequest   | No                                    | Request                    |
+--------------------+---------------------------------------+----------------------------+
| Errors             | No                                    | List of errors             |
+--------------------+---------------------------------------+----------------------------+
| OrderList          | No                                    | List of orders             |
+--------------------+---------------------------------------+----------------------------+

Errors item
-----------

View :doc:`Error page <../errors>`

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
| tag              | String         | No          | order reference             |
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
| stateId | Numeric   | No          | State id        |
+---------+-----------+-------------+-----------------+

**Child items:**

+------------+------------------------------+-------------+---------------------+
| Name       | Type                         | Mandatory   | Description         |
+============+==============================+=============+=====================+
| HotelId    | Numeric                      | Yes         | Hotel id            |
+------------+------------------------------+-------------+---------------------+
| HotelName  | String                       | No          | Hotel name          |
+------------+------------------------------+-------------+---------------------+
| CheckIn    | Date, pattern "YYYY-MM-DD"   | Yes         | Check in date       |
+------------+------------------------------+-------------+---------------------+
| Duration   | Numeric                      | Yes         | Duration (nights)   |
+------------+------------------------------+-------------+---------------------+
| Created    | Date                         | Yes         | Date create         |
+------------+------------------------------+-------------+---------------------+
| Price      | Numeric                      | No          | Price               |
+------------+------------------------------+-------------+---------------------+
| Currency   | String                       | No          | Currency            |
+------------+------------------------------+-------------+---------------------+
| Rooms      | Nested                       | No          | List of Rooms       |
+------------+------------------------------+-------------+---------------------+
| Logs       | Nested                       | No          | History             |
+------------+------------------------------+-------------+---------------------+

Orders/Order/HotelItem/Room item
--------------------------------

**Attributes:**

+-------------------+-----------------+--------------+------------------------------------------------------------+
| Name              | Type            | Mandatory    | Description                                                |
+===================+=================+==============+============================================================+
| roomSizeId        | Numeric         | Yes          | room size id                                               |
+-------------------+-----------------+--------------+------------------------------------------------------------+
| roomTypeId        | Numeric         | Yes          | room type id                                               |
+-------------------+-----------------+--------------+------------------------------------------------------------+
| roomViewId        | Numeric         | Yes          | room view id                                               |
+-------------------+-----------------+--------------+------------------------------------------------------------+
| cots              | Numeric         | Yes          | cots                                                       |
+-------------------+-----------------+--------------+------------------------------------------------------------+

Orders/Order/HotelItem/Room/Paxes item
--------------------------------------

+-------+--------------+----------------------------------------------------------------------------+
| Name  | Mandatory    | Description                                                                |
+=======+==============+============================================================================+
| Paxes | No           | Pax data                                                                   |
+-------+--------------+----------------------------------------------------------------------------+

Orders/Order/HotelItem/Room/Paxes/Pax item
------------------------------------------

Pax data.

**Child items:**

+-----------+-------------------+--------------+---------------------+
| Name      | Type              | Mandatory    | Description         |
+===========+===================+==============+=====================+
| Title     | Mr, Mrs, Ms, Chld | No           | Обращение к персоне |
+-----------+-------------------+--------------+---------------------+
| FirstName | String            | No           | Name                |
+-----------+-------------------+--------------+---------------------+
| LastName  | String            | No           | Last name           |
+-----------+-------------------+--------------+---------------------+

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
