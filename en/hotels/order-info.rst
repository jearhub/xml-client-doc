Order information
#################

Description of XML schema
=========================

A request is formed through URL (using GET method).

XSD-schema response:

-  ``www/xsd/OrderInfoResponse.xsd``

Request
-------

The request must be an parameter - order\_id, taken from the response to
the AddOrder request. Request is passed via the URL with
credentials(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/order_info``

Response, OrderInfoResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>

            <OrderInfoResponse>
             [<Errors>
                <Error code="..." description="..."> - list of errors
              </Errors>]
              <Order>

                <Id>...</Id> - order id
                <Tag>...</Tag> - order reference
            [<AccountComment>...</AccountComment>] - Comment for the account (Mandatory item if XML-client has right "View account comment")
                <State>...</State> - order status
                <CreationDate>...</CreationDate> - date and time of order creation
                <PayForm>...</PayForm> - order pay form
                [<Account_1C> - Information about the account 1C
                    <Document type="..." download="..." date="..." num="..." currency_date="..." total_sum="..."> - information about the document
                </Account_1C>]
                <Paxes>

                  <Pax paxId="..." child="true|false"> - pax data
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
                    <CategoryId>...</CategoryId> - hotel category name
                    <State>...</State> - status
                    <CheckIn>...</CheckIn> - check in date
                    <Duration>...</Duration> - duration
                    <TotalPrice>...</TotalPrice>
                    <ExtraPrice  currency="..." >...</ExtraPrice>
            [<Fee>...</Fee>]
                    <Currency>...</Currency>
                    <HotelPaid>true|false</HotelPaid>
                    [<UseNds>true|false</UseNds>] - VAT
                    <SpecialOfferText>...</SpecialOfferText>
                    <ProviderId>...</ProviderId> - provider id
                    <ProviderReference>...</ProviderReference> - provider reference
                    <PermittedOperations> - list of permitted operations for order item
                        <Edit>true|false</Edit> - can be edited or not
                        <Cancel>true|false</Cancel> - can be cancellated or not
                        <IsBlocked>true|false</IsBlocked> - is blocked or not
                    </PermittedOperations>
                    <EditableOptions> - list of hotel editable options
                       <Option
                               name="..." - option name
                               editable="true|false" - editable or not
                       />
                    </EditableOptions>
                    <RoomLocks> - list of hotel rooms, which locked for modification
                       <Room
                               roomId="..." - room id
                               lock="true|false" - locked or not
                       />
                    </RoomLocks>
                    <Rooms>

                      <Room
                         roomId=".."
                         roomSizeId=".." roomTypeId=".." roomViewId=".."
                         roomName="..."
                         mealId="..." mealName="..."

                         mealBreakfastId="..." mealBreakfastName="..."
                         child="0|1" cots="0|1|2" sharingBedding="true|false"

                         >
                         <Paxes> - list of paxes
                           <PaxId>...</PaxId>
                         </Paxes>
                      </Room>

                    </Rooms>

                    <Remarks> - list of remarks
                      [<Remark>...</Remark>]
                    </Remarks>
                    <ChargeConditions>

                      <Currency>..</Currency> - currency
                      <Cancellations> - cancellation charges
                        <Cancellation 

                          charge="true|false" 

                          [from="2008-02-28T11:50:00"] - charge from date
                          [to="2008-02-28T11:50:00"] - to date

                          [price="100.00"] - price in foreign cyrrency (if charge=true)
                          [policy="1 night"] - charge policy

                        />
                      </Cancellations>
                      <Amendments> - amendment charges
                        <Amendment 
                          charge="true|false"

                          [from="YYYY-MM-DDThh:ii:ss"]
                          [to="YYYY-MM-DDThh:ii:ss"]
                          [price=".."]

                          [policy=".."]

                        />
                      </Amendments>
                    </ChargeConditions>

                    <PriceDetails> - price breakdown
                      <Currency>..</Currency> - currency
                     [<Discount>..</Discount>] - discount from provider
                     [<Offer>..</Offer>] - special offer text from provider
                      <RoomPrices>

                        <Room - 
                          roomNumber=".." - number of rooms
                          roomName="..."

                          child="0|1" - number of children

                         [cots="1|2"] - number of cots (optional)

                          >
                          <Price 

                            date="YYYY-MM-DD"

                            available="true|false" - price available

                            price=".." - price

                           [priceChild=".."] - price for child

                           [priceCot=".."] - price for cots

                          />
                        </Room>

                      </RoomPrices>
                    </PriceDetails>

                  </HotelItem>

                </Items>
                <ContactInfo> -  contact information
                  <Name>...</Name>

                  <Email>...</Email>

                  <Phone>...</Phone>
                  <Comment>...</Comment>
                </ContactInfo>

              </Order>
            </OrderInfoResponse>

OrderInfoResponse item
----------------------

Information about order

Parent item.

**Attributes:** No.

**Child items:**

+----------+-------------+---------------------+
| Name     | Mandatory   | Description         |
+==========+=============+=====================+
| Errors   | No          | List of errors      |
+----------+-------------+---------------------+
| Order    | No          | Order information   |
+----------+-------------+---------------------+

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

Order item
----------

Order description.

**Attributes:** No.

**Child items:**

+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Name           | Type                   | Mandatory | Description                                                                                                                                       |
+================+========================+===========+===================================================================================================================================================+
| Id             | Numeric                | Yes       | Order id                                                                                                                                          |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Tag            | String                 | Yes       | Order reference                                                                                                                                   |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| AccountComment | String                 | No        | Comment for the account (Mandatory item if XML-client has right "View account comment")                                                           |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| State          | String                 | Yes       | Order status (new, modified, cancelled, etc.)                                                                                                     |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| CreationDate   | YYYY-MM-DD HH:MM:SS    | Yes       | Date and time of order creation (for example, 2013-01-11 12:23:00)                                                                                |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| PayForm        | String                 | Yes       | Order pay form (cash, cashless, undefined). If order elements have different pay form (it's possible for old orders), order pay form is undefined |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Account_1C    | List of Document items | No        | Account information 1C                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Paxes          | List                   | Yes       | List of paxes in order                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Items          | List                   | Yes       | List of items (hotels)                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| ContactInfo    | Nested                 | Yes       | Contact information about customer                                                                                                                |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+

Order/Account_1C item
----------------------

List of accounting documents

**Attributes:** no.

**Child items:**

+----------+-----------+----------------------+
| Name     | Mandatory | Description          |
+==========+===========+======================+
| Document | Yes       | Document information |
+----------+-----------+----------------------+

Order/Account_1C/Document item
-------------------------------

Document information.

**Attributes:**

+----------------+---------+-----------+-----------------------------------------------------------------------+
| Name           | Type    | Mandatory | Description                                                           |
+================+=========+===========+=======================================================================+
| type           | String  | Yes       | Type of document (main - invoice, act, report, etc.)                  |
+----------------+---------+-----------+-----------------------------------------------------------------------+
| download       | String  | Yes       | Link to download the document                                         |
+----------------+---------+-----------+-----------------------------------------------------------------------+
| date           | Date    | Yes       | Date and time of document creation (for example, 2013-01-11 12:23:00) |
+----------------+---------+-----------+-----------------------------------------------------------------------+
| num            | String  | Yes       | Document number                                                       |
+----------------+---------+-----------+-----------------------------------------------------------------------+
| currency_date | Date    | Yes       | The date on which the rate is recalculated (for example, 1970-01-01)  |
+----------------+---------+-----------+-----------------------------------------------------------------------+
| total_sum     | Numeric | No        | Total sum                                                             |
+----------------+---------+-----------+-----------------------------------------------------------------------+

Order/Paxes item
----------------

List of paxes

**Attributes:** No.

**Child items:**

+--------+-------------+----------------------------+
| Name   | Mandatory   | Description                |
+========+=============+============================+
| Pax    | Yes         | Information about person   |
+--------+-------------+----------------------------+

Order/Paxes/Pax item
--------------------

Information about person.

**Attributes:**

+-------+--------------+-----------+----------------+
| Name  | Type         | Mandatory | Description    |
+=======+==============+===========+================+
| paxId | Numeric      | Yes       | pax id         |
+-------+--------------+-----------+----------------+
| child | true / false | Yes       | if child, true |
+-------+--------------+-----------+----------------+

**Child items:**

+-----------+-------------------+-----------+-------------+
| Name      | Type              | Mandatory | Description |
+===========+===================+===========+=============+
| Title     | Mr, Mrs, Ms, Chld | Yes       | Title       |
+-----------+-------------------+-----------+-------------+
| FirstName | String            | Yes       | Name        |
+-----------+-------------------+-----------+-------------+
| LastName  | String            | Yes       | Last name   |
+-----------+-------------------+-----------+-------------+

.. note:: **Attantion:** *``FullName`` item now is optional and will be remove from 01.01.2013*

Order/Items/HotelItem item
--------------------------

List of order items.

**Attributes:**

+----------+-----------+-------------+-------------------------+
| Name     | Type      | Mandatory   | Description             |
+==========+===========+=============+=========================+
| itemId   | Numeric   | Yes         | Order item identifier   |
+----------+-----------+-------------+-------------------------+

**Child items:**

+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Name              | Type                       | Mandatory | Description                                         |
+===================+============================+===========+=====================================================+
| HotelId           | Numeric                    | Yes       | hotel id                                            |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| CityId            | Numeric                    | Yes       | city id                                             |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Name              | String                     | Yes       | Hotel name                                          |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| CategoryId        | Numeric                    | Yes       | Hotel category id                                   |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| State             | Numeric                    | Yes       | Status (new, processed, confirmed, cancelled, etc.) |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| CheckIn           | Date, pattern "YYYY-MM-DD" | Yes       | Check in date                                       |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Duration          | Numeric                    | Yes       | Duration (nights)                                   |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| TotalPrice        | Numeric                    | Yes       | Price                                               |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| ExtraPrice        | Numeric                    | Yes       | Provider additional margin                          |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Fee               | Numeric                    | Yes       | Fee price (if exists)                               |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Currency          | String                     | Yes       | Currency                                            |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| HotelPaid         | true / false               | Yes       | Paid                                                |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| UseNds            | true / false               | No        | VAT included                                        |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| SpecialOfferText  | String                     | Yes       | Special offer text                                  |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| SpecialOffers     | List of special offers     | Yes       | List of hotel's special offers                      |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| ProviderId        | Numeric                    | Yes       | provider id                                         |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| ProviderReference | String                     | Yes       | provider reference                                  |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| EditableOptions   | List of options            | Yes       | List of editable hotel options                      |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| RoomLocks         | List of rooms              | Yes       | List of hotel rooms, locked for modification        |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Rooms             | List of rooms              | Yes       | List of rooms                                       |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| Remarks           | List of remarks            | Yes       | List of remarks                                     |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| ChargeConditions  | Nested                     | No        | Charge conditions                                   |
+-------------------+----------------------------+-----------+-----------------------------------------------------+
| PriceDetails      | Nested                     | No        | Price breakdown                                     |
+-------------------+----------------------------+-----------+-----------------------------------------------------+

Order/Items/HotelItem/ExtraPrice item
-------------------------------------

Provider additional margin

**Attributes:**

+----------+------------------------------+-----------+--------------------------------------+
| Name     | Type                         | Mandatory | Description                          |
+==========+==============================+===========+======================================+
| currency | string (EUR, or USD, or ...) | Yes       | Custom sign the arrival, early check |
+----------+------------------------------+-----------+--------------------------------------+

 **Child items:** No.

Order/Items/HotelItem/CheckInTime item
--------------------------------------

Arrival time in hotel room

**Attributes:**

+---------+---------------+-----------+--------------------------------------+
| Name    | Type          | Mandatory | Description                          |
+=========+===============+===========+======================================+
| info    | true or false | Yes       | Custom sign the arrival, early check |
+---------+---------------+-----------+--------------------------------------+
| default | Time HH:MM    | Yes       | The default time for the hotel       |
+---------+---------------+-----------+--------------------------------------+
| value   | Time HH:MM    | Yes       | The time specified in the order      |
+---------+---------------+-----------+--------------------------------------+

**Child items:** No.

Order/Items/HotelItem/CheckOutTime item
---------------------------------------

Time out of the hotel rooms

**Attributes:**

+---------+---------------+-----------+--------------------------------------------+
| Name    | Type          | Mandatory | Description                                |
+=========+===============+===========+============================================+
| info    | true or false | Yes       | Sign custom departure time, late check-out |
+---------+---------------+-----------+--------------------------------------------+
| default | Time HH:MM    | Yes       | The default time for the hotel             |
+---------+---------------+-----------+--------------------------------------------+
| value   | Time HH:MM    | Yes       | The time specified in the order            |
+---------+---------------+-----------+--------------------------------------------+

**Child items:** No.

Order/Items/HotelItem/SpecialOffers/SpecialOffer
------------------------------------------------

Hotel special offer

**Атрибуты:**

+----------+--------+-----------+--------------------------------+
| Name     | Type   | Mandatory | Description                    |
+==========+========+===========+================================+
| text     | String | Yes       | Special offer's title          |
+----------+--------+-----------+--------------------------------+
| key      | String | Yes       |                                |
+----------+--------+-----------+--------------------------------+
| id       | Number | Yes       | Special offers's ID            |
+----------+--------+-----------+--------------------------------+
| from     | String | Yes       | Date from special offer starts |
+----------+--------+-----------+--------------------------------+
| till     | String | Yes       | Date when special offer ends   |
+----------+--------+-----------+--------------------------------+
| stay     | String | Yes       | Number of nights to stay       |
+----------+--------+-----------+--------------------------------+
| pay      | String | Yes       | Number of nights to pay        |
+----------+--------+-----------+--------------------------------+
| nights   | String | Yes       | Discount in nights             |
+----------+--------+-----------+--------------------------------+
| percent  | String | Yes       | Discount in percent            |
+----------+--------+-----------+--------------------------------+
| discount | String | Yes       | Discount value                 |
+----------+--------+-----------+--------------------------------+

Order/Items/HotelItem/PermittedOperations
-----------------------------------------

Permitted operations for this order item

**Attributes:** no

**Child tags:**

+-----------+-------+-----------+-------------+-----------------------------------------------------------------------------------------------------------------+
| Name      | Type  | Mandatory | Description |                                                                                                                 |
+===========+=======+===========+=============+=================================================================================================================+
| Edit      | true\ | false     | Yes         | Modification of this order item is permitted                                                                    |
+-----------+-------+-----------+-------------+-----------------------------------------------------------------------------------------------------------------+
| Cancel    | true\ | false     | Yes         | Cancellation of this order item is permitted                                                                    |
+-----------+-------+-----------+-------------+-----------------------------------------------------------------------------------------------------------------+
| IsBlocked | true\ | false     | Yes         | This order item is blocked or not. If yes, it cann't be cancellated or sent to provider.                        |
|           |       |           |             | Blocking often happened when errors received from provider during booking of new item or sending modified item. |
|           |       |           |             | For getting know, what error is happened, you need to get order log on booking/sending date                     |
|           |       |           |             | (request /xml/order_list, parameters ChangedFrom and ChangedTo)                                                 |
+-----------+-------+-----------+-------------+-----------------------------------------------------------------------------------------------------------------+

Order/Items/HotelItem/EditableOptions/Option
--------------------------------------------

Is this hotel option editable or not

**Attributes:**

+------------+-----------------+-------------+-------------------+
| Name       | Type            | Mandatory   | Description       |
+============+=================+=============+===================+
| name       | String          | Yes         | Option name       |
+------------+-----------------+-------------+-------------------+
| editable   | true or false   | Yes         | Editable or not   |
+------------+-----------------+-------------+-------------------+

Order/Items/HotelItem/RoomLocks/Room
------------------------------------

Is hotel room locked for modification or not

**Attributes:**

+----------+-----------------+-------------+-----------------+
| Name     | Type            | Mandatory   | Description     |
+==========+=================+=============+=================+
| roomId   | Numeric         | Yes         | Room id         |
+----------+-----------------+-------------+-----------------+
| lock     | true or false   | Yes         | Locked or not   |
+----------+-----------------+-------------+-----------------+

Order/Items/HotelItem/Rooms/Room item
-------------------------------------

Rooms description.

**Attributes:**

+---------------------+-------------------------+-------------+------------------------------------------+
| Name                | Type                    | Mandatory   | Description                              |
+=====================+=========================+=============+==========================================+
| roomId              | Numeric                 | Yes         | Room id (need for request ModifyOrder)   |
+---------------------+-------------------------+-------------+------------------------------------------+
| roomSizeId          | Numeric                 | Yes         | Room size id                             |
+---------------------+-------------------------+-------------+------------------------------------------+
| roomTypeId          | Numeric                 | Yes         | Room type id                             |
+---------------------+-------------------------+-------------+------------------------------------------+
| roomViewId          | Numeric                 | Yes         | Room view id                             |
+---------------------+-------------------------+-------------+------------------------------------------+
| roomName            | String                  | Yes         | Room name (room size, type, view)        |
+---------------------+-------------------------+-------------+------------------------------------------+
| mealId              | Numeric                 | Yes         | Meal type id                             |
+---------------------+-------------------------+-------------+------------------------------------------+
| mealName            | String                  | Yes         | Meal name                                |
+---------------------+-------------------------+-------------+------------------------------------------+
| mealBreakfastId     | Numeric                 | Yes         | Breakfast type id                        |
+---------------------+-------------------------+-------------+------------------------------------------+
| mealBreakfastName   | String                  | Yes         | Breakfast name                           |
+---------------------+-------------------------+-------------+------------------------------------------+
| child               | 0 / 1                   | Yes         | Additional place for a child             |
+---------------------+-------------------------+-------------+------------------------------------------+
| cots                | Numeric - from 0 to 2   | Yes         | Number of cots                           |
+---------------------+-------------------------+-------------+------------------------------------------+
| sharingBedding      | true / false            | Yes         | Separation of bedding                    |
+---------------------+-------------------------+-------------+------------------------------------------+

**Child items:**

+---------+-------------+--------------------------------------------------------------------+
| Name    | Mandatory   | Description                                                        |
+=========+=============+====================================================================+
| Paxes   | Yes         | List of paxes in room - list of item PaxId, from Order/Paxes/Pax   |
+---------+-------------+--------------------------------------------------------------------+

Order/Items/HotelItem/Remarks item
----------------------------------

List of order remarks.

**Attributes:** No.

**Child items:**

+----------+----------+-------------+---------------+
| Name     | Type     | Mandatory   | Description   |
+==========+==========+=============+===============+
| Remark   | String   | No          | Remark code   |
+----------+----------+-------------+---------------+

Order/Items/HotelItem/ChargeConditions item
-------------------------------------------

Cancellation and amendment charges

**Attributes:** No.

**Child items:**

+-----------------+-------------+------------------------+
| Name            | Mandatory   | Description            |
+=================+=============+========================+
| Currency        | Yes         | Currency               |
+-----------------+-------------+------------------------+
| Cancellations   | Yes         | Cancellation charges   |
+-----------------+-------------+------------------------+
| Amendments      | No          | Amendment charges      |
+-----------------+-------------+------------------------+

Order/Items/HotelItem/ChargeConditions/DenyNameChanges item
-----------------------------------------------------------

Ability to change the names of clients

**Attributes:**

+------+---------------+-----------+---------------------------------+
| Name | Type          | Mandatory | Description                     |
+======+===============+===========+=================================+
| deny | true or false | Yes       | Deny (true), Allow (false)      |
+------+---------------+-----------+---------------------------------+
| from | Date          | No        | Date and time begin of the deny |
+------+---------------+-----------+---------------------------------+
| to   | Date          | No        | Date and time end of the deny   |
+------+---------------+-----------+---------------------------------+

**Child items:** No.

Order/Items/HotelItem/ChargeConditions/Cancellation item
--------------------------------------------------------

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
| charge      | true / false | Yes       | Charge applied(true), or no(false) |
+-------------+--------------+-----------+------------------------------------+

 **Child items:** No.

Order/Items/HotelItem/ChargeConditions/Amendment item
-----------------------------------------------------

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
| charge        | true / false   | Yes         | Charge applied(true), or no(false)    |
+---------------+----------------+-------------+---------------------------------------+

**Child items:** No.

Order/Items/HotelItem/PriceDetails item
---------------------------------------

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

Order/Items/HotelItem/PriceDetails/RoomPrices/Room item
-------------------------------------------------------

Price breakdown by days.

**Attributes:**

+------------+---------------------+-----------+-----------------------------------+
| Name       | Type                | Mandatory | Description                       |
+============+=====================+===========+===================================+
| roomNumber | Numeric             | Yes       | Number of rooms (>=1)             |
+------------+---------------------+-----------+-----------------------------------+
| roomName   | String              | Yes       | Room name (room size, type, view) |
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

Order/Items/HotelItem/PriceDetails/RoomPrices/Room/Price item
-------------------------------------------------------------

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