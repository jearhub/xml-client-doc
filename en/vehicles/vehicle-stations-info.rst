Additional information about the stations (pick up / drop off)
##############################################################

Description of XML schema
=========================

XSD-schemas:

:download:`www/xsd/vehicle/VehicleStationsInfoRequest.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleStationsInfoRequest.xsd>`

:download:`www/xsd/vehicle/VehicleStationsInfoResponse.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleStationsInfoResponse.xsd>`

Request, VehicleStationsInfoRequest
-----------------------------------

Request path: ``/xml/vehicle_stations_info``. A request for additional
information about the stations may be conducted only when we know the
idsof the stations;(``PickUP/DropOff->Station``).

In the single request you can specify information for only one pair of
stations (pick up / drop off).

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>
    <VehicleStationsInfoRequest>
    <ProviderId>..</ProviderId> - provider id 
      <PickUp>    
        <Date>..</Date> - pick up date
        <Hour>..</Hour> - pick up hour
        <Station>..</Station> - pick up station id
      </PickUp>
      <DropOff>    
        <Date>..</Date> - drop off date
        <Hour>..</Hour> - drop off hour
        <Station>..</Station> - drop off station id
      </DropOff>
    </VehicleStationsInfoRequest>

VehicleStationsInfoRequest Item
-------------------------------

Request

- Parent item.
- Attributes: no.

Child items ``VehicleStationsInfoRequest``:

+----------------+---------------+---------------------+-----------------+
| **Item**       | **Mandatory** | **Description**     |                 |
+================+===============+=====================+=================+
| ``ProviderId`` | yes           | provider id         |                 |
+----------------+---------------+---------------------+-----------------+
| ``PickUp``     | yes           | pick up parameters  |                 |
+----------------+---------------+---------------------+-----------------+
| ``DropOff``    | yes           | drop off parameters |                 |
+----------------+---------------+---------------------+-----------------+
|                | **Item**      | **Mandatory**       | **Description** |
+----------------+---------------+---------------------+-----------------+
|                | ``Date``      | yes                 | date (YY-mm-dd) |
+----------------+---------------+---------------------+-----------------+
|                | ``Hour``      | yes                 | hour (HH:ii)    |
+----------------+---------------+---------------------+-----------------+
|                | ``Station``   | yes                 | station id      |
+----------------+---------------+---------------------+-----------------+

ProviderId Item
---------------

Provider id.
- Mandatory Item.
- Attributes: no.
- Child items: no.

Item PickUp
^^^^^^^^^^^

Pick up parameters.

- Mandatory Item.
- Attributes: no.

Child items:

+-------------+---------------+-----------------+
| **Item**    | **Mandatory** | **Description** |
+=============+===============+=================+
| ``Date``    | yes           | date            |
+-------------+---------------+-----------------+
| ``Hour``    | yes           | hour            |
+-------------+---------------+-----------------+
| ``Station`` | yes           | station id      |
+-------------+---------------+-----------------+

Item DropOff
^^^^^^^^^^^^

Drop off parameters.

- Mandatory Item.
- Attributes: no.
- Child items: like PickUp

Response, VehicleStationsInfoResponse
-------------------------------------

XML-schema:

::

    <?xml version="1.0" encoding="utf-8"?>
    <VehicleStationsInfoResponse>
      <VehicleStationsInfoRequest>... source request ...</VehicleStationsInfoRequest>
      [<Errors>
        <Error code="..." description="..."> - ошибки
      </Errors>]
      <PickUp>   
          <Stationid=".." >
            <Name>..</Name>
                <Address>..</Address>
                <Phone>..</Phone>
                <Fax>..</Fax>
                <OpenningHours>..</OpenningHours>
                <HotelDelivery>..</HotelDelivery> -- hotel delivery
                <OffAirport>..</OffAirport> -- support airport 
              </Station>
      </PickUp>
      <DropOff>      
          <Station id=".." >
            <Name>..</Name>
                <Address>..</Address>
                <Phone>..</Phone>
                <Fax>..</Fax>
                <OpenningHours>..</OpenningHours>
                <HotelDelivery>..</HotelDelivery>
                <OffAirport>..</OffAirport>         
              </Station>
      </DropOff>
    </VehicleStationsInfoResponse>

VehicleStationsInfoResponse Item
--------------------------------

Response.

- Parent item Item.
- Attributeі: no.

Child items ``VehicleStationsInfoResponse``:

+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
| **Item**                       | **Mandatory** | **Description**                                         |                                              |                               |
+================================+===============+=========================================================+==============================================+===============================+
| ``VehicleStationsInfoRequest`` | no            | Source request, look above – VehicleStationsInfoRequest |                                              |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
| ``Errors``                     | no            | List of the errors                                      |                                              |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                | **Item**      | **Mandatory**                                           | **Description**                              |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                | ``Error``     | yes                                                     | Error code and description (may be more one) |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
| ``PickUp``                     | yes           | Additional information about the pick up station        |                                              |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
| ``DropOff``                    | yes           | Additional information about the drop off station       |                                              |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                | **Item**      | **Mandatory**                                           | **Description**                              |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                | ``Station``   | yes                                                     | Additional information about the vehicle     |                               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | **Item**                                                | **Mandatory**                                | **Description**               |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``Name``                                                | yes                                          | Name of the pick up station   |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``Address``                                             | yes                                          | address                       |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``Phone``                                               | no                                           | phone of te station           |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``Fax``                                                 | no                                           | fax of the station            |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``OpenningHours``                                       | no                                           | oppening hours of the station |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``HotelDelivery``                                       | no                                           | hotel delivery                |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+
|                                |               | ``OffAirport``                                          | no                                           | support of the airport        |
+--------------------------------+---------------+---------------------------------------------------------+----------------------------------------------+-------------------------------+

Item VehicleStationsInfoRequest
-------------------------------

Source request.

- Not Mandatory Item.
- Request xsd-schema description look above (``VehicleStationsInfoRequest``)

Item Errors
-----------

View :doc:`Error page <../errors>`


VehicleStationsInfo item
------------------------

Information about the stations.

- Not mandatory item.
- Attributes: no

Child Items:

+-------------+---------------+------------------+
| **Item**    | **Mandatory** | **Description**  |
+=============+===============+==================+
| ``PickUp``  | yes           | Pick up station  |
+-------------+---------------+------------------+
| ``DropOff`` | yes           | Drop off station |
+-------------+---------------+------------------+

Item PickUp
-----------

Pick up station.

- Mandatory Item.
- Attributes: no.

Child items ``Station``:

+-------------+-------------------+---------------------------------------+---------------------+
| **Item**    | **Mandatory**     | **Description**                       |                     |
+=============+===================+=======================================+=====================+
| ``Station`` | yes               | Additional information of the station |                     |
+-------------+-------------------+---------------------------------------+---------------------+
|             | **Item**          | **Mandatory**                         | **Description**     |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``Name``          | yes                                   | Name of the station |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``Address``       | yes                                   | Address             |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``Phone``         | no                                    | phone               |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``Fax``           | no                                    | fax                 |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``OpenningHours`` | no                                    | openning hours      |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``HotelDelivery`` | no                                    | hotel delivery      |
+-------------+-------------------+---------------------------------------+---------------------+
|             | ``OffAirport``    | no                                    | support airport     |
+-------------+-------------------+---------------------------------------+---------------------+

Item DropOff
------------

Drop off station.

- Mandatory Item.
- Attributes: no.

Child items ``Station``:

+-------------+-------------------+------------------------------------------+---------------------+
| **Item**    | **Mandatory**     | **Description**                          |                     |
+=============+===================+==========================================+=====================+
| ``Station`` | yes               | Additional information about the station |                     |
+-------------+-------------------+------------------------------------------+---------------------+
|             | **Item**          | **Mandatory**                            | **Description**     |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``Name``          | yes                                      | Name of the station |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``Address``       | yes                                      | address             |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``Phone``         | no                                       | phone               |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``Fax``           | no                                       | fax                 |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``OpenningHours`` | no                                       | openning hours      |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``HotelDelivery`` | no                                       | hotel delivery      |
+-------------+-------------------+------------------------------------------+---------------------+
|             | ``OffAirport``    | no                                       | support airport     |
+-------------+-------------------+------------------------------------------+---------------------+

Item Station
------------

Information about the Station.

- Mandatory Item.
- Attributes: id of the station.

Child items:

+-------------------+---------------+---------------------+
| **Item**          | **Mandatory** | **Description**     |
+===================+===============+=====================+
| ``Name``          | yes           | name of the station |
+-------------------+---------------+---------------------+
| ``Address``       | yes           | address             |
+-------------------+---------------+---------------------+
| ``Phone``         | no            | phone               |
+-------------------+---------------+---------------------+
| ``Fax``           | no            | fax                 |
+-------------------+---------------+---------------------+
| ``OpenningHours`` | no            | Openning hours      |
+-------------------+---------------+---------------------+
| ``HotelDelivery`` | no            | hotel delivery      |
+-------------------+---------------+---------------------+
| ``OffAirport``    | no            | support airport     |
+-------------------+---------------+---------------------+