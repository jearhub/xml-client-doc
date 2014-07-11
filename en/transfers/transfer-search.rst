Search Transfers
################

Description of XML-schema
=========================

XSD-schema:

:download:`www/xsd/transfer/TransferSearchRequest.xsd <../../themes/hotelbook/static/xsd/transfer/TransferSearchRequest.xsd>`

:download:`www/xsd/transfer/TransferSearchResponse.xsd <../../themes/hotelbook/static/xsd/transfer/TransferSearchResponse.xsd>`

Asynchronous search - see `SearchId item <#h1285-20>`_

Request, TransferSearchRequest
------------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>

    <TransferSearchRequest>
      <Request
        date="YYYY-MM-DD"
        passengers=".."
       [language="id"]/>
       [vehicle="id"]/>
       [assistant="true|false"]/>
       [confirmation="online|onRequest|all"]/>
      <Providers>
         <ProviderId>..</ProviderId>
      </Providers>
      <PickUp
        cityId="id"
        locationType="id"
       [locationId="id"]/>
      <DropOff
        cityId="id"
        locationType="id"
       [locationId="id"]/>
    </TransferSearchRequest>

TransferSearchRequest item
--------------------------

Request for transfer searching .

- Room item.
- Attributes: no.

Child items of ``TransferSearchRequest``:

+---------------+----------------+------------------------------------+------------------------------------+
| **Item**      | **Mandatory**  | **Description**                    |                                    |
+===============+================+====================================+====================================+
| ``Request``   | yes            | Request parameters (as attributes) |                                    |
+---------------+----------------+------------------------------------+------------------------------------+
|               | **Item**       | **Mandatory**                      | **Description**                    |
+---------------+----------------+------------------------------------+------------------------------------+
| ``Providers`` | no             | Providers list                     |                                    |
+---------------+----------------+------------------------------------+------------------------------------+
|               | **Item**       | **Mandatory**                      | **Описание**                       |
+---------------+----------------+------------------------------------+------------------------------------+
|               | ``ProviderId`` | yes                                | Provider id (can be several items) |
+---------------+----------------+------------------------------------+------------------------------------+
| ``PickUp``    | yes            | Pick up attributes                 |                                    |
+---------------+----------------+------------------------------------+------------------------------------+
| ``DropOff``   | yes            | Drop off attributes                |                                    |
+---------------+----------------+------------------------------------+------------------------------------+

Request item
------------

Request parameters are in this item.

- Mandatory.
- Child items: no.

Attributes of ``Request``:

+------------------+-------------------------------+---------------+--------------------------------------------------------------+
| **Attribute**    | **Type**                      | **Mandatory** | **Description**                                              |
+==================+===============================+===============+==============================================================+
| ``date``         | date in format ``YYYY-MM-DD`` | yes           | Transfer date                                                |
+------------------+-------------------------------+---------------+--------------------------------------------------------------+
| ``passengers``   | number                        | yes           | Number of passengers                                         |
+------------------+-------------------------------+---------------+--------------------------------------------------------------+
| ``language``     | number                        | no            | Language id, full list can be found at /xml/languages        |
+------------------+-------------------------------+---------------+--------------------------------------------------------------+
| ``vehicle``      | number                        | no            | Vehicle id, full list can be found /xml/transfer\_vehicles   |
+------------------+-------------------------------+---------------+--------------------------------------------------------------+
| ``assistant``    | true, false                   | no            | Necessity of assistant                                       |
+------------------+-------------------------------+---------------+--------------------------------------------------------------+
| ``confirmation`` | online, onRequest, all        | no            | Confirmation type. If "all" or miss – dont take into account |
+------------------+-------------------------------+---------------+--------------------------------------------------------------+

Providers item
--------------

List of providers. Optional item.

- Attributes: no.

Child items:

+----------------+---------------+-----------------+
| **Item**       | **Mandatory** | **Description** |
+================+===============+=================+
| ``ProviderId`` | yes           | provider id     |
+----------------+---------------+-----------------+

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

Response, TransferSearchResponse
--------------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>

    <TransferSearchResponse>
      <TransferSearchRequest>... source request ...</TransferSearchRequest>
      <Errors>
        <Error code="..." description="..."> - errors
      </Errors>

      <TransferSearch searchId="id" >
         <SearchPickUp  
        countryId="id"
        countryName="..."
        resortId="id"
        resortName="..."
        cityid="id"
        cityName="..." />
         <SearchDropOff  
        countryId="id"
        countryName="..."
        resortId="id"
        resortName="..."
        cityid="id"
        cityName="..." />
      </TransferSearch >

      <Transfers>
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
        </Transfer>
      </Transfers>
    </TransferSearchResponse>

TransferSearchResponse item
---------------------------

Response from server.

- Root item.
- Attributes: no.

Child items of ``TransferSearchResponse``:

+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
| **Item**                  | **Mandatory** | **Description**                            |                                                   |                        |
+===========================+===============+============================================+===================================================+========================+
| ``TransferSearchRequest`` | no            | Sorce request, see – TransferSearchRequest |                                                   |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
| ``Errors``                | no            | Errors (if exist)                          |                                                   |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           | **Item**      | **Mandatory**                              | **Description**                                   |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           | ``Error``     | yes                                        | Error code and description (can be several items) |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
| ``TransferSearch``        | no            | Request parameters                         |                                                   |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
| ``Transfers``             | no            | Transfer list                              |                                                   |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           | **Item**      | **Mandatory**                              | **Description**                                   |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           | ``Transfer``  | no                                         | Found transfer                                    |                        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           |               | **Item**                                   | **Mandatory**                                     | **Description**        |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           |               | ``Language``                               | yes                                               | Language of transfer   |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           |               | ``Vehicle``                                | yes                                               | Vehicle of transfer    |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           |               | ``PickUp``                                 | yes                                               | Pick up parameters     |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           |               | ``DropOff``                                | yes                                               | Drop off parameters    |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+
|                           |               | ``Information``                            | yes                                               | Additional information |
+---------------------------+---------------+--------------------------------------------+---------------------------------------------------+------------------------+

TransferSearchRequest item
--------------------------

Source XML-request of user.

- Mandatory: no. Miss if this request was with syntax errors.
- See shema above (``TransferSearchRequest``)

Errors item
-----------

View :doc:`Error page <../errors>`

TransferSearch item
-------------------

Search parameters.

- Mandatory: no. Miss if there are errors.

Attributes:

+---------------+----------+---------------+-----------------+
| **Attribute** | **Type** | **Mandatory** | **Description** |
+===============+==========+===============+=================+
| ``searchId``  | number   | yes           | id of searching |
+---------------+----------+---------------+-----------------+

Child items:

+--------------------+---------------+---------------------+
| **Item**           | **Mandatory** | **Description**     |
+====================+===============+=====================+
| ``SearchPickUp ``  | yes           | Pick up parameters  |
+--------------------+---------------+---------------------+
| ``SearchDropOff `` | yes           | Drop off parameters |
+--------------------+---------------+---------------------+

SearchPickUp item
-----------------

Pick up parameters.

- Child items: no.

Attributes:

+-----------------+----------+---------------+------------------------------------------------------+
| **Attribute**   | **Type** | **Mandatory** | **Description**                                      |
+=================+==========+===============+======================================================+
| ``countryId``   | number   | yes           | Country id, full list can be found at /xml/countries |
+-----------------+----------+---------------+------------------------------------------------------+
| ``countryName`` | string   | yes           | Country name                                         |
+-----------------+----------+---------------+------------------------------------------------------+
| ``resortId``    | number   | yes           | Resort id, full list can be found at /xml/resorts    |
+-----------------+----------+---------------+------------------------------------------------------+
| ``resortName``  | string   | yes           | Resort name                                          |
+-----------------+----------+---------------+------------------------------------------------------+
| ``cityId``      | number   | yes           | City id, full list can be found at /xml/cities       |
+-----------------+----------+---------------+------------------------------------------------------+
| ``cityName``    | string   | yes           | City name                                            |
+-----------------+----------+---------------+------------------------------------------------------+

SearchDropOff item
------------------

Drop off parameters.

- Child items: no.

Attributes:

+-----------------+----------+---------------+------------------------------------------------------+
| **Attribute**   | **Type** | **Mandatory** | **Description**                                      |
+=================+==========+===============+======================================================+
| ``countryId``   | number   | yes           | Country id, full list can be found at /xml/countries |
+-----------------+----------+---------------+------------------------------------------------------+
| ``countryName`` | string   | yes           | Country name                                         |
+-----------------+----------+---------------+------------------------------------------------------+
| ``resortId``    | number   | yes           | Resort id, full list can be found at /xml/resorts    |
+-----------------+----------+---------------+------------------------------------------------------+
| ``resortName``  | string   | yes           | Resort name                                          |
+-----------------+----------+---------------+------------------------------------------------------+
| ``cityId``      | number   | yes           | City id, full list can be found at /xml/cities       |
+-----------------+----------+---------------+------------------------------------------------------+
| ``cityName``    | string   | yes           | City name                                            |
+-----------------+----------+---------------+------------------------------------------------------+

Transfers item
--------------

Transfer list (child items: ``Transfer``).

- Mandatory: no. Miss if there are errors.
- Attributes: no.

Child items of ``Transfers``:

+--------------+-----------------+--------------------------------+------------------------+
| **Item**     | **Mandatory**   | **Description**                |                        |
+==============+=================+================================+========================+
| ``Transfer`` | no              | Found transfer, its attributes |                        |
+--------------+-----------------+--------------------------------+------------------------+
|              | **Item**        | **Mandatory**                  | **Description**        |
+--------------+-----------------+--------------------------------+------------------------+
|              | ``Language``    | yes                            | Language of transfer   |
+--------------+-----------------+--------------------------------+------------------------+
|              | ``Vehicle``     | yes                            | Vehicle of transfer    |
+--------------+-----------------+--------------------------------+------------------------+
|              | ``PickUp``      | yes                            | Pick up parameters     |
+--------------+-----------------+--------------------------------+------------------------+
|              | ``DropOff``     | yes                            | Drop off parameters    |
+--------------+-----------------+--------------------------------+------------------------+
|              | ``Information`` | yes                            | Additional information |
+--------------+-----------------+--------------------------------+------------------------+

Transfer item
^^^^^^^^^^^^^

| List of attributes of the found transfer, its language, vehicle, pick up and dropp off.
| Mandatory: no. Miss if there are errors or there are no transfers suitable for search parameters.

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

 Child items of ``Transfer``:  ``Language``, ``Vehicle``, ``PickUp``, ``DropOff``, ``Information``

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

Information item
-------------------
Additional information.

SearchId item
-------------

In case, when transfer searching is asynchronously (whith parameter ?async=1), then item will be contain id of innitialized search. Then this response will come immediately and at the Hotelbook side search
will be processed as background task. Found transfers can be asked
periodically by request ``/xml/transfer_search_async?login=&search_id=&from_result_id=`` (every second, for example). For details see `transfer-search-async.html <transfer-search-async.html>`_
Mandatory: no. Miss if there are errors.