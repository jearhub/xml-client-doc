Add order / Add service
#######################

Description of XML schema
=========================

XSD-schema:

-  ``www/xsd/AddOrderRequest.xsd``
-  ``www/xsd/AddOrderResponse.xsd``

After the vehicle was searched, you can create an order with one or
more vehicle. When you create an order, indicate contact information:
full name, email address, phone number and if you want to comment on the
request. Also contains information of the driver, pick up and drop off
locations.

Also with this request you can add new service (vehicle) to the
existing order. You must indicate order id for this case.

Request, AddOrderRequest
------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>
    <AddOrderRequest>
      [<ContactInfo> - contact information (for new order)
        <Name>..</Name> - имя
        <Email>..</Email> - email
        <Phone>..</Phone> - телефон
        <Comment>..</Comment> - комментарий
      </ContactInfo>]
      [<Tag></Tag>] - order reference (for new order)
      [<AccountComment></AccountComment>] - Comment for the account (Mandatory item if XML-client has right "View account comment")
      [<OrderId></OrderId>] - order id (for adding new service to the existing order)
      <Items> - order items
        <VehicleItem> - vehicle
          <Search
            resultId=".." - result id in search results
            searchId=".." - search id
          />
          [<PayForm>cash|cashless<PayForm>] - pay form (must be the same for all items in order), may be missed for existing order
          <PickUp>
        <PickUpStation>..</PickUpStation> - id pick up station
        <PickUpFlightNum>..</PickUpFlightNum> - flight number (if there is support for airports)
        <PickUpHotel [hotelId=".."]>
           <HotelInfo [hotelName=".."]
            [hotelAddress=".."]/>
        </PickUpHotel>   
          </PickUp>
          <DropOff>
        <DropOffStation>..</DropOffStation> - id drop off station
          </DropOff>
          <Driver>
          <Title>Mr|Mrs|Ms|Chld</Title> - asking the person
          <FirstName>..</FirstName> - name (латинские)
          <LastName>..</LastName> - second name (латинские)
          <BirthDate>..</BirthDate> - date of birth (YY-mm-dd)
          </Driver>
          <Extras>      
          <Extra>..</Extra> - id extra option
          </Extras>
          <VoucherInfo>..</VoucherInfo> - information for voucher
        </VehicleItem>
      </Items>
    </AddOrderRequest>

AddOrderRequest item
--------------------

Parent item.

- Attributes: no.

Child items ``AddOrderRequest``:

+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
| **Item**           | **Mandatory**                | **Description**         |                       |                                                       |
+====================+==============================+=========================+=======================+=======================================================+
| ``ContactInfo``    | yes for new order            | Contact information     |                       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | **Item**                     | **Mandatory**           | **Description**       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | ``Name``                     | yes                     | full name             |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | ``Email``                    | yes                     | email                 |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | ``Phone``                    | yes                     | phone (15 symbols)    |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | ``Comment``                  | yes                     | comment (optional)    |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
| ``Tag``            | yes for new                  | Order reference         |                       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
| ``AccountComment`` | yes for XML-client has       | Comment for the account |                       |                                                       |
|                    | right "View account comment" |                         |                       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
| ``OrderId``        | yes for service adding       | order id                |                       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
| ``Items``          | yes                          | order items             |                       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | **Item**                     | **Mandatory**           | **Description**       |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    | ``VehicleItem``              | yes                     | Order item – Vehicle  |                                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | **item**                | **Mandatory**         | **Description**                                       |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``Search``              | yes                   | Identifiers from search response                      |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``PayForm``             | yes для нового заказа | Pay form                                              |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``PickUp``              | yes                   | Pick up location                                      |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``DropOff``             | yes                   | Drop off location                                     |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``Driver``              | yes                   | Driver (Mr, Mrs..., Name, Second Name, Date of birth) |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``Extras``              | no                    | The list of selected extras                           |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+
|                    |                              | ``VoucherInfo``         | no                    | Information for voucher                               |
+--------------------+------------------------------+-------------------------+-----------------------+-------------------------------------------------------+

ContactInfo item
----------------

For new order is mandatory item.

- Attributes: no.

Child items:

+-------------+---------------+---------------------------------------+
| **Item**    | **Mandatory** | **Description**                       |
+=============+===============+=======================================+
| ``Name``    | yes           | full name of customer (max 100 chars) |
+-------------+---------------+---------------------------------------+
| ``Email``   | yes           | email (max 100 chars)                 |
+-------------+---------------+---------------------------------------+
| ``Phone``   | yes           | phone (max 15 chars)                  |
+-------------+---------------+---------------------------------------+
| ``Comment`` | yes           | comment (optional)                    |
+-------------+---------------+---------------------------------------+

Tag item
--------

Order reference.

- For new order is mandatory item.
- Attributes: no.
- Child items: no.

OrderId item
------------

Identifier of existing order.

- Mandatory item if you want to add new vehicle to existing order.
- Attributes: no.
- Child items: no.

AccountComment item
-------------------

Comment for the account.

- Mandatory item if XML-client has right "View account comment".
- Attributes: no.
- Child items: no.

Items Item
----------

Order items (vehicle).

- Mandatory item.
- Attributes: no.
- Child items:

+-----------------+-----------------+-------------------+-------------------------------------------------------+
| **Item**        | **Mandatory**   | **Description**   |                                                       |
+=================+=================+===================+=======================================================+
| ``VehicleItem`` | yes             | Item order        |                                                       |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | **Item**        | **Mandatory**     | **Description**                                       |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``Search``      | yes               | Identifiers from search response                      |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``PayForm``     | yes for new order | Pay form                                              |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``PickUp``      | yes               | Pick up location                                      |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``DropOff``     | yes               | Drop off location                                     |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``Driver``      | yes               | Driver (Mr, Mrs,.., name, second name, date of birth) |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``Extras``      | no                | The list of selected extras                           |
+-----------------+-----------------+-------------------+-------------------------------------------------------+
|                 | ``VoucherInfo`` | no                | Information for voucher                               |
+-----------------+-----------------+-------------------+-------------------------------------------------------+

VehicleItem item
^^^^^^^^^^^^^^^^

Item order - vehicle.

- Manatory item.
- Attributes: no.
- Child items ``VehicleItem``:

+-----------------+---------------+-----------------------------------------------------------+
| **Item**        | **Mandatory** | **Description**                                           |
+=================+===============+===========================================================+
| ``Search``      | yes           | Identifiers from search response                          |
+-----------------+---------------+-----------------------------------------------------------+
| ``PayForm``     | no            | Pay form                                                  |
+-----------------+---------------+-----------------------------------------------------------+
| ``PickUp``      | yes           | Pick up location                                          |
+-----------------+---------------+-----------------------------------------------------------+
| ``DropOff``     | yes           | Drop off location                                         |
+-----------------+---------------+-----------------------------------------------------------+
| ``Driver``      | yes           | Driver (Mr, Mrs, ..., , Name, second name, date of birth) |
+-----------------+---------------+-----------------------------------------------------------+
| ``Extras``      | no            | The list of selected extras                               |
+-----------------+---------------+-----------------------------------------------------------+
| ``VoucherInfo`` | no            | Information for voucher                                   |
+-----------------+---------------+-----------------------------------------------------------+

Search item
'''''''''''

Identifiers from search response.

- Mandatory item.
- Childs item: no.
- Attributes of the item ``Search``:

+---------------+----------+---------------+-----------------+
| **Attribute** | **Type** | **Mandatory** | **Description** |
+===============+==========+===============+=================+
| ``resultId``  | numeric  | yes           | result id       |
+---------------+----------+---------------+-----------------+
| ``searchId``  | numeric  | yes           | search id       |
+---------------+----------+---------------+-----------------+

PayForm item
''''''''''''

Pay form.

- Pay form of this order. Values: cash, cashless.
- Not mandatory item. By default: cash.
- Child items: no.
- Attributes: no.

PickUp item
'''''''''''

Pick up location.

- Mandatory item.
- Attributes: no.

Child items:

+---------------------+--------------------------------------------------------+---------------+-------------------------------------------------------------------+
| **item**            | **Type**                                               | **Mandatory** | **Description**                                                   |
+=====================+========================================================+===============+===================================================================+
| ``PickUpStation``   | numeric                                                | yes           | id pick up station                                                |
+---------------------+--------------------------------------------------------+---------------+-------------------------------------------------------------------+
| ``PickUpFlightNum`` | string                                                 | yes           | fight number (if there is support airports)                       |
+---------------------+--------------------------------------------------------+---------------+-------------------------------------------------------------------+
| ``PickUpHotel``     | contains id or name and address of the hotel (pick up) | no            | information about the hotel (if there is a delivery to the hotel) |
+---------------------+--------------------------------------------------------+---------------+-------------------------------------------------------------------+

PickUpHotel item
''''''''''''''''

Delivery to the hotel (if the option is supported).

- Note mandatory item.

Attributes item ``PickUpHotel``:

+---------------+----------+---------------+-----------------+
| **Attribute** | **Type** | **Mandatory** | **Description** |
+===============+==========+===============+=================+
| ``hotelId``   | numeric  | yes           | id hotel        |
+---------------+----------+---------------+-----------------+

 Child items:

+---------------+----------------------------------------------+---------------+----------------------------------------------+
| **item**      | **Type**                                     | **Mandatory** | **Description**                              |
+===============+==============================================+===============+==============================================+
| ``HotelInfo`` | contains id or name and address of the hotel | no            | contains id or name and address of the hotel |
+---------------+----------------------------------------------+---------------+----------------------------------------------+

HotelInfo item
''''''''''''''

Delivery to the hotel (if the option is supported).

- Note mandatory item item.
- Child items: no.

Attributes of the ``HotelInfo``:

+------------------+----------+---------------+-----------------+
| **Attribute**    | **Type** | **Mandatory** | **Description** |
+==================+==========+===============+=================+
| ``hotelName``    | string   | yes           | hotel title     |
+------------------+----------+---------------+-----------------+
| ``hotelAddress`` | string   | yes           | hotel address   |
+------------------+----------+---------------+-----------------+

DropOff item
''''''''''''

Drop off location.

- Mandatory item.
- Attributes: no.

Child items:

+--------------------+----------+---------------+---------------------+
| **item**           | **Type** | **Mandatory** | **Description**     |
+====================+==========+===============+=====================+
| ``DropOffStation`` | numeric  | yes           | id drop off station |
+--------------------+----------+---------------+---------------------+

item Driver
'''''''''''

Driver.

- Mandatory item.
- Attributes: no.

Child items:

+---------------+----------------+---------------+-----------------------------+
| **item**      | **Type**       | **Mandatory** | **Description**             |
+===============+================+===============+=============================+
| ``Title``     | Mr,Ms,Mrs,Chld | yes           | Mr, Mrs, ...                |
+---------------+----------------+---------------+-----------------------------+
| ``FirstName`` | string         | yes           | Driver name (latin letters) |
+---------------+----------------+---------------+-----------------------------+
| ``LastName``  | string         | yes           | Second name (latin letters) |
+---------------+----------------+---------------+-----------------------------+
| ``BirthDate`` | string         | yes           | Date of birth (YY-mm-dd)    |
+---------------+----------------+---------------+-----------------------------+

Extras item
'''''''''''

The list of selected extras.

- Not Mandatory item.
- Attributes: no.

Child items:

+-----------+-------------------+---------------+---------------------------------+
| **item**  | **Type**          | **Mandatory** | **Description**                 |
+===========+===================+===============+=================================+
| ``Extra`` | id extra (extras) | yes           | the list of the selected extras |
+-----------+-------------------+---------------+---------------------------------+

item VoucherInfo
''''''''''''''''

Information for voucher.

- Not mandatory item.
- Attributes: no.
- Child items: no

Response, AddOrderResponse
--------------------------

XML-schema:

::


    <?xml version="1.0" encoding="utf-8"?>
    <AddOrderResponse>
      [<Errors>
        <Error code="..." description="..."> - list of errors
      </Errors>]
      [<OrderId>..</OrderId>] - order id
    </AddOrderResponse>

AddOrderResponse item
---------------------

Parent item.

- Attributes: no.

Child items:

+-------------+---------------+----------------------+-----------------------------+
| **Item**    | **Mandatory** | **Description**      |                             |
+=============+===============+======================+=============================+
| ``Errors``  | no            | List of errors       |                             |
+-------------+---------------+----------------------+-----------------------------+
|             | **Item**      | **Mandatory**        | **Description**             |
+-------------+---------------+----------------------+-----------------------------+
|             | ``Error``     | yes                  | Error description with code |
+-------------+---------------+----------------------+-----------------------------+
| ``OrderId`` | no            | New order identifier |                             |
+-------------+---------------+----------------------+-----------------------------+

Errors item
-----------

List of errors.

- Optional item.
- Attributes: no.

Child items:

+-----------+---------------+-----------------------------+
| **Item**  | **Mandatory** | **Description**             |
+===========+===============+=============================+
| ``Error`` | yes           | Error code with description |
+-----------+---------------+-----------------------------+

Error item
^^^^^^^^^^

Mandatory item.

- Child items: no.

Attributes:

+-----------------+----------+---------------+-------------------+
| **Attribute**   | **Type** | **Mandatory** | **Description**   |
+=================+==========+===============+===================+
| ``code``        | string   | yes           | Error code UTS.   |
+-----------------+----------+---------------+-------------------+
| ``description`` | string   | yes           | Error description |
+-----------------+----------+---------------+-------------------+

OrderId item
------------

New order id.

- Optional item.
- Attributes: no.
- Child items: no.