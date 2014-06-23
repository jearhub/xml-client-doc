Modify order
############

Description of XML schema
=========================

XSD-schema:

-  ``www/xsd/ModifyOrderRequest.xsd``
-  ``www/xsd/ModifyOrderResponse.xsd``

After the order was created, you can modify one or more hotels in
created order. When you modify an order, indicate order id and list of
items (with item id), that you want to modify. Also indicate room id, if
you modify existing rooms. If you want to add room, skip room id for
this room. For room deletion skip whole room in request. You can modify
room size, type, view, cots, hotel check in and duration. All
identificators (order id, item id, room id) can be found in OrderInfoResponse

Also add to request information on persons in the room. For each room
indicates the number of people strong, with a child, if there is one in
the room - comes last. Number of people must correspond to new room
size. You can add child to the room or remove him from it.

Draw attention that in specific hotel some of its options can be denied
for modification. List of editable options can be take from
OrderInfoResponse. Also the list of rooms, that locked for modification
must be taken from OrderInfoResponse

Request
-------

XML-schema:

::


    <?xml version="1.0" encoding="utf-8"?>
    <ModifyOrderRequest>
      [<ContactInfo> - contact information
        <Name>..</Name> - name
        <Email>..</Email> - email
        <Phone>..</Phone> - phone
        <Comment>..</Comment> - comment
      </ContactInfo>]
      <OrderId>..</OrderId> - order id
      [<AccountComment>..</AccountComment> - Comment for the account  
      [<PayForm>cash|cashless</PayForm>] - order pay from
      <Items> - order items
        <HotelItem> - hotel
          <ItemId>..</ItemId> - item id
          <CheckIn>YYYY-MM-DD</CheckIn> - check in date
          <Duration>..</Duration> - duration
          <Rooms> - room in hotel
            <Room
                  [roomId=".."] - id of existing room (or skip this id for room adding)
                  roomSizeId=".." - room size id
                  roomTypeId=".." - room type id
                  roomViewId=".." - room view id
                  cots="0|1|2" - number of cots in room
                  sharingBedding="true|false" - room has sharing bedding or not
        >
              <RoomPax [child="true|false"] [age=".."]> - paxes in room
                <Title>Mr|Mrs|Ms|Chld</Title> - title
                <FirstName>..</FirstName> - name
                <LastName>..</LastName> - surname
              </RoomPax>
            </Room>
          </Rooms>
          [<Remarks> - list of remarks (Optional item)
             <Remark>remark_id</Remark>
          </Remarks>]
          [<Comment>...</Comment>] - free remark (Optional item)
        </HotelItem>
      </Items>
    </ModifyOrderRequest>

ModifyOrderRequest item
-----------------------

- Parent item.
- Attributes: no.

Child items:

+--------------------+---------------+-------------------------+--------------------+----------------------+
| **Item**           | **Mandatory** | **Description**         |                    |                      |
+====================+===============+=========================+====================+======================+
| ``ContactInfo``    | no            | Contact information     |                    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | **Item**      | **Mandatory**           | **Description**    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | ``Name``      | yes                     | full name          |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | ``Email``     | yes                     | email              |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | ``Phone``     | yes                     | phone              |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | ``Comment``   | yes                     | comment (optional) |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
| ``OrderId``        | yes           | id of existing order    |                    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
| ``AccountComment`` | no            | comment for the account |                    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
| ``PayForm``        | no            | New order pay form      |                    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
| ``Items``          | yes           | Order items (hotels)    |                    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | **Item**      | **Mandatory**           | **Description**    |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    | ``HotelItem`` | yes                     | Order item – Hotel |                      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    |               | **Item**                | **Mandatory**      | **Description**      |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    |               | ``ItemId``              | yes                | id of existing item  |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    |               | ``CheckIn``             | yes                | check-in date        |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    |               | ``Duration``            | yes                | number of nights     |
+--------------------+---------------+-------------------------+--------------------+----------------------+
|                    |               | ``Rooms``               | yes                | Information by rooms |
+--------------------+---------------+-------------------------+--------------------+----------------------+

ContactInfo item
----------------

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

Items item
----------

Order items (hotels).

- Mandatory item.
- Attributes: no.

Child items:

+---------------+---------------+--------------------+-------------------------------------+
| **Item**      | **Mandatory** | **Description**    |                                     |
+===============+===============+====================+=====================================+
| ``HotelItem`` | yes           | Order item – hotel |                                     |
+---------------+---------------+--------------------+-------------------------------------+
|               | **Item**      | **Mandatory**      | **Description**                     |
+---------------+---------------+--------------------+-------------------------------------+
|               | ``ItemId``    | yes                | Identifier of order item            |
+---------------+---------------+--------------------+-------------------------------------+
|               | ``CheckIn``   | yes                | New check-in date for this hotel    |
+---------------+---------------+--------------------+-------------------------------------+
|               | ``Duration``  | yes                | New number of nights for this hotel |
+---------------+---------------+--------------------+-------------------------------------+
|               | ``Rooms``     | yes                | Information by rooms                |
+---------------+---------------+--------------------+-------------------------------------+

HotelItem item
^^^^^^^^^^^^^^

Order item - hotel.

- Mandatory item.
- Attributes: no.

Child items:

+--------------+---------------+--------------------------------+-----------------+-----------------+
| **Item**     | **Mandatory** | **Description**                |                 |                 |
+==============+===============+================================+=================+=================+
| ``ItemId``   | yes           | Identify of order item         |                 |                 |
+--------------+---------------+--------------------------------+-----------------+-----------------+
| ``CheckIn``  | yes           | New check-in date for hotel    |                 |                 |
+--------------+---------------+--------------------------------+-----------------+-----------------+
| ``Duration`` | yes           | New number of nights for hotel |                 |                 |
+--------------+---------------+--------------------------------+-----------------+-----------------+
| ``Rooms``    | yes           | Information by rooms           |                 |                 |
+--------------+---------------+--------------------------------+-----------------+-----------------+
|              | **Item**      | **Mandatory**                  | **Description** |                 |
+--------------+---------------+--------------------------------+-----------------+-----------------+
|              | ``Room``      | yes                            | Rooms           |                 |
+--------------+---------------+--------------------------------+-----------------+-----------------+
|              |               | **Item**                       | **Mandatory**   | **Description** |
+--------------+---------------+--------------------------------+-----------------+-----------------+
|              |               | ``RoomPax``                    | yes             | Paxes info      |
+--------------+---------------+--------------------------------+-----------------+-----------------+

Rooms item
''''''''''

Rooms with information about people who are strictly in the order that
was passed in OrderInfo response.

You can change room size, type, view for existing rooms (for this you
must identify room id). Also you can add or remove rooms. For room
addition add room without id in OrderModify request. For room removing
just skip room in OrderModify request. Mandatory item.

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

Room item
'''''''''

Information about room and about the person in the room. To modify
existing room you must identify room by it id. And vice versa, to add
new room don't identify any room id. For room removing don't specify
room in request

- Mandatory item.

Attributes:

+--------------------+---------------+---------------+-----------------------------------------------+
| **Attribute**      | **Type**      | **Mandatory** | **Description**                               |
+====================+===============+===============+===============================================+
| ``roomId``         | numeric       | no            | id of existing room                           |
+--------------------+---------------+---------------+-----------------------------------------------+
| ``roomSizeId``     | numeric       | yes           | New or existing room size id (/xml/room_size) |
+--------------------+---------------+---------------+-----------------------------------------------+
| ``roomTypeId``     | numeric       | yes           | New or existing room type id (/xml/room_type) |
+--------------------+---------------+---------------+-----------------------------------------------+
| ``roomViewId``     | numeric       | yes           | New or existing room view id (/xml/room_view) |
+--------------------+---------------+---------------+-----------------------------------------------+
| ``cots``           | 0 or 1 or 2   | yes           | New or existing number of cots                |
+--------------------+---------------+---------------+-----------------------------------------------+
| ``sharingBedding`` | true or false | yes           | New or existing flag of sharing bedding       |
+--------------------+---------------+---------------+-----------------------------------------------+

Child items: no

RoomPax item
''''''''''''

Information about the person in the room. If the room has a child, it
must come last in the list of Room!

- Mandatory item.

Attributes:

+---------------+----------+---------------+------------------------------------+
| **Attribute** | **Type** | **Mandatory** | **Description**                    |
+===============+==========+===============+====================================+
| ``child``     | boolean  | no            | true – if child                    |
+---------------+----------+---------------+------------------------------------+
| ``age``       | numeric  | no            | age of child (2–18), if child=true |
+---------------+----------+---------------+------------------------------------+

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

Remarks item
''''''''''''

List of remarks.

- Optional item.
- Attributes: no.

Child items:

+--------------+-----------------+--------------------------+
| **Item**     | **Mandatory**   | **Description**          |
+--------------+-----------------+--------------------------+
| ``Remark``   | yes             | Remark code e.g., "LA"   |
+--------------+-----------------+--------------------------+

Remark item
'''''''''''

Remark id.

List of all remark codes - /xml/remark. Remark code is in Remark@temp attribute. 
List of remarks that are possible for chosen hotel - */xml/hotel_modify_restrictions?search_id=[id_of_search]&result_id=[id_of_result]*.

Remark code in Hotel/PossibleRemarks/Remark@code attribute

- Attributes: no.
- Child items: no.

Comment item
''''''''''''

Free remark (text). Can be only in english

- Optional item.
- Attributes: no.
- Child items: no.

Response, ModifyOrderResponse
-----------------------------

Response pattern is the same as in response to a request for information about order (``OrderInfoResponse``).