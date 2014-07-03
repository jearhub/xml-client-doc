Voucher information
###################

Description of XML schema
=========================

A request for a voucher information is formed through URL (using GET method).

XSD-schema response:

-  ``www/xsd/VoucherInfoResponse.xsd``

Request
-------

Mandatory parameters:

-  ``order_id`` – order id
-  ``item_id`` – id order item (can be missed to receive information about all order items)

Request is passed via the URL with credentials(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/voucher_info``.

Response, VoucherInfoResponse
-----------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <VoucherInfoResponse>
      [<Errors><Error code="..." description="..."></Errors>]
      <Order Id="...">
        <ItemList>
          <Item Id="...">
            <VoucherAvailable>0|1</VoucherAvailable>
            <Voucher>
              <Issued>...</Issued>
              <BookingDetails>
                [<Supplier>...</Supplier>]
                [<Reference>...</Reference>]
                [<AdditionalDetailList>
                   <AdditionalDetail> - details
                     <Title>...</Title>
                     <Value>...</Value>
                   </AdditionalDetail>
                 </AdditionalDetailList>]
              </BookingDetails>
              <Hotel Id="...">
                <Name>...</Name>
                <Country>...</Country>
                <City>...</City>
                <Address>...</Address>
                <Email>...</Email>
                <Telephone>...</Telephone>
                <Fax>...</Fax>
                [<Map type="graphic|link">...</Map>]
                [<Position>
                   <Latitude>...</Latitude>
                   <Longitude>...</Longitude>
                 </Position>]
                [<AdditionalDetailList>
                   <AdditionalDetail>
                     <Title>...</Title>
                     <Value>...</Value>
                   </AdditionalDetail>
                 </AdditionalDetailList>]
              </Hotel>
              <RoomList>
                <Room Id="...">
                  <Name>...</Name>
                  <CheckInDate>...</CheckInDate>
                  <CheckOutDate>...</CheckOutDate>
                  <Duration>...</Duration>
                  <Paxes>...</Paxes>
                  <NumberOfRooms>...</NumberOfRooms>
                  [<AdditionalDetailList>
                     <AdditionalDetail>
                       <Title>...</Title>
                       <Value>...</Value>
                     </AdditionalDetail>
                   </AdditionalDetailList>]
                </Room>
              </RoomList>
              [<HotelRemarks>...</HotelRemarks>] - remarks
              [<AOTNumbers> - contacts
                 <Location name="...">...</Location>
               </AOTNumbers>]
              [<AdditionalInformation>...</AdditionalInformation>]
            </Voucher>
          </Item>
        </ItemList>
      </Order>
    </VoucherInfoResponse>

VoucherInfoResponse item
------------------------

Parent item.

Attributes: No.

Child items:

+--------+-----------+-------------------+
| Name   | Mandatory | Description       |
+========+===========+===================+
| Errors | No        | List of errors    |
+--------+-----------+-------------------+
| Order  | No        | Order information |
+--------+-----------+-------------------+

Errors item
-----------

List of errors.

Attributes: No.

Child items:

+-------+-----------+-----------------------------------+
| Name  | Mandatory | Description                       |
+=======+===========+===================================+
| Error | Yes       | Error description.                |
|       |           |                                   |
|       |           | Attributes:                       |
|       |           |                                   |
|       |           | - code - error code               |
|       |           | - description - error description |
+-------+-----------+-----------------------------------+

Order item
----------

Order information.

Attributes:

Name  Type  Mandatory Description
Id  Numeric Yes Order id

Child items:

+----------+-----------+---------------------+
| Name     | Mandatory | Description         |
+==========+===========+=====================+
| ItemList | Yes       | List of order items |
+----------+-----------+---------------------+

Order/ItemList item
-------------------

List of order items.

Attributes: No.

Child items:

+------+-----------+------------------------+
| Name | Mandatory | Description            |
+======+===========+========================+
| Item | Yes       | Order item description |
+------+-----------+------------------------+

Order/ItemList/Item item
------------------------

Item description.

Attributes:

+------+---------+-----------+-----------------------+
| Name | Type    | Mandatory | Description           |
+======+=========+===========+=======================+
| Id   | Numeric | Yes       | Order item identifier |
+------+---------+-----------+-----------------------+

Child items:

+------------------+-------+-----------------------+
| Name             | Type  | Mandatory Description |
+==================+=======+=======================+
| VoucherAvailable | 0 / 1 | Yes Has voucher       |
+------------------+-------+-----------------------+
| Voucher String   | Yes   | Voucher data          |
+------------------+-------+-----------------------+

Order/ItemList/Item/Voucher item
--------------------------------

Voucher information for item.

Attributes: No.

Child items:

+----------------+-----------+-------------------------------------------+
| Name           | Mandatory | Description                               |
+================+===========+===========================================+
| Issued         | Yes       | Voucher date                              |
+----------------+-----------+-------------------------------------------+
| BookingDetails | Yes       | Details about booking                     |
+----------------+-----------+-------------------------------------------+
| Hotel          | Yes       | Item description (hotel description)      |
+----------------+-----------+-------------------------------------------+
| RoomList       | Yes       | List of reserved rooms                    |
+----------------+-----------+-------------------------------------------+
| HotelRemarks   | No        | Remarks                                   |
+----------------+-----------+-------------------------------------------+
| AOTNumbers     | No        | Contact list for emergency communications |
+----------------+-----------+-------------------------------------------+

Order/ItemList/Item/Voucher/BookingDetails item
-----------------------------------------------

Details about booking

Attributes: No.

Child items:

+----------------------+--------------------------------+-----------------------+---------------------------------------+
| Name                 | Type                           | Mandatory Description |                                       |
+======================+================================+=======================+=======================================+
| Supplier             | String                         | No                    | Supplier name                         |
+----------------------+--------------------------------+-----------------------+---------------------------------------+
| Reference String     | No                             | Order reference       |                                       |
+----------------------+--------------------------------+-----------------------+---------------------------------------+
| AdditionalDetailList | List of AdditionalDetail items | No                    | List of additional data about booking |
+----------------------+--------------------------------+-----------------------+---------------------------------------+

Order/ItemList/Item/Voucher/BookingDetails/AdditionalDetailLists/AdditionalDetailList item
------------------------------------------------------------------------------------------

List of additional data about booking

Attributes: No.

Child items:

+------------------+-----------+-----------------------------------+
| Name             | Mandatory | Description                       |
+==================+===========+===================================+
| AdditionalDetail | No        | Additional details - child items: |
|                  |           |                                   |
|                  |           | - Title - parameter name          |
|                  |           | - Value - value                   |
+------------------+-----------+-----------------------------------+

Order/ItemList/Item/Voucher/Hotel item
--------------------------------------

Hotel information (item).

Attributes:

+------+-----------+-----------------------+
| Name | Mandatory | Description           |
+======+===========+=======================+
| Id   | Yes       | Order item id (hotel) |
+------+-----------+-----------------------+

Child items:

+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Name                 | Type                           | Mandatory | Description                                                           |
+======================+================================+===========+=======================================================================+
| Name                 | String                         | Yes       | Hotel name                                                            |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Country              | String                         | Yes       | Country name                                                          |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| City                 | String                         | Yes       | City name                                                             |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Address              | String                         | Yes       | Hotel address                                                         |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Email                | String                         | Yes       | Email                                                                 |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Telephone            | String                         | Yes       | Phone                                                                 |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Fax                  | String                         | Yes       | Fax                                                                   |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Map                  | String                         | No        | Map. Attributes: type - graphic / link                                |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| Position             | Nested                         | No        | Latitude and longitude of the hotel, if such information is available |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+
| AdditionalDetailList | List of AdditionalDetail items | No        | List of additional details                                            |
+----------------------+--------------------------------+-----------+-----------------------------------------------------------------------+

Order/ItemList/Item/Voucher/Hotel/Position item
-----------------------------------------------

Latitude and longitude of the hotel, if such information is available.

Attributes: No.

Child items:

+-----------+--------+-----------+-------------+
| Name      | Type   | Mandatory | Description |
+===========+========+===========+=============+
| Latitude  | String | Yes       | Latitude    |
+-----------+--------+-----------+-------------+
| Longitude | String | Yes       | Longitude   |
+-----------+--------+-----------+-------------+

Order/ItemList/Item/Voucher/RoomList item
-----------------------------------------

List of reserved rooms.

Attributes: No.

Child items:

+------+-----------+-------------+
| Name | Mandatory | Description |
+======+===========+=============+
| Room | Yes       | Room data   |
+------+-----------+-------------+

Order/ItemList/Item/Voucher/RoomList/Room item
----------------------------------------------

Room data.

Attributes:

+------+-----------------------+---------+
| Name | Mandatory Description |         |
+======+=======================+=========+
| Id   | Yes                   | Room id |
+------+-----------------------+---------+

Child items:

+----------------------+--------------------------------+-----------------------+-----------------------------+
| Name                 | Type                           | Mandatory Description |                             |
+======================+================================+=======================+=============================+
| Name                 | String                         | Yes                   | Room name                   |
+----------------------+--------------------------------+-----------------------+-----------------------------+
| CheckInDate          | Date                           | Yes                   | Check in date               |
+----------------------+--------------------------------+-----------------------+-----------------------------+
| CheckOutDate         | Date                           | Yes                   | Check out date              |
+----------------------+--------------------------------+-----------------------+-----------------------------+
| Duration             | Numeric                        | Yes                   | Duration (nights)           |
+----------------------+--------------------------------+-----------------------+-----------------------------+
| Paxes                | String                         | Yes                   | Full name of person in room |
+----------------------+--------------------------------+-----------------------+-----------------------------+
| NumberOfRooms        | Numeric                        | Yes                   | Number of rooms             |
+----------------------+--------------------------------+-----------------------+-----------------------------+
| AdditionalDetailList | List of AdditionalDetail items | No                    | Additional details          |
+----------------------+--------------------------------+-----------------------+-----------------------------+


Order/ItemList/Item/Voucher/HotelRemarks item
----------------------------------------------

Remarks

Attributes: No.

Child items: No.


Order/ItemList/Item/Voucher/AOTNumbers item
-------------------------------------------

Contact list for emergency communications. 

Attributes: No.

Child items:

+----------+--------+--------------------------------------------------------------------------+
| Name     | Type   | Mandatory Description                                                    |
+==========+========+==========================================================================+
| Location | String | Yes Phones for the city specified in the attribute: ``name`` - city name |
+----------+--------+--------------------------------------------------------------------------+
