Add order / Add service
#######################

Description of XML schema
=========================
XSD-schema:

-  ``www/xsd/AddOrderRequest.xsd``
-  ``www/xsd/AddOrderResponse.xsd``

After the transfer was searched, you can create an order with one or
more transfers. When you create an order, indicate contact information:
full name, email address, phone number and if you want to comment on the
request. Also contains information on persons in the room. For each
number indicates the number of people strong, with a child, if there is
one in the room - comes last.

Also with this request you can add new service (transfer) to the
existing order. You must indicate order id for this case.

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
        <TransferItem>
          <Search
            resultId=".." - result id in search results
            searchId=".." - search id
          />
          [<PayForm>cash|cashless<PayForm>] - pay form (must be the same for all items in order), may be missed for existing order
          <LeadingPax>
             <Title>Mr|Mrs|Ms|Chld</Title>
             <FirstName>..</FirstName>
             <LastName>..</LastName>
             [<Phone>..</Phone>]
          </LeadingPax>
          <PickUp>
            <AirportId>..</AirportId>
            <FlightNum>..</FlightNum>
            <ArrivalAirportId>..</ArrivalAirportId>
            <Time>..</Time>
            or
            <StationId>..</StationId>
            <TrainNum>..</TrainNum>
            <ArrivalCityId>..</ArrivalCityId>
            <Time>..</Time>
            or
            <HotelId>..</HotelId>
            <Time>..</Time>
            or
            <Address>
               <AddressLine>..</AddressLine>
               [<AddressLine>..</AddressLine>]
            </Address>
            <ZipCode>..</ZipCode>
            <District>..</District>
            <Phone>..</Phone>
            <Time>..</Time>
            or
            <ShipName>..</ShipName>
            <ShipCompanyName>..</ShipCompanyName>
            <ArrivalCity>..</ArrivalCity>
            <Time>..</Time>
          </PickUp>
          <DropOff>
              <AirportId>..</AirportId>
              <FlightNum>..</FlightNum>
              <DepartureAirportId>..</ArrivalAirportId>
              <Time>..</Time>
              or
              <StationId>..</StationId>
              <TrainNum>..</TrainNum>
              <DepartureCityId>..</ArrivalCityId>
              <Time>..</Time>
              or
              <HotelId>..</HotelId>
              or
              <Address>
                 <AddressLine>..</AddressLine>
                 [<AddressLine>..</AddressLine>]
              </Address>
              <ZipCode>..</ZipCode>
              <District>..</District>
              <Phone>..</Phone>
              or
              <ShipName>..</ShipName>
              <ShipCompanyName>..</ShipCompanyName>
              <DepartureCity>..</ArrivalCity>
              <Time>..</Time>
          </DropOff>
        </TransferItem>
      </Items>
    </AddOrderRequest>

AddOrderRequest item
--------------------

Parent item.

- Attributes: no.

Child items:

+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
| **Item**           | **Mandatory**                | **Description**         |                       |                                  |
+====================+==============================+=========================+=======================+==================================+
| ``ContactInfo``    | yes for new order            | Contact information     |                       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | **Item**                     | **Mandatory**           | **Description**       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | ``Name``                     | yes                     | full name             |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | ``Email``                    | yes                     | email                 |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | ``Phone``                    | yes                     | phone                 |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | ``Comment``                  | yes                     | comment (optional)    |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
| ``Tag``            | yes for new order            | Order reference         |                       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
| ``AccountComment`` | yes for XML-client has       | Comment for the account |                       |                                  |
|                    | right "View account comment" |                         |                       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
| ``OrderId``        | yes for service adding       | order id                |                       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
| ``Items``          | yes                          | Order items             |                       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | **Item**                     | **Mandatory**           | **Description**       |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    | ``TransferItem``             | yes                     | Order item – Transfer |                                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    |                              | **Item**                | **Mandatory**         | **Description**                  |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    |                              | ``Search``              | yes                   | Identifiers from search response |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    |                              | ``PayForm``             | yes for new order     | Pay form of item                 |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    |                              | ``LeadingPax``          | yes                   | Transfer leader pax              |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    |                              | ``PickUp``              | yes                   | Pick up parameters               |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+
|                    |                              | ``DropOff``             | yes                   | Drop off parameters              |
+--------------------+------------------------------+-------------------------+-----------------------+----------------------------------+

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

AccountComment item
-------------------

Comment for the account.

- Mandatory item if XML-client has right "View account comment".
- Attributes: no.
- Child items: no.

OrderId item
------------

Identifier of existing order.

- Mandatory item if you want to add new transfer to existing order.
- Attributes: no.
- Child items: no.

Items item
----------

Order items (transfer).

- Mandatory item.
- Attributes: no.
- Child items:

+------------------+----------------+-----------------------+----------------------------------+
| **Item**         | **Mandatory**  | **Description**       |                                  |
+==================+================+=======================+==================================+
| ``TransferItem`` | yes            | Order item – transfer |                                  |
+------------------+----------------+-----------------------+----------------------------------+
|                  | **Item**       | **Mandatory**         | **Description**                  |
+------------------+----------------+-----------------------+----------------------------------+
|                  | ``Search``     | yes                   | Identifiers from search response |
+------------------+----------------+-----------------------+----------------------------------+
|                  | ``PayForm``    | yes for new order     | Pay form of item                 |
+------------------+----------------+-----------------------+----------------------------------+
|                  | ``LeadingPax`` | yes                   | Transfer leader pax              |
+------------------+----------------+-----------------------+----------------------------------+
|                  | ``PickUp``     | yes                   | Pick up parameters               |
+------------------+----------------+-----------------------+----------------------------------+
|                  | ``DropOff``    | yes                   | Drop off parameters              |
+------------------+----------------+-----------------------+----------------------------------+

TransferItem item
^^^^^^^^^^^^^^^^^

Order item - transfer.

- Mandatory item.
- Attributes: no.

Child items:

+----------------+-------------------+----------------------------------+
| **Item**       | **Mandatory**     | **Description**                  |
+================+===================+==================================+
| ``Search``     | yes               | Identifiers from search response |
+----------------+-------------------+----------------------------------+
| ``PayForm``    | yes for new order | Pay form of item                 |
+----------------+-------------------+----------------------------------+
| ``LeadingPax`` | yes               | Transfer leader pax              |
+----------------+-------------------+----------------------------------+
| ``PickUp``     | yes               | Pick up parameters               |
+----------------+-------------------+----------------------------------+
| ``DropOff``    | yes               | Drop off parameters              |
+----------------+-------------------+----------------------------------+

Search item
'''''''''''

Mandatory item.

- Child items: no.

Attributes:

+---------------+----------+---------------+-----------------+
| **Attribute** | **Type** | **Mandatory** | **Descriptoin** |
+===============+==========+===============+=================+
| ``resultId``  | numeric  | yes           | result id       |
+---------------+----------+---------------+-----------------+
| ``searchId``  | numeric  | yes           | search id       |
+---------------+----------+---------------+-----------------+

PayForm item
''''''''''''

Pay form of this order. Values: cash, cashless. Not mandatory item. By default: cash.

- Child items: no.
- Attributes: no

LeadingPax item
'''''''''''''''

Leader pax of transfer.

- Mandatory: yes.
- Attributes: no.

Child items:

+---------------+-------------------+---------------+---------------------------------+
| **Item**      | **Type**          | **Mandatory** | **Description**                 |
+===============+===================+===============+=================================+
| ``Title``     | Mr, Ms, Mrs, Chld | yes           | Pax title                       |
+---------------+-------------------+---------------+---------------------------------+
| ``FirstName`` | string            | yes           | Pax name                        |
+---------------+-------------------+---------------+---------------------------------+
| ``LastName``  | string            | yes           | Pax surname                     |
+---------------+-------------------+---------------+---------------------------------+
| ``Phone``     | string            | no            | Phone (for UTS Hotels provider) |
+---------------+-------------------+---------------+---------------------------------+

PickUp item
'''''''''''

Pick up parameters.

- Mandatory: yes.
- Attributes: no.

Child items (transfer location - airport):

+----------------------+----------+---------------+----------------------+
| **Item**             | **Type** | **Mandatory** | **Description**      |
+======================+==========+===============+======================+
| ``AirportId``        | number   | yes           | airport id           |
+----------------------+----------+---------------+----------------------+
| ``FlightNum``        | string   | yes           | flight number        |
+----------------------+----------+---------------+----------------------+
| ``ArrivalAirportId`` | number   | yes           | departure airport id |
+----------------------+----------+---------------+----------------------+
| ``Time``             | HH:SS    | yes           | arrival time         |
+----------------------+----------+---------------+----------------------+

Child items (transfer location - station):

+-------------------+----------+---------------+-------------------+
| **Item**          | **Type** | **Mandatory** | **Description**   |
+===================+==========+===============+===================+
| ``StationId``     | number   | yes           | station id        |
+-------------------+----------+---------------+-------------------+
| ``TrainNum``      | string   | yes           | train number      |
+-------------------+----------+---------------+-------------------+
| ``ArrivalCityId`` | number   | yes           | departure city id |
+-------------------+----------+---------------+-------------------+
| ``Time``          | HH:SS    | yes           | arrival time      |
+-------------------+----------+---------------+-------------------+

Child item (transfer location - hotel):

+-------------+----------+---------------+-----------------+
| **Item**    | **Type** | **Mandatory** | **Description** |
+=============+==========+===============+=================+
| ``HotelId`` | number   | yes           | hotel id        |
+-------------+----------+---------------+-----------------+
| ``Time``    | HH:SS    | yes           | arrival time    |
+-------------+----------+---------------+-----------------+

Child item (transfer location - adress):

+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| **Item**     | **Type**                    | **Mandatory** | **Description**                                                                     |
+==============+=============================+===============+=====================================================================================+
| ``Address``  | nested                      | yes           | address in one or two lines (nested items ``AddressLine``), each upto 40 characters |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``ZipCode``  | string (upto 10 characters) | yes           | zip code                                                                            |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``District`` | string (upto 20 characters) | yes           | district name                                                                       |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``Phone``    | string                      | yes           | phone number                                                                        |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``Time``     | HH:SS                       | yes           | arrival time                                                                        |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+

Child items (transfer location - port):

+---------------------+----------+---------------+---------------------+
| **Item**            | **Type** | **Mandatory** | **Description**     |
+=====================+==========+===============+=====================+
| ``ShipName``        | string   | yes           | ship name           |
+---------------------+----------+---------------+---------------------+
| ``ShipCompanyName`` | string   | yes           | ship company name   |
+---------------------+----------+---------------+---------------------+
| ``ArrivalCity``     | string   | yes           | departure city name |
+---------------------+----------+---------------+---------------------+
| ``Time``            | HH:SS    | yes           | arrival time        |
+---------------------+----------+---------------+---------------------+

DropOff item
''''''''''''

Drop off parameters.

- Mandatory: yes.
- Attributes: no.

Child items (transfer location - airport):

+------------------------+----------+---------------+--------------------+
| **Item**               | **Type** | **Mandatory** | **Description**    |
+========================+==========+===============+====================+
| ``AirportId``          | number   | yes           | airport id         |
+------------------------+----------+---------------+--------------------+
| ``FlightNum``          | string   | yes           | flight number      |
+------------------------+----------+---------------+--------------------+
| ``DepartureAirportId`` | number   | yes           | arrival airport id |
+------------------------+----------+---------------+--------------------+
| ``Time``               | HH:SS    | yes           | departure time     |
+------------------------+----------+---------------+--------------------+

Child items (transfer location - station):

+---------------------+----------+---------------+-----------------+
| **Item**            | **Type** | **Mandatory** | **Description** |
+=====================+==========+===============+=================+
| ``StationId``       | number   | yes           | station id      |
+---------------------+----------+---------------+-----------------+
| ``TrainNum``        | string   | yes           | train number    |
+---------------------+----------+---------------+-----------------+
| ``DepartureCityId`` | number   | yes           | arrival city id |
+---------------------+----------+---------------+-----------------+
| ``Time``            | HH:SS    | yes           | departure time  |
+---------------------+----------+---------------+-----------------+

Child item (transfer location - hotel):

+-------------+----------+---------------+-----------------+
| **Item**    | **Type** | **Mandatory** | **Description** |
+=============+==========+===============+=================+
| ``HotelId`` | number   | yes           | hotel id        |
+-------------+----------+---------------+-----------------+

+-------------+----------+---------------+-----------------+
| **Item**    | **Type** | **Mandatory** | **Description** |
+=============+==========+===============+=================+
| ``HotelId`` | number   | yes           | hotel id        |
+-------------+----------+---------------+-----------------+
| ``Time``    | HH:SS    | yes           | arrival time    |
+-------------+----------+---------------+-----------------+

Child item (transfer location - adress):

+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| **Item**     | **Type**                    | **Mandatory** | **Description**                                                                     |
+==============+=============================+===============+=====================================================================================+
| ``Address``  | nested                      | yes           | address in one or two lines (nested items ``AddressLine``), each upto 40 characters |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``ZipCode``  | string (upto 10 characters) | yes           | zip code                                                                            |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``District`` | string (upto 20 characters) | yes           | district name                                                                       |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``Phone``    | string                      | yes           | phone number                                                                        |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``Time``     | HH:SS                       | yes           | arrival time                                                                        |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+

Child items (transfer location - port):

+---------------------+----------+---------------+---------------------+
| **Item**            | **Type** | **Mandatory** | **Description**     |
+=====================+==========+===============+=====================+
| ``ShipName``        | string   | yes           | ship name           |
+---------------------+----------+---------------+---------------------+
| ``ShipCompanyName`` | string   | yes           | ship company name   |
+---------------------+----------+---------------+---------------------+
| ``ArrivalCity``     | string   | yes           | departure city name |
+---------------------+----------+---------------+---------------------+
| ``Time``            | HH:SS    | yes           | arrival time        |
+---------------------+----------+---------------+---------------------+

DropOff item
''''''''''''

Drop off parameters.

- Mandatory: yes.
- Attributes: no.

Child items (transfer location - airport):

+------------------------+----------+---------------+--------------------+
| **Item**               | **Type** | **Mandatory** | **Description**    |
+========================+==========+===============+====================+
| ``AirportId``          | number   | yes           | airport id         |
+------------------------+----------+---------------+--------------------+
| ``FlightNum``          | string   | yes           | flight number      |
+------------------------+----------+---------------+--------------------+
| ``DepartureAirportId`` | number   | yes           | arrival airport id |
+------------------------+----------+---------------+--------------------+
| ``Time``               | HH:SS    | yes           | departure time     |
+------------------------+----------+---------------+--------------------+

Child items (transfer location - station):

+---------------------+----------+---------------+-----------------+
| **Item**            | **Type** | **Mandatory** | **Description** |
+=====================+==========+===============+=================+
| ``StationId``       | number   | yes           | station id      |
+---------------------+----------+---------------+-----------------+
| ``TrainNum``        | string   | yes           | train number    |
+---------------------+----------+---------------+-----------------+
| ``DepartureCityId`` | number   | yes           | arrival city id |
+---------------------+----------+---------------+-----------------+
| ``Time``            | HH:SS    | yes           | departure time  |
+---------------------+----------+---------------+-----------------+

Child item (transfer location - hotel):

+-------------+----------+---------------+-----------------+
| **Item**    | **Type** | **Mandatory** | **Description** |
+=============+==========+===============+=================+
| ``HotelId`` | number   | yes           | hotel id        |
+-------------+----------+---------------+-----------------+

Child item (transfer location - adress):

+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| **Item**     | **Type**                    | **Mandatory** | **Description**                                                                     |
+==============+=============================+===============+=====================================================================================+
| ``Address``  | nested                      | yes           | address in one or two lines (nested items ``AddressLine``), each upto 40 characters |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``ZipCode``  | string (upto 10 characters) | yes           | zip code                                                                            |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``District`` | string (upto 20 characters) | yes           | district name                                                                       |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+
| ``Phone``    | string                      | yes           | phone number                                                                        |
+--------------+-----------------------------+---------------+-------------------------------------------------------------------------------------+

Child items (transfer location - port):

+---------------------+----------+---------------+-------------------+
| **Item**            | **Type** | **Mandatory** | **Description**   |
+=====================+==========+===============+===================+
| ``ShipName``        | string   | yes           | ship name         |
+---------------------+----------+---------------+-------------------+
| ``ShipCompnayName`` | string   | yes           | ship company name |
+---------------------+----------+---------------+-------------------+
| ``DepartureCity``   | string   | yes           | arrival city name |
+---------------------+----------+---------------+-------------------+
| ``Time``            | HH:SS    | yes           | departure time    |
+---------------------+----------+---------------+-------------------+

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