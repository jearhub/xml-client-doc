Order confirmation
##################

Description of XML schema
=========================

A request is formed through URL (using GET method).

XSD-schema response:

-  :download:`www/xsd/order/ConfirmOrderResponse.xsd <../../themes/hotelbook/static/xsd/order/ConfirmOrderResponse.xsd>`

Request
-------

The request must be an parameter - order\_id, taken from the response to
the AddOrder request. Request is passed via the URL with
credentials(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/confirm_order``


Response, ConfirmOrderResponse
-------------------------------

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>

        <ConfirmOrderResponse>
         [<Errors>
            <Error code="..." description="..."> - erros
          </Errors>]
          [<Changes>
            <Change itemId="...">
              [<title>price</title>]
              [<NewValue>...</NewValue>]
            </Change>
          </Changes>]
          <Order>

            <Id>...</Id> - order id
            <Tag>...</Tag> - order reference (for new order)
            <State>...</State> - order status
            [<Account_1C> - Information about the account 1C
                <Document type="..." download="..." date="..." num="..." currency_date="..."total_sum="..."> - information about the document
            </Account_1C>]
            <Paxes>

              <Pax paxId="..." child="true|false"  isLeader="true|false" childAge="1...21"> - pax data
                <Title>...</Title>

                <FirstName>...</FirstName>

                <LastName>...</LastName>
              </Pax>

            </Paxes>
            <Items>

              <HotelItem itemId="40036"> - order item (hotel)
                <HotelId>...</HotelId> - hotel id 
                <CityId>...</CityId> - city id
                <Name>...</Name> - hotel name
                <CategoryId>...</CategoryId> - Category id
                <State>...</State> - order item status
                <CheckIn>...</CheckIn> - Check in
                <Duration>...</Duration>
                <TotalPrice>...</TotalPrice>
                <ExtraPrice currency="USD" >...</ExtraPrice>
                <Currency>...</Currency>
                <HotelPaid>true|false</HotelPaid>
                <UseNds>true|false</UseNds>
                <SpecialOfferText>...</SpecialOfferText>
                <ProviderId>...</ProviderId>
                [<ProviderReference>...</ProviderReference>] - Provider reference
                <Rooms>

                  <Room
                     roomName="..."
                     mealId="..." mealName="..."

                     mealBreakfastId="..." mealBreakfastName="..."
                     child="0|1" cots="0|1|2" sharingBedding="true|false"

                     >
                     <Paxes>
                       <PaxId>...</PaxId>
                     </Paxes>
                  </Room>

                </Rooms>

                <Remarks> - Remarks order
                  [<Remark>...</Remark>]
                </Remarks>
                <ChargeConditions>

                  <Currency>..</Currency>
                  <Cancellations> 
                    <Cancellation

                      charge="true|false" 

                      [from="2008-02-28T11:50:00"]
                      [to="2008-02-28T11:50:00"]

                      [price="100.00"]
                      [policy="1 ночь"]

                    />
                  </Cancellations>
                  <Amendments>
                    <Amendment
                      charge="true|false"

                      [from="YYYY-MM-DDThh:ii:ss"]
                      [to="YYYY-MM-DDThh:ii:ss"]
                      [price=".."]

                      [policy=".."]

                    />
                  </Amendments>
                </ChargeConditions>

                <PriceDetails>
                  <Currency>..</Currency> 
                 [<Discount>..</Discount>]
                 [<Offer>..</Offer>] 
                  <RoomPrices>

                    <Room 
                      roomNumber=".." 
                      roomSizeId=".."
                      roomTypeId=".."
                      roomViewId=".."
                      child="0|1" 

                     [cots="1|2"] 
                      >
                      <Price 

                        date="YYYY-MM-DD"

                        available="true|false" 
                        price=".." 

                       [priceChild=".."]

                       [priceCot=".."]

                      />
                    </Room>
                  </RoomPrices>
                </PriceDetails>

              </HotelItem>

            </Items>
            <ContactInfo> 
              <Name>...</Name>
              <Email>...</Email>

              <Phone>...</Phone>
              <Comment>...</Comment>
            </ContactInfo>
          </Order>
        </ConfirmOrderResponse>


ConfirmOrderResponse item
----------------------------

- Parent item.
- Attributes: no.

Child items:

+---------+-------------------------------------+--------------------------+
| Item    | Mandatory                           | Description              |
+=========+=====================================+==========================+
| Errors  | No                                  | List of errors           |
+---------+-------------------------------------+--------------------------+
| Changes | No                                  | Alteration of an order   |
+---------+-------------------------------------+--------------------------+
| Order   | No                                  | Order                    |
+---------+-------------------------------------+--------------------------+

Errors item
------------

View :doc:`Error page <../errors>`

Changes item
------------
alteration of an order

- Attributes: no.

Child items: Change.


Changes/Change item
-------------------

- *Attributes: itemId - id item.

Child items:

+----------+-------------------------------------+------------------------------+---------+-----------+
| Item     | Mandatory                           | Description                  | Type    | Attribute |
+==========+=====================================+==============================+=========+===========+
| Title    | no                                  | price                        | String  | no        |
+----------+-------------------------------------+------------------------------+---------+-----------+
| NewValue | no                                  | new value price              | String  | no        |
+----------+-------------------------------------+------------------------------+---------+-----------+

Order item
-------------

description of the order

- *Attributes: no.*

Child items:

+-------------+------------------------+--------------+---------------------------------------------------------+
| Item        | Type                   | Mandatory    | Description                                             |
+=============+========================+==============+=========================================================+
| Id          | Numeric                | Yes          | Order id                                                |
+-------------+------------------------+--------------+---------------------------------------------------------+
| Manager     | String                 | Нет          | Manager                                                 |
+-------------+------------------------+--------------+---------------------------------------------------------+
| Tag         | String                 | Yes          | order reference                                         |
+-------------+------------------------+--------------+---------------------------------------------------------+
| State       | String                 | Yes          | order state (new, modified, cancelled, etc.)            |
+-------------+------------------------+--------------+---------------------------------------------------------+
| Account_1C  | List of Document items | no           | Account information 1C                                  |
+-------------+------------------------+--------------+---------------------------------------------------------+
| Paxes       | List                   | Yes          | List of paxes in order                                  |
+-------------+------------------------+--------------+---------------------------------------------------------+
| Items       | List                   | Yes          | List of items (hotels)                                  |
+-------------+------------------------+--------------+---------------------------------------------------------+
| ContactInfo | Nested                 | Yes          | Contact information about customer                      |
+-------------+------------------------+--------------+---------------------------------------------------------+

item Order/Account_1C
----------------------

List of accounting documents

**Attributes:** no.

**Child items:**

+------------+-------------+--------------------------+
| Name       | Mandatory   | Description              |
+============+=============+==========================+
| Document   | yes         | Информация о документе   |
+------------+-------------+--------------------------+

item Order/Account_1C/Document
-------------------------------

Document information.

**Attributes:**

+---------------+---------+-----------+-----------------------------------------------------------------------+
| Name          | Type    | Mandatory | Description                                                           |
+===============+=========+===========+=======================================================================+
| type          | string  | yes       | Type of document (main - invoice, act, report, etc.)                  |
+---------------+---------+-----------+-----------------------------------------------------------------------+
| download      | string  | yes       | Link to download the document                                         |
+---------------+---------+-----------+-----------------------------------------------------------------------+
| date          | Date    | yes       | Date and time of document creation (for example, 2013-01-11 12:23:00) |
+---------------+---------+-----------+-----------------------------------------------------------------------+
| num           | string  | yes       | Document number                                                       |
+---------------+---------+-----------+-----------------------------------------------------------------------+
| currency_date | Date    | yes       | The date on which the rate is recalculated (for example, 1970-01-01)  |
+---------------+---------+-----------+-----------------------------------------------------------------------+
| total_sum     | Numeric | No        | Total sum                                                             |
+---------------+---------+-----------+-----------------------------------------------------------------------+

Order/Paxes item
-------------------

List of paxes in order   

- *Attributes: no.*

Child items:

+------+--------------+--------------------------+
| Item | Mandatory    | Description              |
+======+==============+==========================+
| Pax  | Yes          | Information about person |
+------+--------------+--------------------------+



Order/Paxes/Pax item
-----------------------

Information about person

Attributes:

+------------+----------------+--------------+------------------------+
| Attribute  | Type           | Mandatory    | Description            |
+============+================+==============+========================+
| paxId      | Numeric        | Yes          | person id              |
+------------+----------------+--------------+------------------------+
| child      | true or false  | Yes          | if child, true         |
+------------+----------------+--------------+------------------------+

Child items:

+-----------+-------------------+--------------+------------------------------------------------------------------+
| Item      | Type              | Mandatory    | Description                                                      |
+===========+===================+==============+==================================================================+
| Title     | Mr, Mrs, Ms, Chld | Yes          | Title                                                            |
+-----------+-------------------+--------------+------------------------------------------------------------------+
| FirstName | String            | Yes          | Name                                                             |
+-----------+-------------------+--------------+------------------------------------------------------------------+
| LastName  | String            | Yes          | Last name                                                         |
+-----------+-------------------+--------------+------------------------------------------------------------------+
| FullName  | String            | Yes          | Full name                                                         |
+-----------+-------------------+--------------+------------------------------------------------------------------+

Order/Items/HotelItem item
-----------------------------

Order item - hotel.

Attributes:

+--------------+---------+--------------+-------------------------------+
| Attribute    | Type    | Mandatory    | Description                   |
+==============+=========+==============+===============================+
| itemId       | Numeric | Yes          | order item id                 |
+--------------+---------+--------------+-------------------------------+

Child items:

+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Item              | Type                        | Mandatory    | Description                                                                 |
+===================+=============================+==============+=============================================================================+
| HotelId           | Numeric                     | Yes          | hotel id                                                                    |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| CityId            | Numeric                     | Yes          | city id                                                                     |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Name              | String                      | Yes          | hotel name                                                                  |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| CategoryId        | Numeric                     | Yes          | Category id                                                                 |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| State             | Numeric                     | Yes          | order item state (new, modified, cancelled, etc.)                           |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| CheckIn           | Дата в формате "YYYY-MM-DD" | Yes          | Check in                                                                    |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Duration          | Numeric                     | Yes          | Duration                                                                    |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| TotalPrice        | Numeric                     | Yes          | Total price                                                                 |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| ExtraPrice        | Numeric                     | Yes          | Extra price                                                                 |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Currency          | String                      | Yes          | Currency                                                                    |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| UseNds            | true or false               | No           | VAT included                                                                |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Information       | String                      | No           | Additional information                                                      |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| SpecialOfferText  | String                      | Yes          | Special offer (text)                                                        |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| ProviderId        | Numeric                     | Yes          | Provider id                                                                 |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| ProviderReference | Numeric                     | No           | Provider reference                                                          |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Rooms             | list                        | Yes          | List of rooms                                                               |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| Remarks           | list                        | Yes          | List of remarks                                                             |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| ChargeConditions  | Nested                      | No           | Charge conditions                                                           |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+
| PriceDetails      | Nested                      | No           | Price details                                                               |
+-------------------+-----------------------------+--------------+-----------------------------------------------------------------------------+

Order/Items/HotelItem/Rooms/Room item
----------------------------------------

Rooms description

Attributes:

+-------------------+-----------------------+--------------+------------------------------------------------------------+
| Attributes        | Type                  | Mandatory    | Description                                                |
+===================+=======================+==============+============================================================+
| roomSizeId        | Numeric               | Yes          | Room size id                                               |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| roomSizeName      | String                | Yes          | Room size name                                             |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| roomTypeId        | Numeric               | Yes          | Room type id                                               |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| roomTypeName      | String                | Yes          | Room type name                                             |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| roomViewId        | Numeric               | Yes          | Room view id                                               |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| roomViewName      | String                | Yes          | Room view name                                             |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| roomName          | String                | Yes          | Room name                                                  |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| mealId            | Numeric               | Yes          | Meal type id                                               |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| mealName          | String                | Yes          | Meal name                                                  |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| mealBreakfastId   | Numeric               | Yes          | Breakfast type id                                          |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| mealBreakfastName | String                | Yes          | Breakfast name                                             |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| child             | 0 or 1                | Yes          | Additional place for a child                               |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| cots              | Numeric - from 0 to 2 | Yes          | Number of cots                                             |
+-------------------+-----------------------+--------------+------------------------------------------------------------+
| sharingBedding    | true or false         | Yes          | Separation of bedding                                      |
+-------------------+-----------------------+--------------+------------------------------------------------------------+


Child items:

+--------+--------------+----------------------------------------------------------------------------+
| Item   | Mandatory    | Description                                                                |
+========+==============+============================================================================+
| Paxes  | Yes          | List of paxes in room - list of item PaxId, from Order/Paxes/Pax           |
+--------+--------------+----------------------------------------------------------------------------+

Order/Items/HotelItem/Remarks item
-------------------------------------

List of remarks.

- *Attributes: no.*

Child items:

+---------+--------+--------------+-------------+
| Item    | Type   | Mandatory    | Description |
+=========+========+==============+=============+
| Remark  | String | No           | Remark code |
+---------+--------+--------------+-------------+

Order/Items/HotelItem/ChargeConditions item
----------------------------------------------

Cancellation and amendment charges

- *Attributes: no.*

Child items:

+---------------+--------------+------------------------------+
| Item          | Mandatory    | Description                  |
+===============+==============+==============================+
| Currency      | Yes          | Currency                     |
+---------------+--------------+------------------------------+
| Cancellations | Yes          | Cancellation charges         |
+---------------+--------------+------------------------------+
| Amendments    | No           | Amendment charges            |
+---------------+--------------+------------------------------+

 
 Order/Items/HotelItem/ChargeConditions/Cancellation item
----------------------------------------------------------

Cancellation charges.

**Attributes:**

+-------------+--------------+-----------+------------------------------------+
| Name        | Type         | Mandatory | Description                        |
+=============+==============+===========+====================================+
| charge      | true / false | Yes       | Charge applied(true), or no(false) |
+-------------+--------------+-----------+------------------------------------+
| denyChanges | true / false | Yes       | Deny cancellation                  |
+-------------+--------------+-----------+------------------------------------+
| from        | Date         | No        | Charge from                        |
+-------------+--------------+-----------+------------------------------------+
| to          | Date         | No        | Charge to                          |
+-------------+--------------+-----------+------------------------------------+
| price       | Numeric      | No        | Price (if charge=true)             |
+-------------+--------------+-----------+------------------------------------+
| policy      | String       | No        | Charge policy                      |
+-------------+--------------+-----------+------------------------------------+

 **Child items:** No.

 Order/Items/HotelItem/ChargeConditions/Amendment item
--------------------------------------------------------

Amendment charges.

**Attributes:**

+---------------+----------------+-------------+---------------------------------------+
| Name          | Type           | Mandatory   | Description                           |
+===============+================+=============+=======================================+
| charge        | true / false   | Yes         | Charge appllied(true), or no(false)   |
+---------------+----------------+-------------+---------------------------------------+
| denyChanges   | true / false   | Yes         | Deny amendment                        |
+---------------+----------------+-------------+---------------------------------------+
| from          | Date           | No          | Charge from                           |
+---------------+----------------+-------------+---------------------------------------+
| to            | Date           | No          | Charge to                             |
+---------------+----------------+-------------+---------------------------------------+
| price         | Numeric        | No          | Price (if charge=true)                |
+---------------+----------------+-------------+---------------------------------------+
| policy        | String         | No          | Charge policy                         |
+---------------+----------------+-------------+---------------------------------------+

 **Child items:** No.


Order/Items/HotelItem/PriceDetails item
----------------------------------------

Price breakdown by rooms.

**Attributes:** No.

**Child items:**

+------------+---------------+-----------+--------------------------+
| Name       | Type          | Mandatory | Description              |
+============+===============+===========+==========================+
| Currency   | String        | Yes       | Currency                 |
+------------+---------------+-----------+--------------------------+
| Discount   | Numeric       | No        | Discount from provider   |
+------------+---------------+-----------+--------------------------+
| Offer      | String        | No        | Special offer text       |
+------------+---------------+-----------+--------------------------+
| RoomPrices | List of rooms | Yes       | Price breakdown by rooms |
+------------+---------------+-----------+--------------------------+

Order/Items/HotelItem/PriceDetails/Room item
-----------------------------------------------

Price breakdown by days.

**Attributes:**

+------------+---------------------+-----------+-----------------------------------+
| Name       | Type                | Mandatory | Description                       |
+============+=====================+===========+===================================+
| roomNumber | Numeric             | Yes       | Number of rooms (>=1)             |
+------------+---------------------+-----------+-----------------------------------+
| roomSizeId | Numeric             | Yes       | id room size                      |
+------------+---------------------+-----------+-----------------------------------+
| roomTypeId | Numeric             | Yes       | id room type                      |
+------------+---------------------+-----------+-----------------------------------+
| roomViewId | Numeric             | Yes       | id room view                      |
+------------+---------------------+-----------+-----------------------------------+
| child      | 0 / 1               | Yes       | Additional place for child        |
+------------+---------------------+-----------+-----------------------------------+
| cots       | Numeric from 1 to 2 | No        | Number of cots                    |
+------------+---------------------+-----------+-----------------------------------+

**Child items:**

+---------+-------------+---------------+
| Name    | Mandatory   | Description   |
+=========+=============+===============+
| Price   | Yes         | Prices        |
+---------+-------------+---------------+

Order/Items/HotelItem/PriceDetails/Room/Price item
-----------------------------------------------------

Price

**Attributes:**

+------------+----------------------------+-----------+--------------------+
| Name       | Type                       | Mandatory | Description        |
+============+============================+===========+====================+
| date       | Date, pattern "YYYY-MM-DD" | Yes       | Date               |
+------------+----------------------------+-----------+--------------------+
| available  | true / false               | Yes       | Price availability |
+------------+----------------------------+-----------+--------------------+
| price      | Numeric                    | Yes       | Price              |
+------------+----------------------------+-----------+--------------------+
| priceChild | Numeric                    | No        | Price for child    |
+------------+----------------------------+-----------+--------------------+
| priceCot   | Numeric                    | No        | Price for cot      |
+------------+----------------------------+-----------+--------------------+

**Child items:** No.


Order/ContactInfo item
----------------------

Contact information.

**Attributes:** No.

**Child items:**

+-----------+--------------------------+-------------+----------------------+
| Name      | Type                     | Mandatory   | Description          |
+===========+==========================+=============+======================+
| Name      | String (max 100 chars)   | Yes         | Full name            |
+-----------+--------------------------+-------------+----------------------+
| Email     | String (max 100 chars)   | Yes         | Email                |
+-----------+--------------------------+-------------+----------------------+
| Phone     | String (max 15 chars)    | Yes         | Phone                |
+-----------+--------------------------+-------------+----------------------+
| Comment   | String                   | Yes         | Comment (optional)   |
+-----------+--------------------------+-------------+----------------------+


Response, ConfirmOrderResponse
------------------------------

Response pattern is the same as in response to a request for information
about order (``OrderInfoResponse``).

And now you only need to check item status from response.