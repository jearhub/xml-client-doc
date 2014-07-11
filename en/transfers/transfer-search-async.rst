Download found transfers (asynchronously)
#########################################

XML-schemas
===========

XSD-schemas:

:download:`www/xsd/transfer/TransferSearchResponse.xsd <../../themes/hotelbook/static/xsd/transfer/TransferSearchResponse.xsd>`

Request for downloading of found transfers
------------------------------------------

This request don't require XML message. Only GET-parameters.

Mandatory parameters:

-  ``login`` - user login
-  ``search_id`` - id of initialized search (by prior call of request ``/xml/transfer_search?async=1``)
-  ``from_result_id`` - from which result_id transfers must be downloaded

Any other parameters are not required.

Response, TransferSearchResponse
--------------------------------

XML-schema is almost the same as regular search request TransferSearch
(with the exception of new attribute ``finalResultId``):

::

    <?xml version="1.0" encoding="utf-8"?>

    <TransferSearchResponse>
      <TransferSearchRequest>... source request ...</TransferSearchRequest>
      <Errors>
         <Error code="..." description="...">
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

      <Transfers [finalResultId=".."] -- result id of last found transfer >
        <Transfer
        resultId="id"
        transferName="..." 
        [providerId="id"] -- can be miss, depend on user rights
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

Draw your attention that the answer can contain ``finalResultId``.
Or rather it will contain this attribute when transfer search will be completed on Hotelbook side.

In this case when you receive transfer with ``resultId`` =
``finalResultId`` , you don't need to send request
``/xml/transfer_search_async`` to download transfers. If transfer with
``resultId`` = ``finalResultId`` are not downloaded yet or attribute
``finalResultId`` is absent, you need request transfers by this way, but
with attribute ``from_result_id`` = resultId (id of last downloaded
transfer) - request such way periodically (for example, once per second).