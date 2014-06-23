Order information
#################

Description of XML schema
=========================

A request is formed through URL (using GET method).

XSD-schema response:

-  ``www/xsd/OrderInfoResponse.xsd``

Request
-------

The request must be an parameter - order_id, taken from the response to
the AddOrder request. Request is passed via the URL with
credentials(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/order_info``

Response, OrderInfoResponse
---------------------------

::

    <?xml version="1.0" encoding="utf-8"?>

        <OrderInfoResponse>
         [<Errors>
            <Error code="..." description="..."> - errors
          </Errors>]
          <Order>

            <Id>...</Id> - order id
            <Tag>...</Tag> - order reference
            [<AccountComment>...</AccountComment>] - Comment for the account (Mandatory item if XML-client has right "View account comment")
            <State>...</State> - orer status
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

              <VehicleItem itemId="40036"> - order item (vehicle)
              <ProviderId>...</ProviderId> - provier id
              <ProviderReference>...</ProviderReference> - provider booking reference
              <State>...</State> - item order state         
              <Editable>...</Editable> - editable orer item
              <Description>...</Description> - vehicle description
              <Passengers>...</Passengers> - passenges
              <Driver>...</Driver> - vehicle driver, link to the pax
              <CarName>...</CarName> - vehicle name
              <ACRISS>...</ACRISS> - ACRISS code
              <OneWay>...</OneWay> - option "One Way"
              <Doors>...</Doors> - number of doors
              <LuggageLarge>...</LuggageLarge>
              <LuggageSmall>...</LuggageSmall>
              <Company companyId="12" companyName="EuropCar"/> - service company
              <Policy policyId="2" policyName="All Inclusive"> - insurance policy
              <Inclusives>
                  <Inclusive>...</Inclusive> - id of the inclusive option
              </Inclusives>
              <Extras> - extra options
                  <Extra>...</Extra> - id of the extra option           
              </Extras>
             

              <PickUp date="2013-06-07" hour="10:00"
               countryId="24" countryName="United Kingdom"
               cityId="2322" cityName="London"
               flightNum="123GH"/>
               hotelId="2445" hotelNameAddress="..."/>
                 <Station id="606149">
                 </Station>           
              </PickUp>

                 <DropOff date="2013-06-07" hour="10:00"
               countryId="24" countryName="United Kingdom"
               cityId="2322" cityName="London"
               flightNum="123GH"/>
               hotelId="2445" hotelNameAddress="..."/>           
                 <Station id="606149">
                 </Station>
                 </DropOff>
                 
                <SpecialOffer date="2013-06-07" hour="10:00"
              />             
                 </DropOff>
                 
              <TotalPrice>...</TotalPrice>
              [<Fee>...</Fee>] - charge (if there is it)
              <Currency>...</Currency>
              [<UseNds>true|false</UseNds>] - VAT

              <Information>...</Information>
                

              <ChargeConditions>

                <Currency>..</Currency> - currency of the charges
                <Cancellations> - штрафы при отмене
                  <Cancellation - может быть несколько таких itemов

                    charge="true|false" - есть ли штраф

                    [from="2008-02-28T11:50:00"] - start date of the charge
                    [to="2008-02-28T11:50:00"]

                    [price="100.00"] - price ((optional) charge=true)
                    [policy="1 ночь"] - policy of the charge

                  />
                </Cancellations>
                <Amendments> - amendment charges
                  <Amendment - may be more one
                    charge="true|false"

                    [from="YYYY-MM-DDThh:ii:ss"]
                    [to="YYYY-MM-DDThh:ii:ss"]
                    [price=".."]

                    [policy=".."]

                  />
                </Amendments>
              </ChargeConditions>


            </VehicleItem>

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

**Attributes:** no.

**Child items:**

+----------+-------------+-------------------------------+
| Name     | Mandatory   | Description                   |
+==========+=============+===============================+
| Errors   | no          | List of the errors.           |
+----------+-------------+-------------------------------+
| Order    | no          | information about the order   |
+----------+-------------+-------------------------------+

Errors item
-----------

Список ошибок (если есть).

**Attributes:** no.

**Child items:**

+-------+-----------+----------------------------------------+
| Name  | Mandatory | Description                            |
+=======+===========+========================================+
| Error | yes       | Description error. Attributes:         |
|       |           |                                        |
|       |           | -  ``code`` - error code               |
|       |           | -  ``description`` - error description |
+-------+-----------+----------------------------------------+




item Order
----------

Description of the order.

**Attributes:** no.

**Child items:**

+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Name           | Type                   | Mandatory | Description                                                                                                                                       |
+================+========================+===========+===================================================================================================================================================+
| Id             | numeric                | yes       | order id                                                                                                                                          |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Tag            | string                 | yes       | order reference                                                                                                                                   |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| AccountComment | String                 | no        | Comment for the account (Mandatory item if XML-client has right "View account comment")                                                           |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| State          | string                 | yes       | order state (new, modified, cancelled, etc.)                                                                                                      |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| CreationDate   | YYYY-MM-DD HH:MM:SS    | yes       | Date and time of order creation (for example, 2013-01-11 12:23:00)                                                                                |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| PayForm        | string                 | yes       | Order pay form (cash, cashless, undefined). If order elements have different pay form (it's possible for old orders), order pay form is undefined |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Account_1C     | List of Document items | no        | Account information 1C                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Paxes          | List                   | yes       | List of paxes in order                                                                                                                            |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| Items          | List                   | yes       | List of items (vehicles)                                                                                                                          |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+
| ContactInfo    | Nested                 | yes       | Contact information about customer                                                                                                                |
+----------------+------------------------+-----------+---------------------------------------------------------------------------------------------------------------------------------------------------+

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

item Order/Paxes
----------------

List of the persons

**Attributes:** no.

**Child items:**

+--------+-------------+----------------------------+
| Name   | Mandatory   | Description                |
+========+=============+============================+
| Pax    | yes         | Information about person   |
+--------+-------------+----------------------------+

item Order/Paxes/Pax
--------------------

Information about person.

**Attributes:**

+---------+-----------------+-------------+--------------------+
| Name    | Type            | Mandatory   | Description        |
+=========+=================+=============+====================+
| paxId   | numeric         | yes         | id of the person   |
+---------+-----------------+-------------+--------------------+
| child   | true or false   | yes         | if child, true     |
+---------+-----------------+-------------+--------------------+

**Child items:**

+-------------+---------------------+-------------+---------------+
| Name        | Type                | Mandatory   | Description   |
+=============+=====================+=============+===============+
| Title       | Mr, Mrs, Ms, Chld   | yes         | Title         |
+-------------+---------------------+-------------+---------------+
| FirstName   | string              | yes         | Name          |
+-------------+---------------------+-------------+---------------+
| LastName    | string              | yes         | Last name     |
+-------------+---------------------+-------------+---------------+

.. note::  **Attantion:** *``FullName`` item now is optional and will be remove from 01.01.2013*

item Order/Items/VehicleItem
----------------------------

Information about vehicle.

**Attributes:**

+----------+-----------+-------------+------------------------+
| Name     | Type      | Mandatory   | Description            |
+==========+===========+=============+========================+
| itemId   | numeric   | yes         | id of the order item   |
+----------+-----------+-------------+------------------------+

**Child items:**

+-------------------+---------------+-----------+------------------------------------------------------------+
| Name              | Type          | Mandatory | Description                                                |
+===================+===============+===========+============================================================+
| ProviderId        | numeric       | yes       | provider id                                                |
+-------------------+---------------+-----------+------------------------------------------------------------+
| ProviderReference | string        | yes       | provider booking reference                                 |
+-------------------+---------------+-----------+------------------------------------------------------------+
| State             | numeric       | yes       | orer item state (new, processed, commited, cancelled etc.) |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Editable          | true, false   | yes       | Editable of the order item                                 |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Description       | string        | no        | vehicle description                                        |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Passengers        | numeric       | yes       | passengers                                                 |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Driver            | numeric       | yes       | vehicle driver, link to the pax                            |
+-------------------+---------------+-----------+------------------------------------------------------------+
| CarName           | string        | yes       | vehicle name                                               |
+-------------------+---------------+-----------+------------------------------------------------------------+
| ACRISS            | string        | yes       | ACRISS code                                                |
+-------------------+---------------+-----------+------------------------------------------------------------+
| OneWay            | string        | yes       | option "One way"                                           |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Doors             | numeric       | yes       | number of the doors                                        |
+-------------------+---------------+-----------+------------------------------------------------------------+
| LuggageLarge      | numeric       | yes       | large luggage                                              |
+-------------------+---------------+-----------+------------------------------------------------------------+
| LuggageSmall      | numeric       | yes       | small luggage                                              |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Company           | -             | yes       | company                                                    |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Policy            | -             | yes       | insurance policy                                           |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Inclusives        | Nested        | yes       | inclusives                                                 |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Extras            | Nested        | yes       | extra options                                              |
+-------------------+---------------+-----------+------------------------------------------------------------+
| PickUp            | Nested        | yes       | pick up location parameters                                |
+-------------------+---------------+-----------+------------------------------------------------------------+
| DropOff           | Nested        | yes       | drop off location parameters                               |
+-------------------+---------------+-----------+------------------------------------------------------------+
| SpecialOffer      | Nested        | yes       | special offer                                              |
+-------------------+---------------+-----------+------------------------------------------------------------+
| TotalPrice        | numeric       | yes       | total price                                                |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Fee               | numeric       | yes       | charge (if there is it)                                    |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Currency          | string        | yes       | currency                                                   |
+-------------------+---------------+-----------+------------------------------------------------------------+
| UseNds            | true or false | no        | If VAT is included                                         |
+-------------------+---------------+-----------+------------------------------------------------------------+
| Information       | string        | yes       | Provider additional information                            |
+-------------------+---------------+-----------+------------------------------------------------------------+
| ChargeConditions  | Nested        | no        | List of the charges                                        |
+-------------------+---------------+-----------+------------------------------------------------------------+

item Order/Items/VehicleItem/Company
------------------------------------

Company services

**Attributes:**

+-------------+---------+-----------+--------------+
| Name        | Type    | Mandatory | Description  |
+=============+=========+===========+==============+
| companyId   | numeric | no        | company id   |
+-------------+---------+-----------+--------------+
| companyName | string  | no        | company name |
+-------------+---------+-----------+--------------+

**Child items:** no

item Order/Items/VehicleItem/Policy
-----------------------------------

Insurance policy

**Attributes:**

+------------+---------+-----------+------------------------------+
| Name       | Type    | Mandatory | Description                  |
+============+=========+===========+==============================+
| policyId   | numeric | no        | id of the insurance policy   |
+------------+---------+-----------+------------------------------+
| policyName | string  | no        | name of the insurance policy |
+------------+---------+-----------+------------------------------+

**Child items:** no

item Order/Items/VehicleItem/Inclusives
---------------------------------------

Inclusives

**Attributes:**no.

**Child items:**

+-----------+--------+-----------+----------------------------------------------------------------+
| Name      | Type   | Mandatory | Description                                                    |
+===========+========+===========+================================================================+
| Inclusive | string | yes       | Name of the inclusive (attribute ``id`` - id of the inclusive) |
+-----------+--------+-----------+----------------------------------------------------------------+

item Order/Items/VehicleItem/Extras
-----------------------------------

Extras

**Attributes:**no.

**Child items:**

+-------+--------+-----------+---------------------------------------------------------------+
| Name  | Type   | Mandatory | Description                                                   |
+=======+========+===========+===============================================================+
| Extra | string | yes       | Name of the extra (attribute ``id`` - id of the extra option) |
+-------+--------+-----------+---------------------------------------------------------------+

item Order/Items/VehicleItem/PickUp
-----------------------------------

Pick up location parameters

**Attributes:**

+------------------+-------------------+-----------+---------------------------------------------------+
| Name             | Type              | Mandatory | Description                                       |
+==================+===================+===========+===================================================+
| date             | string (YY-mm-dd) | yes       | pick up date                                      |
+------------------+-------------------+-----------+---------------------------------------------------+
| hour             | string (HH:ii)    | yes       | pick up hour                                      |
+------------------+-------------------+-----------+---------------------------------------------------+
| countryId        | numeric           | yes       | id of the pick up country                         |
+------------------+-------------------+-----------+---------------------------------------------------+
| countryName      | string            | yes       | name of the pick up country                       |
+------------------+-------------------+-----------+---------------------------------------------------+
| cityId           | numeric           | yes       | id of the pick up city                            |
+------------------+-------------------+-----------+---------------------------------------------------+
| cityName         | string            | yes       | name of the pick up city                          |
+------------------+-------------------+-----------+---------------------------------------------------+
| airportId        | numeric           | no        | id of the pick up airport (optional)              |
+------------------+-------------------+-----------+---------------------------------------------------+
| airportName      | string            | no        | name of the pick up airport (optional)            |
+------------------+-------------------+-----------+---------------------------------------------------+
| flightNum        | string            | no        | flight number (optional)                          |
+------------------+-------------------+-----------+---------------------------------------------------+
| hotelId          | numeric           | no        | id of the hotel delivery (optional)               |
+------------------+-------------------+-----------+---------------------------------------------------+
| hotelNameAddress | string            | no        | name and address of the hotel delivery (optional) |
+------------------+-------------------+-----------+---------------------------------------------------+

**Child items:**

+---------+--------+-----------+----------------------------+
| Name    | Type   | Mandatory | Description                |
+=========+========+===========+============================+
| Station | Nested | yes       | Pick up station parameters |
+---------+--------+-----------+----------------------------+

item Order/Items/VehicleItem/DropOff
------------------------------------

Drop off location parameters

**Attributes:**

+-------------+-------------------+-----------+-----------------------------------------+
| Name        | Type              | Mandatory | Description                             |
+=============+===================+===========+=========================================+
| date        | string (YY-mm-dd) | yes       | drop off date                           |
+-------------+-------------------+-----------+-----------------------------------------+
| hour        | string (HH:ii)    | yes       | drop off hour                           |
+-------------+-------------------+-----------+-----------------------------------------+
| countryId   | numeric           | yes       | id of the drop off country              |
+-------------+-------------------+-----------+-----------------------------------------+
| countryName | string            | yes       | name of the drop off country            |
+-------------+-------------------+-----------+-----------------------------------------+
| cityId      | numeric           | yes       | id of the drop off city                 |
+-------------+-------------------+-----------+-----------------------------------------+
| cityName    | string            | yes       | name of the drop off city               |
+-------------+-------------------+-----------+-----------------------------------------+
| airportId   | numeric           | no        | id of the drop off airport (optional)   |
+-------------+-------------------+-----------+-----------------------------------------+
| airportName | string            | no        | name of the drop off airport (optional) |
+-------------+-------------------+-----------+-----------------------------------------+

**Child items:**

+---------+--------+-----------+-----------------------------+
| Name    | Type   | Mandatory | Description                 |
+=========+========+===========+=============================+
| Station | Nested | yes       | Drop off station parameters |
+---------+--------+-----------+-----------------------------+

item Order/Items/VehicleItem/PickUp/Station
-------------------------------------------

Pick up station parameters

**Attributes:**

+------+---------+-----------+---------------------------+
| Name | Type    | Mandatory | Description               |
+======+=========+===========+===========================+
| id   | numeric | yes       | id of the pick up station |
+------+---------+-----------+---------------------------+

**Child items:**

+-------------+------------------------+-----------+---------------------------------------+
| Name        | Type                   | Mandatory | Description                           |
+=============+========================+===========+=======================================+
| Name        | string                 | yes       | name of the pick up station           |
+-------------+------------------------+-----------+---------------------------------------+
| Address     | string                 | yes       | address of the pick up station        |
+-------------+------------------------+-----------+---------------------------------------+
| Phone       | string                 | yes       | phone of the pick up station          |
+-------------+------------------------+-----------+---------------------------------------+
| Часы работы | string (hh:ii - hh:ii) | yes       | openning hours of the pick up station |
+-------------+------------------------+-----------+---------------------------------------+

item Order/Items/VehicleItem/DropOff/Station
--------------------------------------------

Drop off station parameters

**Attributes:**

+------+---------+-----------+----------------------------+
| Name | Type    | Mandatory | Description                |
+======+=========+===========+============================+
| id   | numeric | yes       | id of the drop off station |
+------+---------+-----------+----------------------------+

**Child items:**

+-------------+------------------------+-----------+----------------------------------------+
| Name        | Type                   | Mandatory | Description                            |
+=============+========================+===========+========================================+
| Name        | string                 | yes       | Name of the drop off station           |
+-------------+------------------------+-----------+----------------------------------------+
| Address     | string                 | yes       | address of the drop off station        |
+-------------+------------------------+-----------+----------------------------------------+
| Phone       | string                 | yes       | phone of the drop off station          |
+-------------+------------------------+-----------+----------------------------------------+
| Часы работы | string (hh:ii - hh:ii) | yes       | Openning hours of the drop off station |
+-------------+------------------------+-----------+----------------------------------------+

item Order/Items/VehicleItem/ChargeConditions
---------------------------------------------

Cancellation and amendment charges

**Attributes:** no.

**Child items:**

+---------------+-----------+----------------------+
| Name          | Mandatory | Description          |
+===============+===========+======================+
| Currency      | yes       | Currency             |
+---------------+-----------+----------------------+
| Cancellations | yes       | Cancellation charges |
+---------------+-----------+----------------------+
| Amendments    | no        | Amendment charges    |
+---------------+-----------+----------------------+

item Order/Items/VehicleItem/ChargeConditions/Cancellation
----------------------------------------------------------

Cancellation charges.

**Attributes:**

+--------+---------------+-----------+------------------------------------+
| Name   | Type          | Mandatory | Description                        |
+========+===============+===========+====================================+
| charge | true or false | yes       | Charge applied(true), or no(false) |
+--------+---------------+-----------+------------------------------------+
| from   | Date          | no        | Charge from                        |
+--------+---------------+-----------+------------------------------------+
| to     | Date          | no        | Charge to                          |
+--------+---------------+-----------+------------------------------------+
| price  | numeric       | no        | Price (if charge=true)             |
+--------+---------------+-----------+------------------------------------+
| policy | string        | no        | Charge policy                      |
+--------+---------------+-----------+------------------------------------+
| charge | true / false  | yes       | Charge applied(true), or no(false) |
+--------+---------------+-----------+------------------------------------+

**Child items:** no.

item Order/Items/VehicleItem/ChargeConditions/Amendment
-------------------------------------------------------

Amendment charges.

**Attributes:**

+--------+---------------+-----------+-------------------------------------+
| Name   | Type          | Mandatory | Description                         |
+========+===============+===========+=====================================+
| charge | true / false  | yes       | Charge appllied(true), or no(false) |
+--------+---------------+-----------+-------------------------------------+
| from   | Date          | no        | Charge from                         |
+--------+---------------+-----------+-------------------------------------+
| to     | Date          | no        | Charge to                           |
+--------+---------------+-----------+-------------------------------------+
| price  | numeric       | no        | Price (if charge=true)              |
+--------+---------------+-----------+-------------------------------------+
| policy | string        | no        | Charge policy                       |
+--------+---------------+-----------+-------------------------------------+
| charge | true or false | yes       | Charge applied(true), or no(false)  |
+--------+---------------+-----------+-------------------------------------+

 **Child items:** no.

item Order/ContactInfo
----------------------

Contact information.

**Attributes:** no.

**Child items:**

+---------+------------------------+-----------+-------------------+
| Name    | Type                   | Mandatory | Description       |
+=========+========================+===========+===================+
| Name    | string (max 100 chars) | yes       | Full name         |
+---------+------------------------+-----------+-------------------+
| Email   | String (max 100 chars) | yes       | email             |
+---------+------------------------+-----------+-------------------+
| Phone   | string (max 15 chars)  | yes       | phone             |
+---------+------------------------+-----------+-------------------+
| Comment | string                 | yes       | comment(optional) |
+---------+------------------------+-----------+-------------------+
