Выгрузка отелей (асинхронная)
#############################

Описание XML схем поиска отелей
===============================

XSD-схемы поиска отелей:

- :download:`www/xsd/hotel/HotelSearchResponse.xsd <../../themes/hotelbook/static/xsd/hotel/HotelSearchResponse.xsd>`


Запрос на выгрузку найденных отелей
-----------------------------------

Данный запрос не требует передачи XML сообщения, нужно лишь указать параметр GET-методом.

Обязательные параметры:

-  ``login`` - логин
-  ``search_id`` - id инициализированного поиска (предварительным вызовом ``/xml/hotel_search?async=1``)
-  ``from_result_id`` - с какого result_id должны быть выгружены отели

Остальных параметров данный запрос не требует.

Ответ на поиск отелей, HotelSearchResponse
------------------------------------------

XML-схема ответа, практически аналогична обычному поиску отелей через HotelSearch (за исключением нового аттрибута ``finalResultId``):

::

    <?xml version="1.0" encoding="utf-8"?>

    <HotelSearchResponse>
      <HotelSearchRequest>... исходный запрос ...</HotelSearchRequest>
      <Errors>
        <Error code="..." description="..."> - ошибки
      </Errors>

      <HotelSearch
        searchId="id"
        countryId="id" countryName=".."
        resourtId="id" resortName=".."
        cityId="id" cityName=".."/>

      <Hotels [finalResultId=..] -- resultId последнего найденного отеля>
        <Hotel
            resultId="id"
            hotelId="id"
            hotelName=".."
            hotelCatId="id"
            hotelCatName=".."
            confirmation="onRequest|online|inaccessible" -- вид подтверждения
            price="orig_price" -- цена в валюте currency
            currency=".."
            comparePrice="real_price" -- цена в рублях
            duration=".."
            information=".."
            visaMsk="true|false"
            visaSpb="true|false"
            [useNds="true|false"]
            specialOffer="true|false" - действует ли специальное предложение

            [providerId="id"] -- поля может не быть, в зависимости от настроек пользователя
        >
          <Rooms>
            <Room
              roomName="..." 

              roomNumber=".."
              mealId="id"
              mealName="..."
              mealBreakfastId="id"
              mealBreakfastName="..."
              children=".."
              cots="0|1|2"
              sharingBedding="true|false"
            >

              [<ChildAge>2..18</ChildAge>] -- если есть ребёнок, возраст
            </Room>
          </Rooms>
          [<Locations>

            <Location id=".." name="..." /> -- может быть несколько локаций, к которым относится отель
          </Locations>]
        </Hotel>

      </Hotels>
    </HotelSearchResponse>


Обратите внимание, что ответ может содержать ``finalResultId``.
Вернее, он будет его содержать, как только поиск отелей будет полностью завершен на стороне Хотелбука.

В этом случае, как только вы получите отель с ``resultId`` = ``finalResultId`` вам не нужно повторно отправлять запрос ``/xml/hotel_search_async`` на получение отелей. 

Если же отель с ``resultId`` = ``finalResultId`` ещё не выгружен, или отсутствует аттрибут ``finalResultId`` вам нужно периодически (например раз в секунду) запрашивать отели этим же способом, но с указанием ``from_result_id`` = resultId последнего выгруженного отеля.
