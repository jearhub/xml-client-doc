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
              <Transfer>
                 <Date>...</Date>
                 <Name>...</Name>
                 <Description>...</Description>
                 <Language>...</Language>
                 <LeadPassenger>...</LeadPassenger>
                 <TotalPassengers>...</TotalPassengers>
                [<AdditionalDetailList>
                   <AdditionalDetail>
                      <Title>...</Title>
                      <Value>...</Value>
                   </AdditionalDetail>
                 </AdditionalDetailList>]
              </Transfer>
              <PickUp>
                 <LocationDetail>
                    <Title>...</Title>
                    <Value>...</Value>
                 </LocationDetail>
              </PickUp>
              <DropOff>
                 <LocationDetail>
                    <Title>...</Title>
                    <Value>...</Value>
                 </LocationDetail>
              </DropOff>
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

Order information.

**Attributes:**

+------+---------+-----------+-------------+
| Name | Type    | Mandatory | Description |
+======+=========+===========+=============+
| Id   | Numeric | Yes       | Order id    |
+------+---------+-----------+-------------+

**Child items:**

+----------+-----------+---------------------+
| Name     | Mandatory | Description         |
+==========+===========+=====================+
| ItemList | Yes       | List of order items |
+----------+-----------+---------------------+

Order/ItemList item
-------------------

List of order items.

**Attributes:** No.

**Child items:**

+------+-----------+------------------------+
| Name | Mandatory | Description            |
+======+===========+========================+
| Item | Yes       | Order item description |
+------+-----------+------------------------+

Order/ItemList/Item item
------------------------

Item description.

**Attributes:**

+------+---------+-----------+-----------------------+
| Name | Type    | Mandatory | Description           |
+======+=========+===========+=======================+
| Id   | Numeric | Yes       | Order item identifier |
+------+---------+-----------+-----------------------+

**Child items:**

+------------------+--------+-----------+--------------+
| Name             | Type   | Mandatory | Description  |
+==================+========+===========+==============+
| VoucherAvailable | 0 / 1  | Yes       | Has voucher  |
+------------------+--------+-----------+--------------+
| Voucher          | String | Yes       | Voucher data |
+------------------+--------+-----------+--------------+

Order/ItemList/Item/Voucher item
--------------------------------

Voucher information for item.

**Attributes:** No.

**Child items:**

+-----------------------+-----------+-------------------------------------------+
| Name                  | Mandatory | Description                               |
+=======================+===========+===========================================+
| Issued                | Yes       | Voucher date                              |
+-----------------------+-----------+-------------------------------------------+
| BookingDetails        | Yes       | Details about booking                     |
+-----------------------+-----------+-------------------------------------------+
| Transfer              | Yes       | Transfer details                          |
+-----------------------+-----------+-------------------------------------------+
| PickUp                | Yes       | Pick up details                           |
+-----------------------+-----------+-------------------------------------------+
| DropOff               | Yes       | Drop off details                          |
+-----------------------+-----------+-------------------------------------------+
| AOTNumbers            | No        | Contact list for emergency communications |
+-----------------------+-----------+-------------------------------------------+
| AdditionalInformation | No        | Additional info                           |
+-----------------------+-----------+-------------------------------------------+

Order/ItemList/Item/Voucher/BookingDetails item
-----------------------------------------------

Details about booking

**Attributes:** No.

**Child items:**

+----------------------+--------------------------------+-----------+---------------------------------------+
| Name                 | Type                           | Mandatory | Description                           |
+======================+================================+===========+=======================================+
| Supplier             | String                         | No        | Supplier name                         |
+----------------------+--------------------------------+-----------+---------------------------------------+
| Reference            | String                         | No        | Order reference                       |
+----------------------+--------------------------------+-----------+---------------------------------------+
| AdditionalDetailList | List of AdditionalDetail items | No        | List of additional data about booking |
+----------------------+--------------------------------+-----------+---------------------------------------+

Order/ItemList/Item/Voucher/BookingDetails/AdditionalDetailLists/AdditionalDetailListitem
-----------------------------------------------------------------------------------------

List of additional data about booking

**Attributes:** No.

**Child items:**

+------------------+-----------+-----------------------------------+
| Name             | Mandatory | Description                       |
+==================+===========+===================================+
| AdditionalDetail | No        | Additional details - child items: |
|                  |           | -  Title - parameter name         |
|                  |           | -  Value - value                  |
+------------------+-----------+-----------------------------------+

Order/ItemList/Item/Voucher/Transfer item
-----------------------------------------

Transfer information (item).

**Attributes:** No.

+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| Name                 | Type                           | Mandatory | Description                                                                                     |
+======================+================================+===========+=================================================================================================+
| Date                 | String                         | Yes       | Transfer date (for example, "12 December 2012")                                                 |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| Name                 | String                         | Yes       | Transfer name                                                                                   |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| Description          | String                         | Yes       | Transfer description                                                                            |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| Language             | String                         | Yes       | Transfer language                                                                               |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| LeadPassenger        | String                         | Yes       | Transfer leading pax                                                                            |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| TotalPassengers      | Number                         | Yes       | Total number of passengers                                                                      |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+
| AdditionalDetailList | List of AdditionalDetail items | No        | List of additional transfer details (similarly to Voucher/BookingDetails/AdditionalDetailLists) |
+----------------------+--------------------------------+-----------+-------------------------------------------------------------------------------------------------+

Order/ItemList/Item/Voucher/PickUp item
---------------------------------------

Pick up parameters

**Attributes:** no.

**Child items:**

+----------------+-----------+------------------------------+
| Name           | Mandatory | Description                  |
+================+===========+==============================+
| LocationDetail | No        | two child items:             |
|                |           |                              |
|                |           | -  Title - parameter's name  |
|                |           | -  Value - parameter's value |
+----------------+-----------+------------------------------+

Order/ItemList/Item/Voucher/DropOff item
----------------------------------------

Drop off parameters

**Atributes:** no.

**Child items:**

+----------------+-----------+------------------------------+
| Name           | Mandatory | Description                  |
+================+===========+==============================+
| LocationDetail | No        | two child items:             |
|                |           |                              |
|                |           | -  Title - parameter's name  |
|                |           | -  Value - parameter's value |
+----------------+-----------+------------------------------+

Order/ItemList/Item/Voucher/AOTNumbers item
-------------------------------------------

Contact list for emergency communications.

**Attributes:** No.

**Child items:**

+----------+--------+-----------------------+-------------------------------------------------+
| Name     | Type   | Mandatory Description |                                                 |
+==========+========+=======================+=================================================+
| Location | String | Yes                   | Phones for the city specified in the attribute: |
|          |        |                       |                                                 |
|          |        |                       | -  ``name`` - city name                         |
+----------+--------+-----------------------+-------------------------------------------------+