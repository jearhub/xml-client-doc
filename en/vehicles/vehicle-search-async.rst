Download found vehicles (asynchronously)
########################################

XML-schemas
===========

XSD-schemas:

``www/xsd/VehicleSearchResponse.xsd``

Request for downloading of found vehicles
-----------------------------------------

This request don't require XML message. Only GET-parameters.

Mandatory parameters:

-  ``login`` - user login
-  ``search_id`` - id of initialized search (by prior call of request ``/xml/vehicle_search?async=1``)
-  ``from_result_id`` - from which result\_id vehicles must be downloaded

Any other parameters are not required.

Response, VehicleSearchResponse
-------------------------------

XML-schema is almost the same as regular search request VehicleSearch
(with the exception of new attribute ``finalResultId``):

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
            
      <Vehicles [finalResultId=".."] -- result id of last found vehicle >
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


Draw your attention that the answer can contain ``finalResultId``.

Or rather it will contain this attribute when vehicle search will be completed on Hotelbook side.
In this case when you receive vehicle with ``resultId`` =
``finalResultId`` , you don't need to send request
``/xml/vehicle_search_async`` to download vehicles. If vehicle with
``resultId`` = ``finalResultId`` are not downloaded yet or attribute
``finalResultId`` is absent, you need request vehicles by this way, but
with attribute ``from_result_id`` = resultId (id of last downloaded
vehicle) - request such way periodically (for example, once per second).
