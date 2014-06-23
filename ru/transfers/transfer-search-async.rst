Выгрузка трансферов (асинхронная)
#################################

Описание XML схем поиска трансферов
===================================

XSD-схемы поиска трансферов:

``www/xsd/TransferSearchResponse.xsd``

Запрос на выгрузку найденных трансферов
---------------------------------------

Данный запрос не требует передачи XML сообщения, нужно лишь указать
параметр GET-методом.

Обязательные параметры:

-  ``login`` - логин
-  ``search_id`` - id инициализированного поиска (предварительным вызовом ``/xml/transfer_search?async=1``)
-  ``from_result_id`` - с какого result\_id должны быть выгружены трансферы

Остальных параметров данный запрос не требует.

Ответ на поиск трансферов, TransferSearchResponse
-------------------------------------------------

XML-схема ответа, практически аналогична обычному поиску трансферов
через TransferSearch (за исключением нового аттрибута ``finalResultId``):

::

    <?xml version="1.0" encoding="utf-8"?>

    <TransferSearchResponse>
      <TransferSearchRequest>... исходный запрос ...</TransferSearchRequest>
      <Errors>
         <Error code="..." description="..."> - ошибки
      </Errors>

      <TransferSearch searchId="id" >
        <SearchPickUp  
        countryId="id"
        countryName="..."
        resortId="id"
        resortName="..."
        cityid="id"
        cityName="..." /> - посадка
        <SearchDropOff  
        countryId="id"
        countryName="..."
        resortId="id"
        resortName="..."
        cityid="id"
        cityName="..." /> - высадка
      </TransferSearch >

      <Transfers [finalResultId=".."] -- resultId последнего найденного трансфера >
        <Transfer
        resultId="id"
        transferName="..." 
        [providerId="id"] -- поля может не быть, в зависимости от настроек пользователя
        confirmation="onRequest|online|inaccessible"  -- вид подтверждения
        price="orig_price"  -- цена в валюте currency
        currency=".."
        comparePrice=" -- цена в рублях
        [useNds="true|false"]
        passengers=".." -- максимально пассажиров
        [transferTime="true|false"] -- время трансфера
        [checkInTime="true|false"] -- время регистрации
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

Обратите внимание, что ответ может содержать ``finalResultId``.
Вернее, он будет его содержать, как только поиск трансферов будет
полностью завершен на стороне Хотелбука.

В этом случае, как только вы получите трансфер с ``resultId`` =
``finalResultId`` вам не нужно повторно отправлять запрос
``/xml/transfer_search_async`` на получение трансферов. Если же трансфер
с ``resultId`` = ``finalResultId`` ещё не выгружен, или отсутствует
аттрибут ``finalResultId`` вам нужно периодически (например раз в
секунду) запрашивать трансферы этим же способом, но с указанием
``from_result_id`` = resultId последнего выгруженного трансфера.