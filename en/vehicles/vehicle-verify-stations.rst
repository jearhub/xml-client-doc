Verification of the stations (pick up / drop off)
#################################################

Description of XML schema
=========================

XSD-schemas:

:download:`www/xsd/vehicle/VehicleVerifyStationsRequest.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleVerifyStationsRequest.xsd>`

:download:`www/xsd/vehicle/VehicleVerifyStationsResponse.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleVerifyStationsResponse.xsd>`

Request, VehicleVerifyStationsRequest
-------------------------------------

Request path: ``/xml/vehicle_verify_stations``. This request may be
conducted only when we know id search (searchId) and id results
(resultId) from the search and id of the
stations;(``PickUP/DropOff->Station``).

In the single request you can specify information for only one pair of
stations (pick up / drop off).
 XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>

    <VehicleVerifyStationsRequest>
      <SearchId>..</SearchId> - search d
      <ResultId>..</ResultId> - result id
      <PickUp>        
          <Station>..</Station> - pick up station id
      </PickUp>
      <DropOff>        
          <Station>..</Station> - drop off station id
      </DropOff>
    </VehicleVerifyStationsRequest>

VehicleVerifyStationsRequest
----------------------------

Request.
- Parent item.
- Atributes: no.

Child items ``VehicleVerifyStationsRequest``:

+----------------+-----------------+-----------------------+------------------------------------------+
| **Item**       | **Mandatory**   | **Description**       |                                          |
+----------------+-----------------+-----------------------+------------------------------------------+
| ``SearchId``   | yes             | search id             |
+----------------+-----------------+-----------------------+------------------------------------------+
| ``ResultId``   | yes             | result id             |
+----------------+-----------------+-----------------------+------------------------------------------+
| ``PickUp``     | yes             | pick up parameters    |
+----------------+-----------------+-----------------------+------------------------------------------+
| ``DropOff``    | yes             | drop off parameters   |
+----------------+-----------------+-----------------------+------------------------------------------+
|                | **Item**        | **Mandatory**         | **Description**                          |
+----------------+-----------------+-----------------------+------------------------------------------+
|                | ``Station``     | yes                   | id of the station (pick up / drop off)   |
+----------------+-----------------+-----------------------+------------------------------------------+

SearchId Item
-------------

Search id.

- Mandatory Item.
- Attributeы: no.
- Child items: no.

Item ResultId
-------------

Result id (from the search)

- Mandatory Item.
- Attributeы: no.
- Child items: no.

Item PickUp
^^^^^^^^^^^

Pick up parameters.

- Mandatory Item.
- Attributeы: no.
- Child items:

+---------------+-----------------+----------------------+
| **Item**      | **Mandatory**   | **Description**      |
+---------------+-----------------+----------------------+
| ``Station``   | yes             | pick up station id   |
+---------------+-----------------+----------------------+

Item DropOff
^^^^^^^^^^^^

Drop off parameters.

- Mandatory Item.
- Attributeы: no.
- Child items: like PickUp

Response, VehicleVerifyStationsResponse
---------------------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>
    <VehicleVerifyStationsResponse>
      <VehicleVerifyStationsRequest>... source request ...</VehicleVerifyStationsRequest>
      [<Errors>
        <Error code="..." description="..."> - errors
      </Errors>]
      <VehicleVerifyStations>        
          <Verify>true|false</Verify>          
              <AdditionalInfo>   
                    <Detail>      
                            <Title>..</Title>
                            <Value>..</Value>
                    </Detail>
              </AdditionalInfo>
      </VehicleVerifyStations>  
    </VehicleStationsInfoResponse>

Item VehicleStationsInfoResponse
--------------------------------

Response Parent Item.

- Attributeі: no.

Child items ``VehicleVerifyStationsResponse``:

+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
| **Item**                         | **Mandatory**      | **Description**                                           |                                                         |                                       |                 |
+==================================+====================+===========================================================+=========================================================+=======================================+=================+
| ``VehicleVerifyStationsRequest`` | no                 | Source request, look above – VehicleVerifyStationsRequest |                                                         |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
| ``Errors``                       | no                 | List of the errors                                        |                                                         |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  | **Item**           | **Mandatory**                                             | **Description**                                         |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  | ``Error``          | yes                                                       | Error description (and code) (may be more one)          |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
| ``VehicleVerifyStations``        | no                 | information about the stations verification               |                                                         |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  | **Item**           | **Mandatory**                                             | **Description**                                         |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  | ``Verify``         | yes                                                       | true, false information about the stations verification |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  | ``AdditionalInfo`` | no                                                        | Additonal information (example, hotel delivery)         |                                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  |                    | **Item**                                                  | **Mandatory**                                           | **Description**                       |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  |                    | ``Detail``                                                | no                                                      | details of the additional information |                 |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  |                    |                                                           | **Item**                                                | **Mandatory**                         | **Description** |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  |                    |                                                           | ``Title``                                               | yes                                   | parameter name  |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+
|                                  |                    |                                                           | ``Value``                                               | yes                                   | value           |
+----------------------------------+--------------------+-----------------------------------------------------------+---------------------------------------------------------+---------------------------------------+-----------------+

Item VehicleVerifyStationsRequest
---------------------------------

Source request.

- Not Mandatory Item.
- request xsd-schema description look above (``VehicleVerifyStationsRequest``)

Item Errors
-----------

View :doc:`Error page <../errors>`

Item VehicleVerifyStations
--------------------------

Information about the stations verification.

- Not mandatory item.
- Attributeы: no.

Child items:

+--------------------+---------------+--------------------------------------------------------+
| **Item**           | **Mandatory** | **Description**                                        |
+====================+===============+========================================================+
| ``Verify``         | yes           | true,false information about the stations verification |
+--------------------+---------------+--------------------------------------------------------+
| ``AdditionalInfo`` | no            | Additional information (example, hotel delivery)       |
+--------------------+---------------+--------------------------------------------------------+

Item Verify
-----------

Information about the stations verification (true \| false).
 
- Mandatory Item.
- Attributeы: no.
- Child items: no

Item AdditionalInfo
-------------------

Additional information (example, hotel delivery).

- Not Mandatory Item.
- Attributeы: no.

Child items:

+--------------+-----------------+-----------------------------------------+-------------------+
| **Item**     | **Mandatory**   | **Description**                         |                   |
+--------------+-----------------+-----------------------------------------+-------------------+
| ``Detail``   | no              | Details of the additional information   |                   |
+--------------+-----------------+-----------------------------------------+-------------------+
|              | **Item**        | **Mandatory**                           | **Description**   |
+--------------+-----------------+-----------------------------------------+-------------------+
|              | ``Title``       | yes                                     | parameter item    |
+--------------+-----------------+-----------------------------------------+-------------------+
|              | ``Value``       | yes                                     | value             |
+--------------+-----------------+-----------------------------------------+-------------------+