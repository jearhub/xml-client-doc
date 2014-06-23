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

                  <TransferItem itemId="40036"> - order item (transfer)

            <ProviderId>...</ProviderId>
            <ProviderReference>...</ProviderReference>
            <State>...</State>
            <Date>...</Date>
            <Passengers>...</Passengers>
            <Description>...</Description>
            <Vehicle>
                <Name>...</Name>
                <Description>...</Description>
            </Vehicle>
            <Language id="..">...</Language>
            <TransferTime>...</TransferTime>
            <CheckInTime>...</CheckInTime>

            <ModifyRestrictions>
                <FixFrom>true|false</FixFrom> - deny of pick up edition
                <FixTo>true|false</FixTo> - deny of drop off edition
            </ModifyRestrictions>

            <PaxId>...</PaxId> - клиент трансфера

            <TotalPrice>...</TotalPrice>
            [<Fee>...</Fee>]
            <Currency>...</Currency>
            [<UseNds>true|false</UseNds>] - VAT

            <Information>...</Information>

            <PickUp>
               <Airport id="..">...</Airport>
               <FlightNum>...</FlightNum>
               <ArrivalAirport id="..">...</ArrivalAirport>
               <Time>...</Time>

               or

               <Station id="..">...</Station>
               <TrainNum>...</TrainNum>
               <ArrivalCity id="..">...</ArrivalCity>
               <Time>...</Time>

               or

               <Hotel id="..">...</Hotel>
               <Time>...</Time>

               or

               <Address> - транспорт
                   <AddressLine>...</AddressLine>
                   [<AddressLine>...</AddressLine>]
               </Address>
               <ZipCode>...</ZipCode>
               <District>...</District>
               <Phone>...</Phone>
               <Time>...</Time>

               or

               <ShipName>...</ShipName>
               <ShipCompanyName>...</ShipCompanyName>
               <ArrivalCity>...</ArrivalCity>
               <Time>...</Time>

            </PickUp>

            <DropOff>
               <Airport id="..">...</Airport>
               <FlightNum>...</FlightNum>
               <DepartureAirport id="..">...</DepartureAirport>
               <Time>...</Time>

               or

               <Station id="..">...</Station>
               <TrainNum>...</TrainNum>
               <DepartureCity id="..">...</DepartureCity>
               <Time>...</Time>

               or

               <Hotel id="..">...</Hotel>
               <Time>...</Time>

               or

               <Address> - транспорт
                   <AddressLine>...</AddressLine>
                   [<AddressLine>...</AddressLine>]
               </Address>
               <ZipCode>...</ZipCode>
               <District>...</District>
               <Phone>...</Phone>
               <Time>...</Time>

               or

               <ShipName>...</ShipName>
               <ShipCompanyName>...</ShipCompanyName>
               <DepartureCity>...</DepartureCity>
               <Time>...</Time>

            </DropOff>
        
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

                  </TransferItem>

                </Items>
                <ContactInfo> -  contact information
                  <Name>...</Name>

                  <Email>...</Email>

                  <Phone>...</Phone>
                  <Time>...</Time>
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

**Attributes:** No.

**Child items:**

+-------+-----------+----------------------------------------+
| Name  | Mandatory | Description                            |
+=======+===========+========================================+
| Error | Yes       | Error description.                     |
|       |           |                                        |
|       |           | Attributes:                            |
|       |           |                                        |
|       |           | -  ``code`` - error code               |
|       |           | -  ``description`` - error description |
+-------+-----------+----------------------------------------+

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
| Account_1C     | List of Document items | No        | Account information 1C                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Paxes          | List                   | Yes       | List of paxes in order                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Items          | List                   | Yes       | List of items (transfer)                                                                                                                          |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| ContactInfo    | Nested                 | Yes       | Contact information about customer                                                                                                                |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+

Order/Account_1C item
---------------------

List of accounting documents

**Attributes:** no.

**Child items:**

+----------+-----------+----------------------+
| Name     | Mandatory | Description          |
+==========+===========+======================+
| Document | Yes       | Document information |
+----------+-----------+----------------------+

Order/Account\_1C/Document item
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
| currency\_date | Date    | Yes       | The date on which the rate is recalculated (for example, 1970-01-01)  |
+----------------+---------+-----------+-----------------------------------------------------------------------+
| total\_sum     | Numeric | No        | Total sum                                                             |
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

+---------+----------------+-------------+------------------+
| Name    | Type           | Mandatory   | Description      |
+=========+================+=============+==================+
| paxId   | Numeric        | Yes         | pax id           |
+---------+----------------+-------------+------------------+
| child   | true / false   | Yes         | if child, true   |
+---------+----------------+-------------+------------------+

**Child items:**

+-------------+---------------------+-------------+---------------+
| Name        | Type                | Mandatory   | Description   |
+=============+=====================+=============+===============+
| Title       | Mr, Mrs, Ms, Chld   | Yes         | Title         |
+-------------+---------------------+-------------+---------------+
| FirstName   | String              | Yes         | Name          |
+-------------+---------------------+-------------+---------------+
| LastName    | String              | Yes         | Last name     |
+-------------+---------------------+-------------+---------------+

.. note:: **Attantion:** *``FullName`` item now is optional and will be remove from 01.01.2013*

Order/Items/TransferItem item
-----------------------------

List of order items.

**Attributes:**

+----------+-----------+-------------+-------------------------+
| Name     | Type      | Mandatory   | Description             |
+==========+===========+=============+=========================+
| itemId   | Numeric   | Yes         | Order item identifier   |
+----------+-----------+-------------+-------------------------+

**Child items:**

+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Name               | Type                        | Mandatory | Description                                           |
+====================+=============================+===========+=======================================================+
| ProviderId         | Number                      | Yes       | Id of transfer provider                               |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| ProviderReference  | String                      | Yes       | Reference of transfer provider                        |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| State              | Number                      | Yes       | Item state (new, processed, commited, cancelled etc.) |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Date               | Date in format "YYYY-MM-DD" | Yes       | Transfer date                                         |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Passengers         | Number                      | Yes       | Number of passengers                                  |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Description        | String                      | Yes       | Transfer description                                  |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Vehicle            | Nested                      | Yes       | Transfer vehicle                                      |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Language           | String                      | Yes       | Transfer language                                     |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| TransferTime       | String                      | Yes       | Transfer time                                         |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| CheckInTime        | String                      | Yes       | Check in time                                         |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| ModifyRestrictions | Nested                      | Yes       | Restrictions on transfer modification                 |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| PaxId              | number                      | Yes       | Transfer pax                                          |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| TotalPrice         | Number                      | Yes       | Transfer price                                        |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Fee                | Number                      | Yes       | Fee price (if exists)                                 |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Currency           | string                      | Yes       | Transfer currency                                     |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| UseNds             | true or false               | No        | If VAT is included                                    |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| Information        | string                      | Yes       | Additional info                                       |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| PickUp             | Nested                      | Yes       | Pick up parameters                                    |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| DropOff            | Nested                      | Yes       | Drop off parameters                                   |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+
| ChargeConditions   | Nested                      | No        | List of charge conditions                             |
+--------------------+-----------------------------+-----------+-------------------------------------------------------+

Order/Items/TransferItem/Vehicle item
-------------------------------------

Transfer vehicle

**Attributes:**

+--------+----------+-------------+---------------+
| Name   | Type     | Mandatory   | Description   |
+========+==========+=============+===============+
| id     | number   | yes         | vehicle id    |
+--------+----------+-------------+---------------+

**Child items:**

+---------------+----------+-------------+-----------------------+
| Name          | Type     | Mandatory   | Description           |
+===============+==========+=============+=======================+
| Name          | string   | yes         | Vehicle name          |
+---------------+----------+-------------+-----------------------+
| Description   | string   | yes         | Vehicle description   |
+---------------+----------+-------------+-----------------------+

Order/Items/TransferItem/ModifyRestrictions item
------------------------------------------------

Restriction of modification

**Attributes:**no.

**Child items:**

+-----------+---------------+-------------+--------------------------------------------------------------+
| Name      | Type          | Mandatory   | Description                                                  |
+===========+===============+=============+==============================================================+
| FixFrom   | true or false   | yes         | Deny of pick up edition (id of airport, station or hotel)    |
+-----------+---------------+-------------+--------------------------------------------------------------+
| FixTo     | true or false   | yes         | Deny of drop off edition (id of airport, station or hotel)   |
+-----------+---------------+-------------+--------------------------------------------------------------+

Order/Items/TransferItem/PickUp item
------------------------------------

Pick up parameters

**Attributes:**no.

**Child items(transfer location - *airport*):**

+----------------+--------+-----------+--------------------------------------------------------+
| Name           | Type   | Mandatory | Description                                            |
+================+========+===========+========================================================+
| Airport        | string | yes       | Airport name (attribute ``id`` - airport id)           |
+----------------+--------+-----------+--------------------------------------------------------+
| FlightNum      | string | yes       | flight number                                          |
+----------------+--------+-----------+--------------------------------------------------------+
| ArrivalAirport | string | yes       | Departure airport name (attribute ``id`` - airport id) |
+----------------+--------+-----------+--------------------------------------------------------+
| Time           | HH:MM  | yes       | Arrival time                                           |
+----------------+--------+-----------+--------------------------------------------------------+

**Child item (transfer location - *station*):**

+-------------+--------+-----------+--------------------------------------------------+
| Name        | Type   | Mandatory | Description                                      |
+=============+========+===========+==================================================+
| Station     | string | yes       | Station name (attribute ``id`` - station id)     |
+-------------+--------+-----------+--------------------------------------------------+
| TrainNum    | string | yes       | Train number                                     |
+-------------+--------+-----------+--------------------------------------------------+
| ArrivalCity | string | yes       | Departure city name (attribute ``id`` - city id) |
+-------------+--------+-----------+--------------------------------------------------+
| Time        | HH:MM  | yes       | Arrival time                                     |
+-------------+--------+-----------+--------------------------------------------------+

**Child item (transfer location - *hotel*):**

+-------+--------+-----------+------------------------------------------+
| Name  | Type   | Mandatory | Description                              |
+=======+========+===========+==========================================+
| Hotel | string | yes       | Hotel name (attribute ``id`` - hotel id) |
+-------+--------+-----------+------------------------------------------+
| Time  | HH:MM  | yes       | Arrival time                             |
+-------+--------+-----------+------------------------------------------+

**Child items (transfer location - *address*):**

+----------+---------------------------------------+-----------+----------------------------------------------------------+
| Name     | Type                                  | Mandatory | Description                                              |
+==========+=======================================+===========+==========================================================+
| Address  | Nested items AddressLine (one or two) | yes       | Address (one or two strings not more than 40 characters) |
+----------+---------------------------------------+-----------+----------------------------------------------------------+
| ZipCode  | string                                | yes       | Zip code (not more than 10 characters)                   |
+----------+---------------------------------------+-----------+----------------------------------------------------------+
| District | string                                | yes       | District name (not more than 20 characters)              |
+----------+---------------------------------------+-----------+----------------------------------------------------------+
| Phone    | string                                | yes       | Phone number                                             |
+----------+---------------------------------------+-----------+----------------------------------------------------------+
| Time     | HH:SS                                 | yes       | Arrival time                                             |
+----------+---------------------------------------+-----------+----------------------------------------------------------+

**Child items (transfer location- *port*):**

+-------------------+----------+-------------+----------------------------+
| Name              | Type     | Mandatory   | Description                |
+===================+==========+=============+============================+
| ShipName          | String   | yes         | Name of the ship           |
+-------------------+----------+-------------+----------------------------+
| ShipCompanyName   | string   | yes         | Name of the ship company   |
+-------------------+----------+-------------+----------------------------+
| ArrivalCity       | string   | yes         | Departure city name        |
+-------------------+----------+-------------+----------------------------+
| Time              | HH:MM    | yes         | Arrival time               |
+-------------------+----------+-------------+----------------------------+

Order/Items/TransferItem/DropOff item
-------------------------------------

Drop off parameters

**Attributes:**no.

**Child items(transfer location - *airport*):**

+--------------------+----------+-------------+--------------------------------------------------------+
| Name               | Type     | Mandatory   | Description                                            |
+====================+==========+=============+========================================================+
| Airport            | string   | yes         | Airport name (attribute ``id`` - airport id)           |
+--------------------+----------+-------------+--------------------------------------------------------+
| FlightNum          | string   | yes         | flight number                                          |
+--------------------+----------+-------------+--------------------------------------------------------+
| DepartureAirport   | string   | yes         | Arrival airport name (attribute ``id`` - airport id)   |
+--------------------+----------+-------------+--------------------------------------------------------+
| Time               | HH:MM    | yes         | Departure time                                         |
+--------------------+----------+-------------+--------------------------------------------------------+

**Child item (transfer location - *station*):**

+-----------------+----------+-------------+--------------------------------------------------+
| Name            | Type     | Mandatory   | Description                                      |
+=================+==========+=============+==================================================+
| Station         | string   | yes         | Station name (attribute ``id`` - station id)     |
+-----------------+----------+-------------+--------------------------------------------------+
| TrainNum        | string   | yes         | Train number                                     |
+-----------------+----------+-------------+--------------------------------------------------+
| DepartureCity   | string   | yes         | Arrival city name (attribute ``id`` - city id)   |
+-----------------+----------+-------------+--------------------------------------------------+
| Time            | HH:MM    | yes         | Departure time                                   |
+-----------------+----------+-------------+--------------------------------------------------+

**Child item (transfer location - *hotel*):**

+---------+----------+-------------+--------------------------------------------+
| Name    | Type     | Mandatory   | Description                                |
+=========+==========+=============+============================================+
| Hotel   | string   | yes         | Hotel name (attribute ``id`` - hotel id)   |
+---------+----------+-------------+--------------------------------------------+
| Time    | HH:MM    | yes         | Departure time                             |
+---------+----------+-------------+--------------------------------------------+

**Child items (transfer location - *address*):**

+------------+-----------------------------------------+-------------+------------------------------------------------------------+
| Name       | Type                                    | Mandatory   | Description                                                |
+============+=========================================+=============+============================================================+
| Address    | Nested items AddressLine (one or two)   | yes         | Address (one or two strings not more than 40 characters)   |
+------------+-----------------------------------------+-------------+------------------------------------------------------------+
| ZipCode    | string                                  | yes         | Zip code (not more than 10 characters)                     |
+------------+-----------------------------------------+-------------+------------------------------------------------------------+
| District   | string                                  | yes         | District name (not more than 20 characters)                |
+------------+-----------------------------------------+-------------+------------------------------------------------------------+
| Phone      | string                                  | yes         | Phone number                                               |
+------------+-----------------------------------------+-------------+------------------------------------------------------------+
| Time       | HH:SS                                   | yes         | Departure time                                             |
+------------+-----------------------------------------+-------------+------------------------------------------------------------+

**Child items (transfer location- *port*):**

+-------------------+----------+-------------+----------------------------+
| Name              | Type     | Mandatory   | Description                |
+===================+==========+=============+============================+
| ShipName          | String   | yes         | Name of the ship           |
+-------------------+----------+-------------+----------------------------+
| ShipCompanyName   | string   | yes         | Name of the ship company   |
+-------------------+----------+-------------+----------------------------+
| DepartureCity     | string   | yes         | Arrival city name          |
+-------------------+----------+-------------+----------------------------+
| Time              | HH:MM    | yes         | Departure time             |
+-------------------+----------+-------------+----------------------------+

Order/Items/TransferItem/ChargeConditions item
----------------------------------------------

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

Order/Items/TransferItem/ChargeConditions/Cancellation item
-----------------------------------------------------------

Cancellation charges.

**Attributes:**

+----------+----------------+-------------+--------------------------------------+
| Name     | Type           | Mandatory   | Description                          |
+==========+================+=============+======================================+
| charge   | true / false   | Yes         | Charge applied(true), or no(false)   |
+----------+----------------+-------------+--------------------------------------+
| from     | Date           | No          | Charge from                          |
+----------+----------------+-------------+--------------------------------------+
| to       | Date           | No          | Charge to                            |
+----------+----------------+-------------+--------------------------------------+
| price    | Numeric        | No          | Price (if charge=true)               |
+----------+----------------+-------------+--------------------------------------+
| policy   | String         | No          | Charge policy                        |
+----------+----------------+-------------+--------------------------------------+
| charge   | true / false   | Yes         | Charge applied(true), or no(false)   |
+----------+----------------+-------------+--------------------------------------+

**Child items:** No.

Order/Items/TransferItem/ChargeConditions/Amendment item
--------------------------------------------------------

Amendment charges.

**Attributes:**

+----------+----------------+-------------+---------------------------------------+
| Name     | Type           | Mandatory   | Description                           |
+==========+================+=============+=======================================+
| charge   | true / false   | Yes         | Charge appllied(true), or no(false)   |
+----------+----------------+-------------+---------------------------------------+
| from     | Date           | No          | Charge from                           |
+----------+----------------+-------------+---------------------------------------+
| to       | Date           | No          | Charge to                             |
+----------+----------------+-------------+---------------------------------------+
| price    | Numeric        | No          | Price (if charge=true)                |
+----------+----------------+-------------+---------------------------------------+
| policy   | String         | No          | Charge policy                         |
+----------+----------------+-------------+---------------------------------------+
| charge   | true / false   | Yes         | Charge applied(true), or no(false)    |
+----------+----------------+-------------+---------------------------------------+

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