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

Request is passed via the URL with credentials(``login``, ``password``,``checksum``,..).

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
              <Vehicle>
                <CarInfo>         
                  <Detail>
                     <Title>...</Title>
                     <Value>...</Value>
                  </Detail>
              </CarInfo>
              <DriverInfo>         
                  <Detail>
                     <Title>...</Title>
                     <Value>...</Value>
                  </Detail>
              </DriverInfo>
              <LocationsInfo>
                  <PickUp>
                     <Detail>
                        <Title>...</Title>
                        <Value>...</Value>
                     </Detail>
                  </PickUp>
                  <DropOff>
                     <Detail>
                        <Title>...</Title>
                        <Value>...</Value>
                     </Detail>
                  </DropOff>
                </LocationsInfo>         
                <PolicyInfo>...</PolicyInfo>
                <RentConditions>...</RentConditions>
              </Vehicle>          
              <RentConditions>...</RentConditions>
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

**Attributes:** no.

**Child items:**

+----------+-------------+----------------------+
| Name     | Mandatory   | Description          |
+==========+=============+======================+
| Errors   | no          | List of the errors   |
+----------+-------------+----------------------+
| Order    | no          | Order description    |
+----------+-------------+----------------------+

Errors item
-----------

List of the errors

**Attributes:** no.

**Child items:**

+-------------------------+-------------------------+-------------------------+
| Name                    | Mandatory               | Description             |
+=========================+=========================+=========================+
| Error                   | yes                     | error description.      |
|                         |                         |  Attributes:            |
|                         |                         |                         |
|                         |                         | -  ``code`` - error     |
|                         |                         |    code                 |
|                         |                         | -  ``description`` -    |
|                         |                         |    error description    |
+-------------------------+-------------------------+-------------------------+

Order item
----------

Order description.

**Attributes:**

+--------+-----------+-------------+---------------+
| Name   | Type      | Mandatory   | Description   |
+========+===========+=============+===============+
| Id     | numeric   | yes         | order id      |
+--------+-----------+-------------+---------------+

| 
|  **Child items:**

+------------+-------------+---------------------------+
| Name       | Mandatory   | Description               |
+============+=============+===========================+
| ItemList   | yes         | List of the order items   |
+------------+-------------+---------------------------+

item Order/ItemList
-------------------

List of the order items.

**Attributes:** no.

**Child items:**

+--------+-------------+---------------------------+
| Name   | Mandatory   | Description               |
+========+=============+===========================+
| Item   | yes         | Order item description.   |
+--------+-------------+---------------------------+

item Order/ItemList/Item
------------------------

Orer item description.

**Attributes:**

+--------+-----------+-------------+------------------------+
| Name   | Type      | Mandatory   | Description            |
+========+===========+=============+========================+
| Id     | numeric   | yes         | id of the order item   |
+--------+-----------+-------------+------------------------+

| 
|  **Child items:**

+--------------------+----------+-------------+----------------+
| Name               | Type     | Mandatory   | Description    |
+====================+==========+=============+================+
| VoucherAvailable   | 0 \| 1   | yes         | Has voucher    |
+--------------------+----------+-------------+----------------+
| Voucher            | string   | yes         | Voucher data   |
+--------------------+----------+-------------+----------------+

item Order/ItemList/Item/Voucher
--------------------------------

Voucher information for item.

**Attributes:** no.

**Child items:**

+-------------------------+-------------+---------------------------------------------+
| Name                    | Mandatory   | Description                                 |
+=========================+=============+=============================================+
| Issued                  | yes         | Voucher date                                |
+-------------------------+-------------+---------------------------------------------+
| BookingDetails          | yes         | Details about booking                       |
+-------------------------+-------------+---------------------------------------------+
| Vehicle                 | yes         | Vehicle description                         |
+-------------------------+-------------+---------------------------------------------+
| AOTNumbers              | no          | Contact list for emergency communications   |
+-------------------------+-------------+---------------------------------------------+
| AdditionalInformation   | no          | Additional information                      |
+-------------------------+-------------+---------------------------------------------+

Order/ItemList/Item/Voucher/BookingDetails item
-----------------------------------------------

Details about booking

**Attributes:** no.

**Child items:**

+------------------------+----------------------------------+-------------+-----------------------------------------+
| Name                   | Type                             | Mandatory   | Description                             |
+========================+==================================+=============+=========================================+
| Supplier               | string                           | no          | Supplier name                           |
+------------------------+----------------------------------+-------------+-----------------------------------------+
| Reference              | string                           | no          | Order reference                         |
+------------------------+----------------------------------+-------------+-----------------------------------------+
| AdditionalDetailList   | Список itemов AdditionalDetail   | no          | List of additional data about booking   |
+------------------------+----------------------------------+-------------+-----------------------------------------+

item Order/ItemList/Item/Voucher/BookingDetails/AdditionalDetailLists/AdditionalDetailList
------------------------------------------------------------------------------------------

List of additional data about booking

**Attributes:** no.

**Child items:**

+-------------------------+-------------------------+-------------------------+
| Name                    | Mandatory               | Description             |
+=========================+=========================+=========================+
| AdditionalDetail        | no                      | Additional details -    |
|                         |                         | child items:            |
|                         |                         |                         |
|                         |                         | -  Title - parameter    |
|                         |                         |    name                 |
|                         |                         | -  Value - value        |
+-------------------------+-------------------------+-------------------------+

item Order/ItemList/Item/Voucher/Vehicle
----------------------------------------

Information about vehicle.

**Attributes:** no.

+------------------+----------+-------------+--------------------------------------------------+
| Name             | Type     | Mandatory   | Description                                      |
+==================+==========+=============+==================================================+
| CarInfo          | Nested   | yes         | Information about vehicle                        |
+------------------+----------+-------------+--------------------------------------------------+
| DriverInfo       | Nested   | yes         | Information about driver                         |
+------------------+----------+-------------+--------------------------------------------------+
| LocationsInfo    | Nested   | yes         | Information about pick up / drop off locations   |
+------------------+----------+-------------+--------------------------------------------------+
| PolicyInfo       | string   | yes         | Information about the insurance policy           |
+------------------+----------+-------------+--------------------------------------------------+
| RentConditions   | string   | yes         | Rent conditions                                  |
+------------------+----------+-------------+--------------------------------------------------+

item Order/ItemList/Item/Voucher/Vehicle/CarInfo
------------------------------------------------

Vehicle parameters (group, class)

**Attributes:** no.

**Child items:**

+-------------------------+-------------------------+-------------------------+
| Name                    | Mandatory               | Description             |
+=========================+=========================+=========================+
| Detail                  | no                      | Detail - child items:   |
|                         |                         |                         |
|                         |                         | -  Title - parameter    |
|                         |                         |    name                 |
|                         |                         | -  Value - value        |
+-------------------------+-------------------------+-------------------------+

item Order/ItemList/Item/Voucher/Vehicle/DriverInfo
---------------------------------------------------

Information about the driver

**Attributes:** no.

**Child items:**

+-------------------------+-------------------------+-------------------------+
| Name                    | Mandatory               | Description             |
+=========================+=========================+=========================+
| Detail                  | no                      | Detail - child items:   |
|                         |                         |                         |
|                         |                         | -  Title - parameter    |
|                         |                         |    name                 |
|                         |                         | -  Value - value        |
+-------------------------+-------------------------+-------------------------+

item Order/ItemList/Item/Voucher/LocationsInfo
----------------------------------------------

Information pick up / drop off locations

**Attributes:** no.

**Child items:**

+-----------+-------------+-------------------------------+
| Name      | Mandatory   | Description                   |
+===========+=============+===============================+
| PickUp    | yes         | pick up location parameters   |
+-----------+-------------+-------------------------------+
| DropOff   | yes         | drop off location parameter   |
+-----------+-------------+-------------------------------+

item Order/ItemList/Item/Voucher/Vehicle/LocationsInfo/PickUp
-------------------------------------------------------------

Pick up location parameters (date, hour, country, city, station, ... )

**Attributes:** no.

**Child items:**

+-------------------------+-------------------------+-------------------------+
| Name                    | Mandatory               | Description             |
+=========================+=========================+=========================+
| Detail                  | no                      | Detail - child items:   |
|                         |                         |                         |
|                         |                         | -  Title - parameter    |
|                         |                         |    name                 |
|                         |                         | -  Value - value        |
+-------------------------+-------------------------+-------------------------+

item Order/ItemList/Item/Voucher/Vehicle/LocationsInfo/DropOff
--------------------------------------------------------------

Drop off location parameters (date, hour, country, city, station, ... )

**Attributes:** no.

**Child items:**

+-------------------------+-------------------------+-------------------------+
| Name                    | Mandatory               | Description             |
+=========================+=========================+=========================+
| Detail                  | no                      | Detial - child items:   |
|                         |                         |                         |
|                         |                         | -  Title - parameter    |
|                         |                         |    name                 |
|                         |                         | -  Value - value        |
+-------------------------+-------------------------+-------------------------+

item Order/ItemList/Item/Voucher/AOTNumbers
-------------------------------------------

Contact list for emergency communications.

**Attributes:** no.

**Child items:**

+--------------------+--------------------+--------------------+--------------------+
| Name               | Type               | Mandatory          | Description        |
+====================+====================+====================+====================+
| Location           | string             | yes                | Phones for the     |
|                    |                    |                    | city specified in  |
|                    |                    |                    | the attribute:     |
|                    |                    |                    |                    |
|                    |                    |                    | -  ``name`` - city |
|                    |                    |                    |    name            |
+--------------------+--------------------+--------------------+--------------------+