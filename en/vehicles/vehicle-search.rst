Search Vehicle
##############

Description of XML-schema
=========================

XSD-schema:

-  ``www/xsd/VehicleSearchRequest.xsd``
-  ``www/xsd/VehicleSearchResponse.xsd``

Asynchronous search - see `SearchId item <#h1285-20>`_

Request, VehicleSearchRequest
-----------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>

    <VehicleSearchRequest>
      <Request    
       [vehicleClass="all"]/>
       [vehicleType="all"]/>
       [vehicleTransmission="all"]/>   
       [vehicleAC="all"]/>   
       [seats="0"]/>   
       [confirmation="all"]/>   
      <Providers>
         <ProviderId>..</ProviderId>
      </Providers>
      <PickUp
        cityId="id"    
       [airportId="id"]
       date="YY-mm-dd"
       hour="HH:ii"/>
      <DropOff
        cityId="id"    
       [airportId="id"]
       date="YY-mm-dd"
       hour="HH:ii"/>
    </VehicleSearchRequest>

VehicleSearchRequest
--------------------

Request

- Parent item.
- Attributes: no.

Child items ``VehicleSearchRequest``:

+---------------+----------------+----------------------------------------------+------------------------------+
| **item**      | **Mandatory**  | **Description**                              |                              |
+===============+================+==============================================+==============================+
| ``Request``   | no             | Параметры запроса (как Attributeы)           |                              |
+---------------+----------------+----------------------------------------------+------------------------------+
|               | **item**       | **Mandatory**                                | **Description**              |
+---------------+----------------+----------------------------------------------+------------------------------+
| ``Providers`` | no             | Поставщики                                   |                              |
+---------------+----------------+----------------------------------------------+------------------------------+
|               | **item**       | **Mandatory**                                | **Description**              |
+---------------+----------------+----------------------------------------------+------------------------------+
|               | ``ProviderId`` | yes                                          | Поставщик (может быть много) |
+---------------+----------------+----------------------------------------------+------------------------------+
| ``PickUp``    | yes            | Параметры получения vehicle (как Attributeы) |                              |
+---------------+----------------+----------------------------------------------+------------------------------+
| ``DropOff``   | yes            | Параметры возврата vehicle (как Attributeы)  |                              |
+---------------+----------------+----------------------------------------------+------------------------------+

item Request
------------

В itemе указываются параметры запроса (как Attributeы).

- Mandatory item.
- Child items: no.

Attributes itemа ``Request``:

+-------------------------+------------------------+---------------+-------------------------------------------------------------------+
| **Attribute**           | **Type**               | **Mandatory** | **Description**                                                   |
+=========================+========================+===============+===================================================================+
| ``vehicleClass``        | string                 | no            | id of the vehicle class, /xml/vehicle\_classes;                   |
+-------------------------+------------------------+---------------+-------------------------------------------------------------------+
| ``vehicleType``         | string                 | no            | id of the vehicle type, /xml/vehicle\_types;                      |
+-------------------------+------------------------+---------------+-------------------------------------------------------------------+
| ``vehicleTransmission`` | string                 | no            | id of the vehicle transmission type, /xml/vehicle\_transmissions; |
+-------------------------+------------------------+---------------+-------------------------------------------------------------------+
| ``vehicleAC``           | string                 | no            | id of the vehicle fuel type, /xml/vehicle\_fuel\_ac;              |
+-------------------------+------------------------+---------------+-------------------------------------------------------------------+
| ``seats``               | numeric                | no            | Кол-во мест в vehicle                                             |
+-------------------------+------------------------+---------------+-------------------------------------------------------------------+
| ``confirmation``        | online, onRequest, all | no            | kind of confirmation                                              |
+-------------------------+------------------------+---------------+-------------------------------------------------------------------+

Providers item
--------------

List of providers. Optional item.

- Not Mandatory item.
- Attributeов no.

Child items:

+----------------+---------------+-----------------------------+
| **item**       | **Mandatory** | **Description**             |
+================+===============+=============================+
| ``ProviderId`` | yes           | provider id, /xml/providers |
+----------------+---------------+-----------------------------+

PickUp item
-----------

Pick up parameters.

- Mandatory item.

Attributes:

+-----------------+---------------------+-----------------+--------------------------------------------+
| **Attribute**   | **Type**            | **Mandatory**   | **Description**                            |
+-----------------+---------------------+-----------------+--------------------------------------------+
| ``cityId``      | numeric             | yes             | id of the pick up city, /xml/cities        |
+-----------------+---------------------+-----------------+--------------------------------------------+
| ``airportId``   | numeric             | no              | id of the pick up airport, /xml/airports   |
+-----------------+---------------------+-----------------+--------------------------------------------+
| ``date``        | string (YY-mm-dd)   | no              | pick up date                               |
+-----------------+---------------------+-----------------+--------------------------------------------+
| ``hour``        | string (HH:ii)      | no              | pick up hour                               |
+-----------------+---------------------+-----------------+--------------------------------------------+

 Child items: no.

DropOff< item /h3> Drop off parameters.

- Mandatory item.

Attributes:

+---------------+-------------------+---------------+------------------------------------------+
| **Attribute** | **Type**          | **Mandatory** | **Description**                          |
+===============+===================+===============+==========================================+
| ``cityId``    | numeric           | yes           | id of the pick up city, /xml/cities      |
+---------------+-------------------+---------------+------------------------------------------+
| ``airportId`` | numeric           | no            | id of the pick up airport, /xml/airports |
+---------------+-------------------+---------------+------------------------------------------+
| ``date``      | string (YY-mm-dd) | no            | pick up date                             |
+---------------+-------------------+---------------+------------------------------------------+
| ``hour``      | string (HH:ii)    | no            | pick up hour                             |
+---------------+-------------------+---------------+------------------------------------------+

Child items: no.

Response, VehicleSearchResponse
-------------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>

    <VehicleSearchResponse>
      <VehicleSearchRequest>... request ...</VehicleSearchRequest>
      <Errors>
        <Error code="..." description="..."> - errors
      </Errors>

      <VehicleSearch searchId="id" >
         <SearchPickUp  
        countryId="id"
        countryName="..." 
        cityid="id"
        cityName="..." />
        [airportid="id"] 
        [airportName="..."] /> pick up
         <SearchDropOff  
        countryId="id"
        countryName="..." 
        cityid="id"
        cityName="..." />
        [airportid="id"] 
        [airportName="..."] /> - drop off
      </VehicleSearch >
            
      <Vehicles>
        <Vehicle
        resultId="id"
        vehicleName="..." 
        [providerId="id"] -- (optional),  - depend on user rights this item can be miss
        confirmation="onRequest|online|inaccessible"  -- confirmation type   
        specialOffer="id"  - special offer    
        >
        <VehicleClass id=".." > </VehicleClass>
        <VehicleType id=".." > </VehicleType>
        <VehicleCompany id=".." logo_url=".." > </VehicleCompany>
        <ACRISS 
           acrissClass="id" 
           acrissType="id"  
           acrissTransmission="id" 
           acrissFuelAC="id" > 
        </ACRISS>
        <VehicleImage url=".." />
        <VehicleInformation 
           doors=".." 
           auto=".."  
           ac=".." 
           luggagelarge=".." />
        <SpecialOffer 
           acrissClass="id" />
        </SpecialOffer>      
        <VehicleInsurancePolicy 
           id=".." 
           name=".."  
           price=".." 
           currency=".." 
           comparePrice=".."       
           currencyTarget=".." > 
        </VehicleInsurancePolicy>      
        </Vehicle>
      </Vehicles>
    </VehicleSearchResponse>

item VehicleSearchResponse
--------------------------

Response **VehicleSearchRequest**.

- Parent item.
- Attributeов no.

Child items ``VehicleSearchResponse``:

+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
| **item**                 | **Mandatory** | **Description**                            |                                                   |                               |
+==========================+===============+============================================+===================================================+===============================+
| ``VehicleSearchRequest`` | no            | Source request, see – VehicleSearchRequest |                                                   |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
| ``Errors``               | no            | List of the errors                         |                                                   |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          | **item**      | **Mandatory**                              | **Description**                                   |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          | ``Error``     | yes                                        | Error description (error code), (may be more one) |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
| ``VehicleSearch``        | no            | Request parameters search vehicle          |                                                   |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
| ``Vehicles``             | no            | List of the vehicles                       |                                                   |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          | **item**      | **Mandatory**                              | **Description**                                   |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          | ``Vehicle``   | no                                         | vehicle                                           |                               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | **item**                                   | **Mandatory**                                     | **Description**               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``VehicleClass``                           | no                                                | vehicle class                 |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``VehicleType``                            | no                                                | vehicle type                  |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``VehicleCompany``                         | no                                                | company service               |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``ACRISS``                                 | yes                                               | vehicle ACRISS-code           |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``VehicleImage``                           | no                                                | vehicle image                 |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``VehicleInformation``                     | no                                                | Information about the vehicle |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``SpecialOffer``                           | no                                                | special offer                 |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+
|                          |               | ``VehicleInsurancePolicy``                 | no                                                | Insurance policy              |
+--------------------------+---------------+--------------------------------------------+---------------------------------------------------+-------------------------------+

item VehicleSearchRequest
-------------------------

Source request.

- Not Mandatory item. Miss if this request was with syntax errors.
- See shema above (``VehicleSearchRequest``)

item Errors
-----------

List of the errors (Child items ``Error``).

- Not Mandatory item.
- Attributeов no.

Child items ``Errors``:

+-----------+---------------+------------------------------------------------------------------------+
| **item**  | **Mandatory** | **Description**                                                        |
+===========+===============+========================================================================+
| ``Error`` | yes           | Error code(``code``) & description(``description``) as item attributes |
+-----------+---------------+------------------------------------------------------------------------+

Error item
^^^^^^^^^^

Description and code of the error

- Mandatory item.
- Child items: no.

Attributes itemа ``Error``:

+-----------------+----------+---------------+-------------------+
| **Attribute**   | **Type** | **Mandatory** | **Description**   |
+=================+==========+===============+===================+
| ``code``        | string   | yes           | Error code UTS.   |
+-----------------+----------+---------------+-------------------+
| ``description`` | string   | yes           | Error description |
+-----------------+----------+---------------+-------------------+

VehicleSearch item
------------------

Search parameters.

- Not Mandatory item. Miss if this request was with syntax errors.

Attributes:

+---------------+----------+---------------+-----------------+
| **Attribute** | **Type** | **Mandatory** | **Description** |
+===============+==========+===============+=================+
| ``searchId``  | numeric  | yes           | searc id        |
+---------------+----------+---------------+-----------------+

 Child items:

+--------------------+---------------+-----------------+
| **item**           | **Mandatory** | **Description** |
+====================+===============+=================+
| ``SearchPickUp ``  | yes           | pick up         |
+--------------------+---------------+-----------------+
| ``SearchDropOff `` | yes           | drop off        |
+--------------------+---------------+-----------------+

item SearchPickUp
-----------------

Pick up parameters.

- Chld items: no.

Attributes:

+-----------------+----------+---------------+-------------------------------------------+
| **Attribute**   | **Type** | **Mandatory** | **Description**                           |
+=================+==========+===============+===========================================+
| ``countryId``   | numeric  | yes           | id of the pick up country, /xml/countries |
+-----------------+----------+---------------+-------------------------------------------+
| ``countryName`` | string   | yes           | Country name                              |
+-----------------+----------+---------------+-------------------------------------------+
| ``cityId``      | numeric  | yes           | id of the pick up city, /xml/cities       |
+-----------------+----------+---------------+-------------------------------------------+
| ``cityName``    | string   | yes           | City name                                 |
+-----------------+----------+---------------+-------------------------------------------+
| ``airportId``   | numeric  | no            | id of the pick up airport, /xml/airports  |
+-----------------+----------+---------------+-------------------------------------------+
| ``airportName`` | string   | no            | Airport name                              |
+-----------------+----------+---------------+-------------------------------------------+

SearchDropOff item
------------------

Drop of parameters.

- Child items: no.

Attributes:

+-----------------+----------+---------------+--------------------------------------------+
| **Attribute**   | **Type** | **Mandatory** | **Description**                            |
+=================+==========+===============+============================================+
| ``countryId``   | numeric  | yes           | id of the drop off country, /xml/countries |
+-----------------+----------+---------------+--------------------------------------------+
| ``countryName`` | string   | yes           | Country name                               |
+-----------------+----------+---------------+--------------------------------------------+
| ``cityId``      | numeric  | yes           | id of the drop off city, /xml/cities       |
+-----------------+----------+---------------+--------------------------------------------+
| ``cityName``    | string   | yes           | City name                                  |
+-----------------+----------+---------------+--------------------------------------------+
| ``airportId``   | numeric  | no            | id of the drop off airport, /xml/airports  |
+-----------------+----------+---------------+--------------------------------------------+
| ``airportName`` | string   | no            | Airport name                               |
+-----------------+----------+---------------+--------------------------------------------+

Vehicles item
-------------

List of the vehicles (Child items ``Vehicle``).

- Not Mandatory item. Miss if this request was with syntax errors.
- Attributeов no.

Child items ``Vehicles``:

+-------------+----------------------------+-----------------------------------+-------------------------------+
| **item**    | **Mandatory**              | **Description**                   |                               |
+=============+============================+===================================+===============================+
| ``Vehicle`` | no                         | Найденное vehicle, его Attributes |                               |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | **item**                   | **Mandatory**                     | **Description**               |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``VehicleClass``           | no                                | Class vehicle                 |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``VehicleType``            | no                                | Type vehicle                  |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``VehicleCompany``         | no                                | company service               |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``ACRISS``                 | yes                               | ACRISS-code vehicle           |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``VehicleImage``           | no                                | vehicle image                 |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``VehicleInformation``     | no                                | Information about the vehicle |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``SpecialOffer``           | no                                | Special offer                 |
+-------------+----------------------------+-----------------------------------+-------------------------------+
|             | ``VehicleInsurancePolicy`` | no                                | Insurance policy              |
+-------------+----------------------------+-----------------------------------+-------------------------------+

Vehicle item
^^^^^^^^^^^^

Vehicle parameters. Class, Type, Company, ACRISS-code, Image ...

- Not Mandatory item. Miss if there are errors or there are no vehicle suitable for search parameters..

Attributes itemа ``Vehicle``:

+------------------+---------------------------------+---------------+--------------------------------------------------------+
| **Attribute**    | **Type**                        | **Mandatory** | **Description**                                        |
+==================+=================================+===============+========================================================+
| ``resultId``     | numeric                         | yes           | result id.                                             |
+------------------+---------------------------------+---------------+--------------------------------------------------------+
| ``vehicleName``  | string                          | no            | vehicle name                                           |
+------------------+---------------------------------+---------------+--------------------------------------------------------+
| ``providerId``   | numeric                         | no            | provider id. This information is not available to all. |
+------------------+---------------------------------+---------------+--------------------------------------------------------+
| ``confirmation`` | onRequest, online, inaccessible | yes           | confirmation type.                                     |
+------------------+---------------------------------+---------------+--------------------------------------------------------+
| ``specialOffer`` | numeric                         | yes           | Special offer.                                         |
+------------------+---------------------------------+---------------+--------------------------------------------------------+

 Child items ``Vehicle``:  ``VehicleClass``, ``VehicleType``, ``VehicleCompany``, ``ACRISS``, ``VehicleImage``, ``VehicleInformation``, ``SpecialOffer``, ``VehicleInsurancePolicy``

item VehicleClass
'''''''''''''''''

Class vehicle.

- Not Mandatory item.
- Attributes: id of the vehicle class (/xml/vehicle\_classes)
- Child items: no.

VehicleType item
''''''''''''''''

Type vehicle.

- Not Mandatory item.
- Attributes: id of the vehicle type ( /xml/vehicle\_types)
- Child items: no.

VehicleCompany item
'''''''''''''''''''

Company service.

- Not Mandatory item.

Attributes:

+---------------+----------+---------------+---------------------------------------------------+
| **Attribute** | **Type** | **Mandatory** | **Description**                                   |
+===============+==========+===============+===================================================+
| ``id``        | numeric  | yes           | id of the vehicle class ( /xml/vehicle_companies) |
+---------------+----------+---------------+---------------------------------------------------+
| ``logo_url``  | string   | yes           | url of the logo company                           |
+---------------+----------+---------------+---------------------------------------------------+

Child items: no.

ACRISS item
'''''''''''

ACRISS-code vehicle.

- Mandatory item.

Attributes:

+------------------------+----------+---------------+------------------------------------------------------------------+
| **Attribute**          | **Type** | **Mandatory** | **Description**                                                  |
+========================+==========+===============+==================================================================+
| ``acrissClass``        | string   | yes           | id of the vehicle class, /xml/vehicle\_classes                   |
+------------------------+----------+---------------+------------------------------------------------------------------+
| ``acrissType``         | string   | yes           | id of the vehicle type, /xml/vehicle\_types                      |
+------------------------+----------+---------------+------------------------------------------------------------------+
| ``acrissTransmission`` | string   | yes           | id of the vehicle transmission type, /xml/vehicle\_transmissions |
+------------------------+----------+---------------+------------------------------------------------------------------+
| ``acrissFuelAC``       | string   | yes           | id of the vehicle fuel type, /xml/vehicle\_fuelAC                |
+------------------------+----------+---------------+------------------------------------------------------------------+

Child items: no.

VehicleImage item
-----------------

Vehicle image.

- Not Mandatory item.
- Attributes: url of the vehicle image.
- Child items: no.

iehicleInformation tem V
------------------------

Addtitional information about of the vehicle.

- Not Mandatory item.

Attributes:

+------------------+------------------+---------------+----------------------------------+
| **Attribute**    | **Type**         | **Mandatory** | **Description**                  |
+==================+==================+===============+==================================+
| ``doors``        | numeric          | no            | number of vehicle                |
+------------------+------------------+---------------+----------------------------------+
| ``auto``         | numeric (0 or 1) | no            | Vehicle type transmission        |
+------------------+------------------+---------------+----------------------------------+
| ``ac``           | numeric (0 or 1) | no            | availability of air conditioning |
+------------------+------------------+---------------+----------------------------------+
| ``luggagelarge`` | numeric (0 or 1) | no            | large luggage                    |
+------------------+------------------+---------------+----------------------------------+

Child items: no.

SpecialOffer item
'''''''''''''''''

company servce.

- Not Mandatory item.
- Attributes: id special offer
- Child items: no.

item VehicleInsurancePolicy
'''''''''''''''''''''''''''

Insurance policy.

- НеMandatory item.

Attributes:

+--------------------+----------+---------------+----------------------------+
| **Attribute**      | **Type** | **Mandatory** | **Description**            |
+====================+==========+===============+============================+
| ``id``             | numeric  | yes           | id of the insurance policy |
+--------------------+----------+---------------+----------------------------+
| ``name``           | string   | yes           | insurance policy name      |
+--------------------+----------+---------------+----------------------------+
| ``price``          | numeric  | yes           | price                      |
+--------------------+----------+---------------+----------------------------+
| ``currency``       | string   | yes           | currency                   |
+--------------------+----------+---------------+----------------------------+
| ``comparePrice``   | numeric  | no            | price (RUB)                |
+--------------------+----------+---------------+----------------------------+
| ``currencyTarget`` | string   | no            | (RUB)                      |
+--------------------+----------+---------------+----------------------------+

 Child items: no.

item SearchId
-------------

In case, when vehicle searching is asynchronously (whith parameter
?async=1), then item will be contain id of innitialized search. Then
this response will come immediately and at the Hotelbook side search
will be processed as background task. Found vehicles can be asked
periodically by request
``/xml/Vehicle_search_async?login=&search_id=&from_result_id=`` (every second, for example). For details see `vehicle-search-async.html <vehicle-search-async.html>`_
 НеMandatory item. Может отсутствовать, если возникли errorки.