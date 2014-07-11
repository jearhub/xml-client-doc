Search details
##############

Description of XML schema
=========================

XSD-schema:

:download:`www/xsd/transfer/TransferSearchDetailsRequest.xsd <../../themes/hotelbook/static/xsd/transfer/TransferSearchDetailsRequest.xsd>`

:download:`www/xsd/transfer/TransferSearchDetailsResponse.xsd <../../themes/hotelbook/static/xsd/transfer/TransferSearchDetailsResponse.xsd>`

Request
-------

A request for additional information may be conducted only when we know
the id search (searchId) and id results (resultId) from the search.

XSD-schema request:

::


    <?xml version="1.0" encoding="utf-8"?>

    <TransferSearchDetailsRequest>
      <TransferSearches>
        <TransferSearch>
          <SearchId>..</SearchId> - search id
          <ResultId>..</ResultId> - result id from search
        </TransferSearch>
      </TransferSearches>
    </TransferSearchDetailsRequest>

TransferSearchDetailsRequest item
---------------------------------

You may retrieve information about cancellation policies.

- Parent item.
- Attributes: no.

Child items:

+----------------------+--------------------+-----------------+-----------------+-----------------+
| **Item**             | **Mandatory**      | **Description** |                 |                 |
+======================+====================+=================+=================+=================+
| ``TransferSearches`` | yes                | Transfers       |                 |                 |
+----------------------+--------------------+-----------------+-----------------+-----------------+
|                      | **Item**           | **Mandatory**   | **Description** |                 |
+----------------------+--------------------+-----------------+-----------------+-----------------+
|                      | ``TransferSearch`` | yes             | Transfer        |                 |
+----------------------+--------------------+-----------------+-----------------+-----------------+
|                      |                    | **Item**        | **Mandatory**   | **Description** |
+----------------------+--------------------+-----------------+-----------------+-----------------+
|                      |                    | ``SearchId``    | yes             | search id       |
+----------------------+--------------------+-----------------+-----------------+-----------------+
|                      |                    | ``ResultId``    | yes             | result id       |
+----------------------+--------------------+-----------------+-----------------+-----------------+

TransferSearches item
---------------------

The element specifies a list of transfers from the search results(`TransferSearchResponse <#h1164-8>`_).

- Mandatory item.
- Attributes: no.

Child items:

+--------------------+---------------+----------------------+
| **Item**           | **Mandatory** | **Description**      |
+====================+===============+======================+
| ``TransferSearch`` | yes           | transfer from search |
+--------------------+---------------+----------------------+

TransferSearch item
^^^^^^^^^^^^^^^^^^^

In response you can see identifiers: ``TransferSearch->searchId`` – search id and ``Transfers->Transfer->resultId`` – result id (own for each transfer).

- Mandatory item.

Child items:

+--------------+---------------+-----------------+
| **Item**     | **Mandatory** | **Description** |
+==============+===============+=================+
| ``SearchId`` | yes           | search id       |
+--------------+---------------+-----------------+
| ``ResultId`` | yes           | result id       |
+--------------+---------------+-----------------+

Response, TransferSearchDetailsResponse
---------------------------------------

XML-schema response:

::


    <?xml version="1.0" encoding="utf-8"?>
    <TransferSearchDetailsResponse>
      <TransferSearchDetailsRequest>... source XML request ...</TransferSearchDetailsRequest>

      [<Errors>
        <Error code="..." description="..."> - list of errors
      </Errors>]
      <TransferSearchDetails>

        <Transfer
        resultId="id"
        transferName="..." 
        [providerId="id"] -- depend on user rights this item can be miss
        confirmation="onRequest|online|inaccessible"  -- confirmation type
        price="orig_price"  -- price in foreign currency
        currency=".."
        comparePrice=" -- price in rubles
        [useNds="true|false"]
        passengers=".." -- maximum number of passengers
        [transferTime="true|false"]
        [checkInTime="true|false"]
        >
        <Language id=".." > </Language>
        <Vehicle id=".." >
           <Name >...</Name>
           <Description >...</Description>
        </Vehicle>
        <PickUp
          cityId="id"
          locationType="id"
         [locationId="id"]/>
        <DropOff
          cityId="id"
          locationType="id"
         [locationId="id"]/>

        <ChargeConditions> - policies
          <Currency>..</Currency>
          <Cancellations> - cancellations policies
            <Cancellation
              charge="true|false" - charge presence

              [from="2008-02-28T11:50:00"] - charge start date
              [to="2008-02-28T11:50:00"] - charge end date

              [price="100.00"] - price (item is presence only if charge=true)
              [policy="1 night"] - charge policy
            />

          </Cancellations>
          <Amendments> - amendment policies
            <Amendment
              charge="true|false"
              [from="YYYY-MM-DDThh:ii:ss"]
              [to="YYYY-MM-DDThh:ii:ss"]
              [price=".."]
              [policy=".."]
            />

          </Amendments>
        </ChargeConditions>
            
        </Transfer>
      </TransferSearchDetails>

    </TransferSearchDetailsResponse>

TransferSearchDetailsResponse item
----------------------------------

Parent item.

- Attributes: no.

Child items:

+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
| **Item**                         | **Mandatory** | **Description**                |                             |                                   |
+==================================+===============+================================+=============================+===================================+
| ``TransferSearchDetailsRequest`` | no            | Source request                 |                             |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
| ``Errors``                       | no            | List of errors                 |                             |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  | **Item**      | **Mandatory**                  | **Description**             |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  | ``Error``     | yes                            | Error description with code |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
| ``TransferSearchDetails``        | no            | List of transfers with details |                             |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  | **Item**      | **Mandatory**                  | **Description**             |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  | ``Transfer``  | yes                            | Transfer search details     |                                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | **Item**                       | **Mandatory**               | **Description**                   |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | ``Language``                   | yes                         | Language of transfer              |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | ``Vehicle``                    | yes                         | Vehicle of transfer               |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | ``PickUp``                     | yes                         | Pick up parameters                |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | ``DropOff``                    | yes                         | Drop off parameters               |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | ``Information``                | yes                         | Additional information            |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+
|                                  |               | ``ChargeConditons``            | no                          | Amendment & cancellation policies |
+----------------------------------+---------------+--------------------------------+-----------------------------+-----------------------------------+

TransferSearchDetailsRequest item
---------------------------------

Source XML request.

- Optional item.

Errors item
-----------

View :doc:`Error page <../errors>`


TransferSearchDetails item
--------------------------

List of errors.

- Optional item.
- Attributes: no.

Child items:

+--------------+---------------------+-------------------+------------------------+----------------------+
| **Item**     | **Mandatory**       | **Description**   |                        |                      |
+==============+=====================+===================+========================+======================+
| ``Transfer`` | yes                 | Search details    |                        |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | **Item**            | **Mandatory**     | **Description**        |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | ``Language``        | yes               | Language of transfer   |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | ``Vehicle``         | yes               | Vehicle of transfer    |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | ``PickUp``          | yes               | Pick up parameters     |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | ``DropOff``         | yes               | Drop off parameters    |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | ``Information``     | yes               | Additional information |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              | ``ChargeConditons`` | no                | Charges                |                      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              |                     | **Item**          | **Mandatory**          | **Description**      |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              |                     | ``Currency``      | yes                    | Currency             |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              |                     | ``Cancellations`` | yes                    | Cancellation charges |
+--------------+---------------------+-------------------+------------------------+----------------------+
|              |                     | ``Amendments``    | no                     | Amendment charges    |
+--------------+---------------------+-------------------+------------------------+----------------------+

Transfer item
^^^^^^^^^^^^^

List of attributes of the found transfer, its language, vehicle, pick up
and dropp off.

Mandatory: no. Miss if there are errors or there are no transfers
suitable for search parameters.

Attributes of ``Transfer``:

+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| **Attribute**    | **Type**                        | **Mandatory** | **Description**                                                                     |
+==================+=================================+===============+=====================================================================================+
| ``resultId``     | number                          | yes           | Result id. Different for every found transfer.                                      |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``transferName`` | string                          | no            | Transfer name (short description)                                                   |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``providerId``   | number                          | no            | Provider id, which give information of this transfer. This id show not to all users |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``confirmation`` | onRequest, online, inaccessible | yes           | Confirmation type                                                                   |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``price``        | price                           | yes           | Price in foreign ``currency``                                                       |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``currency``     | string                          | yes           | Transfer currency name                                                              |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``comparePrice`` | price                           | yes           | Price in rubles                                                                     |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``useNds``       | true, false                     | no            | Use VAT or not                                                                      |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``passengers``   | number                          | yes           | Maximum number of passengers                                                        |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``transferTime`` | string                          | no            | Transfer time                                                                       |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+
| ``checkInTime``  | string                          | no            | Check in time                                                                       |
+------------------+---------------------------------+---------------+-------------------------------------------------------------------------------------+

 Child items of ``Transfer``: ``Language``, ``Vehicle``, ``PickUp``, ``DropOff``, ``Information``

Language item
'''''''''''''

Transfer language.

- Mandatory: yes.
- Attributes: language id (from /xml/languages)
- Child items: no.

Vehicle item
''''''''''''

Transfer vehicle.

- Mandatory: yes.
- Attributes: vehicle id (from /xml/transfer\_vehicles)

Child items:

+-----------------+---------------+---------------------+
| **Item**        | **Mandatory** | **Description**     |
+=================+===============+=====================+
| ``Name``        | yes           | Vehicle name        |
+-----------------+---------------+---------------------+
| ``Description`` | yes           | Vehicle description |
+-----------------+---------------+---------------------+

PickUp item
-----------

Pick up parameters.

- Mandatory.

Attributes:

+------------------+----------+---------------+----------------------------------------------------------------------------------------+
| **Attributes**   | **Type** | **Mandatory** | **Description**                                                                        |
+==================+==========+===============+========================================================================================+
| ``cityId``       | number   | yes           | City id, full list can be found at /xml/cities                                         |
+------------------+----------+---------------+----------------------------------------------------------------------------------------+
| ``locationType`` | number   | yes           | Transfer location id, full list can be found at /xml/transfer\_locations               |
+------------------+----------+---------------+----------------------------------------------------------------------------------------+
| ``locationId``   | number   | no            | Airport id or Station id, full list can be found at /xml/airports and at /xml/stations |
+------------------+----------+---------------+----------------------------------------------------------------------------------------+

Child items: no.

DropOff item
------------

Drop off parameters.

- Mandatory.

Attributes:

+------------------+----------+---------------+----------------------------------------------------------------------------------------+
| **Attributes**   | **Type** | **Mandatory** | **Description**                                                                        |
+==================+==========+===============+========================================================================================+
| ``cityId``       | number   | yes           | City id, full list can be found at /xml/cities                                         |
+------------------+----------+---------------+----------------------------------------------------------------------------------------+
| ``locationType`` | number   | yes           | Transfer location id, full list can be found at /xml/transfer\_locations               |
+------------------+----------+---------------+----------------------------------------------------------------------------------------+
| ``locationId``   | number   | no            | Airport id or Station id, full list can be found at /xml/airports and at /xml/stations |
+------------------+----------+---------------+----------------------------------------------------------------------------------------+

Child items: no.

ChargeConditions item
'''''''''''''''''''''

Cancellation and amendment charges.

- Optional item.
- Attributes: no.

Child items:

+-------------------+------------------+----------------------+-----------------+
| **Item**          | **Mandatory**    | **Description**      |                 |
+===================+==================+======================+=================+
| ``Currency``      | yes              | Foreign currency     |                 |
+-------------------+------------------+----------------------+-----------------+
| ``Cancellations`` | yes              | Cancellation charges |                 |
+-------------------+------------------+----------------------+-----------------+
|                   | **Item**         | **Mandatory**        | **Description** |
+-------------------+------------------+----------------------+-----------------+
|                   | ``Cancellation`` | yes                  | Charge          |
+-------------------+------------------+----------------------+-----------------+
| ``Amendments``    | no               | Amendment charges    |                 |
+-------------------+------------------+----------------------+-----------------+
|                   | **Item**         | **Mandatory**        | **Description** |
+-------------------+------------------+----------------------+-----------------+
|                   | ``Amendment``    | yes                  | Charge          |
+-------------------+------------------+----------------------+-----------------+

Cancellation item
'''''''''''''''''

Cancellation charges.

- Mandatory item.
- Child items: no.

Attributes:

+---------------+----------+---------------+-----------------------------------------------+
| **Attribute** | **Type** | **Mandatory** | **Description**                               |
+===============+==========+===============+===============================================+
| ``charge``    | boolean  | yes           | charge applied(if true)                       |
+---------------+----------+---------------+-----------------------------------------------+
| ``from``      | date     | no            | start time                                    |
+---------------+----------+---------------+-----------------------------------------------+
| ``to``        | date     | no            | end time                                      |
+---------------+----------+---------------+-----------------------------------------------+
| ``price``     | numeric  | no            | price (if ``charge``=true, else empty charge) |
+---------------+----------+---------------+-----------------------------------------------+
| ``policy``    | string   | no            | charge policy                                 |
+---------------+----------+---------------+-----------------------------------------------+

Amendment item
''''''''''''''

Amendment charges.

- Mandatory item.
- Child items: no.