Order item information
######################

Description of XML schema
=========================

A request for a list of categories is formed through URL (using GET method).

XSD-schema response:

-  ``www/xsd/OrderItemInfoResponse.xsd``

Request
-------

You can specify parameter ``?order_id=id``, or parameter ``?item_id=id``.

Request path: ``/xml/order_item_info``

Response, OrderItemInfoResponse
-------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderItemInfoResponse>
      [<Errors>
        <Error code="..." description="..."> - list of errors
      </Errors>]
     
      <Items
            orderId="..." - order identifier
            orderUserId="..." orderUserName="..." - user id and name
            orderManagerId="..." orderManagerName="..." - manager id and name
            >
        <Item type="hotel" id="..." [useNds="true|false"] /> - hotels in the order
        [<Item type="transfer" id="..." [useNds="true|false"] />] - transfers in the order
        [<Item type="vehicle" id="..."/>] - vehicles in the order
        <Item type="visa" id="..."> - visa
          <Status>...</Status> - visa status
          <Country id="...">...</Country> - country visa
          <VisaCity>spb|msk</VisaCity> - city visa
          <DepartureDate>...</DepartureDate> - departure date
          <ArrivalDate>...</ArrivalDate> - arrival date
          <ArrivalPlace>...</ArrivalPlace> - arrival place (text)
          <Transport type="avia|sea|railway|avto">
            <Date>...</Date> 
            <From>
              <City id=""/> 
            </From>
            <To>
              <City id=""/> 
            </To>
            [<Number>...</Number>] - flight number
            [<FlightTime>...</FlightTime>] 
          </Transport>
          <Price currency="...">...</Price>
          <PassportChild>...</PassportChild> - number of children in passport
          <Paxes>
            <Pax id="..." [pax_id="..."]>
              [<Title>Mr|Ms|Mrs|Chld</Title>]
              [<Name>...</Name>]
              [<SecondName>...</SecondName>]
              [<BirthDate>...</BirthDate>]
              [<IsChild [age="..."]>true|false</IsChild>]
              [<Citizenship id="...">...</Citizenship>]
              [<Passport> - passport info
                <Series>...</Series>
                <Number>...</Number>
                <Expiration>...</Expiration>
              </Passport>]
              [<Insurances>
                [<Insurance id="...">...</Insurance>] 
              </Insurances>]
            </Pax>
          </Paxes>
          <Hotels>
            <Hotel
                   itemId="..."
                   id="..." - hotel id
                   cityId="..." - city id
                   countryId="..." - country id
                   from="..." - check in date
                   to="..." - check out date
                   [external_hotel = 'true'] 
                   >...</Hotel> - hotel name
          </Hotels>
        </Item>
        <Item type="invitation" id="..."> - invitations
          <Status>...</Status> - status
          <Country id="...">...</Country>
          <Provider id="...">...</Provider> - provider
          <Price currency="...">...</Price>
          <Paxes>
                  <Pax id="..." [pax_id="..."]>
                    [<Title>Mr|Ms|Mrs|Chld</Title>]
                    [<Name>...</Name>]
                    [<SecondName>...</SecondName>]
                    [<BirthDate>...</BirthDate>]
                    [<IsChild [age="..."]>true|false</IsChild>]
                    [<Citizenship id="...">...</Citizenship>]
                    [<Passport> 
                      <Series>...</Series>
                      <Number>...</Number>
                      <Expiration>...</Expiration>
                    </Passport>]
                    [<Insurances>
                      [<Insurance id="...">...</Insurance>] 
                    </Insurances>]
                  </Pax>
          </Paxes>
          <Hotels>
                <Hotel
                           itemId="..."
                           id="..." - hotel id

                           cityId="..." - city id
                           countryId="..." - country id
                           from="..." - check in date

                           to="..." - check out date
                           [external_hotel = 'true']  
                       >...</Hotel> - hotel name
          </Hotels>
        </Item>
      </Items>
    </OrderItemInfoResponse>

OrderItemInfoResponse item
--------------------------
Item information

Parent item.

**Attributes:** No.

**Child items:**

+----------+-------------+------------------+
| Name     | Mandatory   | Description      |
+==========+=============+==================+
| Errors   | No          | List of errors   |
+----------+-------------+------------------+
| Items    | No          | List of items    |
+----------+-------------+------------------+

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

Items item
----------

List of items.

**Attributes:**

+------------------+---------+-----------+--------------+
| Name             | Type    | Mandatory | Description  |
+==================+=========+===========+==============+
| orderId          | Numeric | Yes       | Order id     |
+------------------+---------+-----------+--------------+
| orderUserId      | Numeric | Yes       | User id      |
+------------------+---------+-----------+--------------+
| orderUserName    | String  | Yes       | User name    |
+------------------+---------+-----------+--------------+
| orderManagerId   | Numeric | No        | Manager id   |
+------------------+---------+-----------+--------------+
| orderManagerName | String  | No        | Manager name |
+------------------+---------+-----------+--------------+

**Child items:**

+--------+-------------+--------------------+
| Name   | Mandatory   | Description        |
+========+=============+====================+
| Item   | No          | Item information   |
+--------+-------------+--------------------+

Items/Item item
---------------

Item information

**Attributes:**

+----------+----------------------------------------------+-------------+----------------+
| Name     | Type                                         | Mandatory   | Description    |
+==========+==============================================+=============+================+
| type     | hotel, transfer, vehicle, visa, invitation   | Yes         | Type           |
+----------+----------------------------------------------+-------------+----------------+
| id       | Numeric                                      | Yes         | Item id        |
+----------+----------------------------------------------+-------------+----------------+
| useNds   | true / false                                 | No          | VAT included   |
+----------+----------------------------------------------+-------------+----------------+

**Child items:**

+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Name          | Type    | Mandatory              | Description                                                           |
+===============+=========+========================+=======================================================================+
| Status        | String  | Yes                    | Status                                                                |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Country       | String  | Yes                    | Country. Attributes: id - country id                                  |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Provider      | String  | For visa               | Visa support. Attributes: id - provider identifier                    |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| VisaCity      | msk,spb | For visa               | Visa city                                                             |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| DepartureDate | Date    | For visa               | Departure date                                                        |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| ArrivalDate   | Date    | For visa               | Arrival date                                                          |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| ArrivalPlace  | String  | For visa               | Arrival Place                                                         |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Transport     |         | For visa               | Transport information                                                 |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Price         | String  | For visa or invitation | Price for item. Attributes: currency                                  |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| PassportChild | Numeric | For visa               | Number of children in passport                                        |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Paxes         |         | For visa or invitation | List of paxes. Child items: Pax - pax information                     |
+---------------+---------+------------------------+-----------------------------------------------------------------------+
| Hotels        |         | For visa or invitation | List of hotels in visa/invitation. Child items: Hotel - hotel details |
+---------------+---------+------------------------+-----------------------------------------------------------------------+

Items/Item/Transport item
-------------------------

Transport information.

**Attributes:**

+--------+----------------------------+-------------+---------------+
| Name   | Type                       | Mandatory   | Description   |
+========+============================+=============+===============+
| type   | avia, sea, railway, avto   | Yes         | Type          |
+--------+----------------------------+-------------+---------------+

**Child items:**

+--------------+----------+-------------+-------------------------------+
| Name         | Type     | Mandatory   | Description                   |
+==============+==========+=============+===============================+
| Date         | Date     | Yes         | Date of arrival / departure   |
+--------------+----------+-------------+-------------------------------+
| From         |          | Yes         | From                          |
+--------------+----------+-------------+-------------------------------+
| To           |          | Yes         | To                            |
+--------------+----------+-------------+-------------------------------+
| Number       | String   | No          | Flight number                 |
+--------------+----------+-------------+-------------------------------+
| FlightTime   | Time     | No          | Flight time (arrival time)    |
+--------------+----------+-------------+-------------------------------+

Items/Item/Transport/From and Items/Item/Transport/To item
----------------------------------------------------------

**Attributes:** No.

**Child items:**

+------+------+-----------+----------------------------------------+
| Name | Type | Mandatory | Description                            |
+======+======+===========+========================================+
| City | Type | Yes       | City of path. Attributes: id - City id |
+------+------+-----------+----------------------------------------+

Items/Item/Paxes/Pax item
-------------------------

Information about pax.

**Attributes:**

+---------+-----------+-------------+---------------+
| Name    | Type      | Mandatory   | Description   |
+=========+===========+=============+===============+
| id      | Numeric   | Yes         | pax id        |
+---------+-----------+-------------+---------------+
| paxId   | Numeric   | No          | pax id        |
+---------+-----------+-------------+---------------+

**Child items:**

+-------------+--------------+-----------+-------------------------------------------------+
| Name        | Type         | Mandatory | Description                                     |
+=============+==============+===========+=================================================+
| Title       | Mr, Mrs, Ms, | Chld No   | Title                                           |
+-------------+--------------+-----------+-------------------------------------------------+
| Name        | String       | No        | Name                                            |
+-------------+--------------+-----------+-------------------------------------------------+
| SecondName  | String       | No        | Last name                                       |
+-------------+--------------+-----------+-------------------------------------------------+
| BirthDate   | Date         | No        | Birth date                                      |
+-------------+--------------+-----------+-------------------------------------------------+
| IsChild     | true / false | No        | Attributes: age                                 |
+-------------+--------------+-----------+-------------------------------------------------+
| Citizenship | String       | No        | Citizenship. Attributes:                        |
|             |              |           |                                                 |
|             |              |           | - id - country id                               |
+-------------+--------------+-----------+-------------------------------------------------+
| Passport    |              | No        | Passport information.                           |
|             |              |           | Child items:                                    |
|             |              |           |                                                 |
|             |              |           | - Series - passport series                      |
|             |              |           | - Number - passport number                      |
|             |              |           | - Expiration - passport expiration date         |
+-------------+--------------+-----------+-------------------------------------------------+
| Insurances  | String       | Yes       | List of insurances. Child items: Insurance - id |
+-------------+--------------+-----------+-------------------------------------------------+

Items/Item/Hotels/Hotel item
----------------------------

Hotel in visa

**Attributes:**

+-------------+-----------+-------------+-------------------+
| Name        | Type      | Mandatory   | Description       |
+=============+===========+=============+===================+
| itemId      | Numeric   | Yes         | item id (hotel)   |
+-------------+-----------+-------------+-------------------+
| id          | Numeric   | Yes         | hotel id          |
+-------------+-----------+-------------+-------------------+
| cityId      | Numeric   | Yes         | city id           |
+-------------+-----------+-------------+-------------------+
| countryId   | Numeric   | Yes         | country id        |
+-------------+-----------+-------------+-------------------+
| from        | Date      | Yes         | Arrival date      |
+-------------+-----------+-------------+-------------------+
| to          | Date      | Yes         | Departure date    |
+-------------+-----------+-------------+-------------------+

**Child items:** No.