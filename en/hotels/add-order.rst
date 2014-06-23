Add order / Add service
#######################

Description of XML schema
=========================

XSD-schema:

-  ``www/xsd/AddOrderRequest.xsd``
-  ``www/xsd/AddOrderResponse.xsd``

After the hotel was searched, you can create an order with one or more
hotels. When you create an order, indicate contact information: full
name, email address, phone number and if you want to comment on the
request. Also contains information on persons in the room. For each
number indicates the number of people strong, with a child, if there is
one in the room - comes last.

Also with this request you can add new service (hotel) to the existing
order. You must indicate order id for this case.

Request
-------

XML-schema:

::


    <?xml version="1.0" encoding="utf-8"?>
    <AddOrderRequest>
      [<ContactInfo> - contact information (for new order)
        <Name>..</Name> - name
        <Email>..</Email> - email
        <Phone>..</Phone> - phone
        <Comment>..</Comment> - comment
      </ContactInfo>]
      [<Tag></Tag>] - order reference (for new order)
      [<AccountComment></AccountComment>] - Comment for the account (Mandatory item if XML-client has right "View account comment")
      [<OrderId></OrderId>] - order id (for adding new service to the existing order)
      <Items> - order items
        <HotelItem> - hotel
          <Search
            resultId=".." - result id from search response
            searchId=".." - search id
          />
          [<DuplicatesAllowed>true|false<DuplicatesAllowed>] - is duplicates allowed for this hotel
          [<PayForm>cash|cashless<PayForm>] - pay form of order (must be the same for every hotel), for existing order this is optional
          <Rooms> - room, in the order in which were transferred in search response
            <Room>
              <RoomPax [child="true|false"] [age=".."]> - paxes in room
                <Title>Mr|Mrs|Ms|Chld</Title> - title
                <FirstName>..</FirstName> - name
                <LastName>..</LastName> - surname
              </RoomPax>
            </Room>
          </Rooms>
          <Remarks> - list of remarks (Optional item)
             <Remark>remark_id</Remark>
          </Remarks>
          <Comment>...</Comment> - free remark (Optional item)
        </HotelItem>
      </Items>
    </AddOrderRequest>

AddOrderRequest item
--------------------

- Parent item.
- Attributes: no.

Child items:

+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
| **Item**           | **Mandatory**                | **Description**         |                    |                                  |
+====================+==============================+=========================+====================+==================================+
| ``ContactInfo``    | yes for new order            | Contact information     |                    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | **Item**                     | **Mandatory**           | **Description**    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | ``Name``                     | yes                     | full name          |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | ``Email``                    | yes                     | email              |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | ``Phone``                    | yes                     | phone              |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | ``Comment``                  | yes                     | comment (optional) |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
| ``Tag``            | yes for new order            | Order reference         |                    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
| ``AccountComment`` | yes for XML-client has       | Comment for the account |                    |                                  |
|                    | right "View account comment" |                         |                    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
| ``OrderId``        | yes for service adding       | order id                |                    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
| ``Items``          | yes                          | Order items (hotels)    |                    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | **Item**                     | **Mandatory**           | **Description**    |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    | ``HotelItem``                | yes                     | Order item – Hotel |                                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    |                              | **Item**                | **Mandatory**      | **Description**                  |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    |                              | ``Search``              | yes                | Identifiers from search response |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+
|                    |                              | ``Rooms``               | yes                | Information by rooms             |
+--------------------+------------------------------+-------------------------+--------------------+----------------------------------+

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

- Mandatory item if you want to add new hotel to existing order.
- Attributes: no.
- Child items: no.

AccountComment item
-------------------

Comment for the account.

- Mandatory item if XML-client has right "View account comment".
- Attributes: no.
- Child items: no.

Items item
----------

Order items (hotels).

- Mandatory item.
- Attributes: no.

Child items:

+---------------+---------------+--------------------+----------------------------------+
| **Item**      | **Mandatory** | **Description**    |                                  |
+===============+===============+====================+==================================+
| ``HotelItem`` | yes           | Order item – hotel |                                  |
+---------------+---------------+--------------------+----------------------------------+
|               | **Item**      | **Mandatory**      | **Description**                  |
+---------------+---------------+--------------------+----------------------------------+
|               | ``Search``    | yes                | Identifiers from search response |
+---------------+---------------+--------------------+----------------------------------+
|               | ``Rooms``     | yes                | Information by rooms             |
+---------------+---------------+--------------------+----------------------------------+

HotelItem item
^^^^^^^^^^^^^^

Order item - hotel.

- Mandatory item.
- Attributes: no.

Child items:

+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
| **Item**                | **Mandatory** | **Description**                               |                 |                 |
+=========================+===============+===============================================+=================+=================+
| ``Search``              | yes           | Identifiers from search response              |                 |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
| ``AlternativesAllowed`` | no            | Is deprecated (value 'false' is only allowed) |                 |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
| ``DuplicatesAllowed``   | no            | Is duplicates allowed for this hotel          |                 |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
| ``PayForm``             | no            | Pay form of order                             |                 |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
| ``Rooms``               | yes           | Information by rooms                          |                 |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
|                         | **Item**      | **Mandatory**                                 | **Description** |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
|                         | ``Room``      | yes                                           | Rooms           |                 |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
|                         |               | **Item**                                      | **Mandatory**   | **Description** |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+
|                         |               | ``RoomPax``                                   | yes             | Paxes info      |
+-------------------------+---------------+-----------------------------------------------+-----------------+-----------------+

Search item
'''''''''''

- Mandatory item.
- Child items: no.

Attributes:

+---------------+----------+---------------+-----------------+
| **Attribute** | **Type** | **Mandatory** | **Description** |
+===============+==========+===============+=================+
| ``resultId``  | numeric  | yes           | result id       |
+---------------+----------+---------------+-----------------+
| ``searchId``  | numeric  | yes           | search id       |
+---------------+----------+---------------+-----------------+

AlternativesAllowed item
''''''''''''''''''''''''

This tag is deprecated. Value 'false' is only allowed.

- Child items: no.
- Attributes: no

DuplicatesAllowed item
''''''''''''''''''''''

If order duplicates is allowed. Values: true, false

Duplicate is an order, where the same hotel is booked with the same
check-in/check-out dates, for the same persons and from the same inner
supplier. If system find such order, it return error "E301" ("Similar
booking already exists"). For some hotels duplicates is not allowed.

Therefore even with DuplicatesAllowed = true system return error E301.

- Not mandatory item. By default: false
- Child items: no.
- Attributes: no

PayForm item
''''''''''''

Pay form of this order. Values: cash, cashless. Not mandatory item. By default: cash.

- Child items: no.
- Attributes: no

Rooms item
''''''''''

Rooms with information about people who are strictly in the order that
was passed in search response on the resultId.

- Mandatory item.
- Attributes: no.

Child items:

+----------+---------------+------------------+-------------------+------------------------------+
| **Item** | **Mandatory** | **Description**  |                   |                              |
+==========+===============+==================+===================+==============================+
| ``Room`` | yes           | Room information |                   |                              |
+----------+---------------+------------------+-------------------+------------------------------+
|          | **Item**      | **Mandatory**    | **Description**   |                              |
+----------+---------------+------------------+-------------------+------------------------------+
|          | ``RoomPax``   | yes              | Paxes information |                              |
+----------+---------------+------------------+-------------------+------------------------------+
|          |               | **Item**         | **Mandatory**     | **Description**              |
+----------+---------------+------------------+-------------------+------------------------------+
|          |               | ``Title``        | yes               | Title (Mr / Mrs / Ms / Chld) |
+----------+---------------+------------------+-------------------+------------------------------+
|          |               | ``FirstName``    | yes               | Name                         |
+----------+---------------+------------------+-------------------+------------------------------+
|          |               | ``LastName``     | yes               | Last name                    |
+----------+---------------+------------------+-------------------+------------------------------+

RoomPax item
            

Information about the person in the room. If the room has a child, it must come last in the list of Room! You don't need to give information about infants

- Mandatory item.

Attributes:

+---------------+----------+---------------+--------------------------------------------------------------------------+
| **Attribute** | **Type** | **Mandatory** | **Description**                                                          |
+===============+==========+===============+==========================================================================+
| ``child``     | boolean  | no            | true – if child                                                          |
+---------------+----------+---------------+--------------------------------------------------------------------------+
| ``age``       | numeric  | no            | age of child (2–18), if child=true. If age < 2, system will return error |
+---------------+----------+---------------+--------------------------------------------------------------------------+

Child items:

+---------------+---------------+------------------------------+
| **Item**      | **Mandatory** | **Description**              |
+===============+===============+==============================+
| ``Title``     | yes           | Title (Mr / Mrs / Ms / Chld) |
+---------------+---------------+------------------------------+
| ``FirstName`` | yes           | Name                         |
+---------------+---------------+------------------------------+
| ``LastName``  | yes           | Second name                  |
+---------------+---------------+------------------------------+

.. note:: **Attantion:** *``FullName`` item now is optional and will be remove from 01.01.2013*

Remarks item
''''''''''''

List of remarks.

- Optional item.
- Attributes: no.
 
Child items:

+------------+---------------+------------------------+
| **Item**   | **Mandatory** | **Description**        |
+============+===============+========================+
| ``Remark`` | yes           | Remark code e.g., "LA" |
+------------+---------------+------------------------+

Remark item
'''''''''''

Remark id.

- List of all remark codes - /xml/remark. Remark code is in Remark@tempattribute. 
- List of remarks that are possible for chosen hotel - */xml/hotel_modify_restrictions?search_id=[id_of_search]&result_id=[id_of_result]*.

Remark code in Hotel/PossibleRemarks/Remark@code attribute

- Attributes: no.
- Child items: no.

Comment item
''''''''''''

Free remark (text). Can be only in english

- Optional item.
- Attributes: no.
- Child items: no.

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

- Mandatory item.
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