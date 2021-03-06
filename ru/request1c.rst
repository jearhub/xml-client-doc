Запрос на выставление счета
###########################

Описание XML схемы
==================

Запрос на выставление счета формируется через URL (методом GET)

XSD-схема ответа: :download:`www/xsd/Request1CResponse.xsd <../themes/hotelbook/static/xsd/Request1CResponse.xsd>`

Запрос на выставление счета
---------------------------

Запрос с одним параметром ``order_id`` (id заказа). Он передаётся через
URL вместе с учётными данными (``login``, ``password``, ``checksum``,..).

Запрос формируется по пути: ``/xml/request_1c?order_id=``

Ответ на запрос, Request1CResponse
----------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Success>true</Success>
    </Response>

В случае успеха запрос вернет один элемент ``Success``. Иначе - ошибки в ``Errors``. 

После выставления счета в заказе, информация о счете станет доступна в запросе ``OrderInfo`` (элемент ``Account_1C``).

Элемент Errors
--------------

Смотри страницу :doc:`Ошибки <../errors>`