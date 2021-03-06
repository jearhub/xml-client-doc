Список заказов
##############

Описание XML схемы получения списка заказов
===========================================

XSD-схема запроса списка заказов:

:download:`www/xsd/order/OrderListRequest.xsd <../../themes/hotelbook/static/xsd/order/OrderListRequest.xsd>`

XSD-схема ответа на запрос списка заказов:

:download:`www/xsd/order/OrderListResponse.xsd <../../themes/hotelbook/static/xsd/order/OrderListResponse.xsd>`

Запрос списка заказов, OrderListRequest
---------------------------------------

Запрос формируется по пути: ``/xml/order_list``

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderListRequest>
        [<CheckInFrom>...</CheckInFrom>]
        [<CheckInTo>...</CheckInTo>]
        [<CreatedFrom>...</CreatedFrom>]
        [<CreatedTo>...</CreatedTo>]
        [<ChangedFrom>...</ChangedFrom>]
        [<ChangedTo>...</ChangedTo>]
        [<Agents>
          <Agent>...<Agent>
        </Agents>]
    </OrderListRequest>

Элемент OrderListRequest
------------------------

Корневой элемент.

**Атрибуты:** нет.

**Дочерние элементы:**

+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| Имя         | Тип                         | Обязательный | Описание                                                          |
+=============+=============================+==============+===================================================================+
| CheckInFrom | Дата в формате "YYYY-MM-DD" | Нет          | Вернуть лишь те отели, дата заезда которых по эту дату            |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| CheckInTo   | Дата в формате "YYYY-MM-DD" | Нет          | Вернуть лишь те отели, дата заезда которых с этой даты            |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| CreatedFrom | Дата в формате "YYYY-MM-DD" | Нет          | Вернуть лишь те отели, дата создания которых С этой даты          |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| CreatedTo   | Дата в формате "YYYY-MM-DD" | Нет          | Вернуть лишь те отели, дата создания которых ДО этой даты         |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| ChangedFrom | Дата в формате "YYYY-MM-DD" | Нет          | Вернуть лишь те отели, в которых произошли изменения С этой даты  |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| ChangedTo   | Дата в формате "YYYY-MM-DD" | Нет          | Вернуть лишь те отели, в которых произошли изменения ДО этой даты |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+
| Agents      | Вложенные элементы          | Нет          | Список агентов agent                                              |
+-------------+-----------------------------+--------------+-------------------------------------------------------------------+

Ответ на запрос списка заказов, OrderListResponse
-------------------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <OrderListResponse>
     [<OrderListRequest>...</OrderListRequest>] - Request for this response
     [<Errors>
        <Error code="..." description="..."> - ошибки
      </Errors>]
      <OrderList>
        <Orders agent="..."> - список заказов (может быть много)
          <Order id="..." state="..." via_xml_gate="true|false"> - список элементов заказа (может быть несколько)
            <VehicleItem id="..." state="...">          
              <Created>...</Created>
              <PickUpDate>...</PickUpDate>
              <DropOffDate>...</DropOffDate>
              <PointType>...</PointType>
              <PickUpPoint>...</PickUpPoint>
              <DropOffPoint>...</DropOffPoint>
              <PickUpStation>...</PickUpStation>
              <DropOffStation>...</DropOffStation>
              <ACRISS>...</ACRISS>
              <CompanyName>...</CompanyName>
              <Logs>
                  <Log>...</Log>
              </Logs>
            </VehicleItem>
          </Order>
        </Orders>
      </OrderList>
    </OrderListResponse>

Элемент OrderListResponse
-------------------------

Корневой элемент.

**Атрибуты:** нет.

**Дочерние элементы:**

+--------------------+---------------------------------------+----------------------------+
| Имя                | Обязательный                          | Описание                   |
+====================+=======================================+============================+
| OrderListRequest   | Нет                                   | Содержит xml запрос        |
+--------------------+---------------------------------------+----------------------------+
| Errors             | Нет                                   | Список ошибок, если есть   |
+--------------------+---------------------------------------+----------------------------+
| OrderList          | Нет (отсутствует, если есть ошибки)   | Список найденных заказов   |
+--------------------+---------------------------------------+----------------------------+

Элемент Errors
--------------

Смотри страницу :doc:`Ошибки <../errors>`

Элемент OrderList
-----------------

Список найденных заказов.

**Атрибуты:** нет.

**Дочерние элементы:**

+----------+----------------+------------------------------------------------------------------+
| Имя      | Обязательный   | Описание                                                         |
+==========+================+==================================================================+
| Orders   | Да             | Найденные заказы (элементы Order), принадлежащие одному агенту   |
+----------+----------------+------------------------------------------------------------------+

Элемент Orders
--------------

Найденные заказы, принадлежащие одному агенту.

**Атрибуты:**

+---------+----------+----------------+--------------+
| Имя     | Тип      | Обязательный   | Описание     |
+=========+==========+================+==============+
| agent   | Строка   | Да             | Имя агента   |
+---------+----------+----------------+--------------+

**Дочерние элементы:**

+---------+----------------+---------------------------+
| Имя     | Обязательный   | Описание                  |
+=========+================+===========================+
| Order   | Да             | Список элементов заказа   |
+---------+----------------+---------------------------+

Элемент Orders/Order
--------------------

Содержит cписок элементов заказа.

**Атрибуты:**

+--------------+----------------+--------------+----------------------------------------------+
| Имя          | Тип            | Обязательный | Описание                                     |
+==============+================+==============+==============================================+
| Id           | Число          | Да           | Идентификатор заказа                         |
+--------------+----------------+--------------+----------------------------------------------+
| state        | Строка         | Да           | Состояние заказа                             |
+--------------+----------------+--------------+----------------------------------------------+
| via_xml_gate | true или false | Да           | Если true, заказ был добавлен через xml-шлюз |
+--------------+----------------+--------------+----------------------------------------------+
| tag          | Стркоа         | Нет          | Референс заказа                              |
+--------------+----------------+--------------+----------------------------------------------+

 **Дочерние элементы:**

+-------------+--------------+----------------------+
| Имя         | Обязательный | Описание             |
+=============+==============+======================+
| VehicleItem | Да           | Описание авто заказа |
+-------------+--------------+----------------------+

Элемент Orders/Order/VehicleItem
--------------------------------

Описание элемента заказа.

**Атрибуты:**

+---------+--------+--------------+------------------------------+
| Имя     | Тип    | Обязательный | Описание                     |
+=========+========+==============+==============================+
| Id      | Число  | Да           | Идентификатор элемента       |
+---------+--------+--------------+------------------------------+
| state   | Строка | Да           | Состояние элемента заказа    |
+---------+--------+--------------+------------------------------+
| stateId | Число  | Нет          | id состояния элемента заказа |
+---------+--------+--------------+------------------------------+

**Дочерние элементы:**

+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| Имя            | Тип                      | Обязательный | Описание                                                               |
+================+==========================+==============+========================================================================+
| Created        | Дата                     | Да           | Дата создания                                                          |
+================+==========================+==============+========================================================================+
| PickUpDate     | Дата (YY-mm-dd)          | Да           | Дата получения авто                                                    |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| DropOffDate    | Дата (YY-mm-dd)          | Да           | Дата возврата авто                                                     |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| PointType      | Строка ( city, airport ) | Да           | Тип точки получения                                                    |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| PickUpPoint    | Число                    | Да           | id точки получения (города или аэропорта, в зависисомсти от PonitType) |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| DropOffPoint   | Число                    | Да           | id точки возврата (города или аэропорта, в зависисомсти от PonitType)  |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| PickUpStation  | Число                    | Да           | id станции получения авто                                              |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| DropOffStation | Число                    | Да           | id станции возврата авто                                               |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| ACRISS         | Строка                   | Да           | ACRISS - код авто                                                      |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| CompanyName    | Строка                   | Нет          | Название компании, обслуживающей станции                               |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+
| Logs           | Список элементов Log     | Нет          | История                                                                |
+----------------+--------------------------+--------------+------------------------------------------------------------------------+

Элемент Orders/Order/VehicleItem/Logs
-------------------------------------

История элемента заказа.

**Атрибуты:** нет

**Дочерние элементы:**

+-----+--------+--------------+------------------------------------+
| Имя | Тип    | Обязательный | Описание                           |
+=====+========+==============+====================================+
| Log | Строка | Нет          | Запись истории (описание действия) |
+-----+--------+--------------+------------------------------------+

Элемент Orders/Order/VehicleItem/Logs/Log
-----------------------------------------

Запись истории элемента заказа.

**Атрибуты:**

+------+--------------+--------------+----------------------------------------------------------------------------------------------------+
| Имя  | Тип          | Обязательный | Описание                                                                                           |
+======+==============+==============+====================================================================================================+
| date | Дата и время | Да           | Дата и время действия, описанного в этой записи истории                                            |
+------+--------------+--------------+----------------------------------------------------------------------------------------------------+
| user | Строка       | Да           | Логин пользователя, совершившего описанное действие (или system, если действие совершено системой) |
+------+--------------+--------------+----------------------------------------------------------------------------------------------------+