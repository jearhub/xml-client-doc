Выгрузка авто (асинхронная)
###########################

Описание XML схем поиска авто
=============================

XSD-схемы поиска авто:

:download:`www/xsd/vehicle/VehicleSearchResponse.xsd <../../themes/hotelbook/static/xsd/vehicle/VehicleSearchResponse.xsd>`

Запрос на выгрузку найденных авто
---------------------------------

Данный запрос не требует передачи XML сообщения, нужно лишь указать
параметр GET-методом.

Обязательные параметры:

-  ``login`` - логин
-  ``search_id`` - id инициализированного поиска (предварительным вызовом ``/xml/vehicle_search?async=1``)
-  ``from_result_id`` - с какого result\_id должны быть выгружены авто Остальных параметров данный запрос не требует.

Ответ на поиск авто, VehicleSearchResponse
------------------------------------------

XML-схема ответа, практически аналогична обычному поиску авто через
VehicleSearch (за исключением нового аттрибута ``finalResultId``):

::

    <?xml version="1.0" encoding="utf-8"?>

    <VehicleSearchResponse>
      <VehicleSearchRequest>... исходный запрос ...</VehicleSearchRequest>
      <Errors>
        <Error code="..." description="..."> - ошибки
      </Errors>

      <VehicleSearch searchId="id" >
         <SearchPickUp  
        countryId="id"
        countryName="..." 
        cityid="id"
        cityName="..." />
        [airportid="id"] 
        [airportName="..."] /> - получение
         <SearchDropOff  
        countryId="id"
        countryName="..." 
        cityid="id"
        cityName="..." />
        [airportid="id"] 
        [airportName="..."] /> - возврат
      </VehicleSearch >
            
      <Vehicles [finalResultId=".."] -- resultId последнего найденного авто >
        <Vehicle
        resultId="id"
        vehicleName="..." 
        [providerId="id"] -- поля может не быть, в зависимости от настроек пользователя
        confirmation="onRequest|online|inaccessible"  -- вид подтверждения    
        specialOffer="id"  -- спецпредложение    
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

Обратите внимание, что ответ может содержать ``finalResultId``.
Вернее, он будет его содержать, как только поиск авто будет полностью
завершен на стороне Хотелбука.

В этом случае, как только вы получите авто с ``resultId`` =
``finalResultId`` вам не нужно повторно отправлять запрос
``/xml/vehicle_search_async`` на получение авто. Если же авто с
``resultId`` = ``finalResultId`` ещё не выгружен, или отсутствует
аттрибут ``finalResultId`` вам нужно периодически (например раз в
секунду) запрашивать авто этим же способом, но с указанием
``from_result_id`` = resultId последнего выгруженного авто.
