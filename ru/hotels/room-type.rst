Типы номеров
################

Описание XML схемы запроса типов номеров
==========================================

Запрос на получение списка типов номеров формируется через URL (методом GET)

XSD-схема ответа :

- :download:`www/xsd/dict/room/RoomTypesResponse.xsd <../../themes/hotelbook/static/xsd/dict/room/RoomTypesResponse.xsd>`

Запрос списка типов номеров
-----------------------------

Запрос без параметров, передаётся через URL вместе с учётными данными (``login``, ``password``, ``checksum``,..).

Запрос формируется по пути: ``/xml/room_type``

Ответ на запрос списка типов номеров, RoomTypesResponse
-----------------------------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <RoomTypes>
            <RoomType id="..." name="...">...</RoomType> - список типов номеров
        </RoomTypes>
    </Response>

Элемент Response
----------------

Корневой элемент.

**Атрибуты:** нет.

**Дочерний элемент:**

+---------------+--------------+------------------------------+
| Имя           | Обязательный | Описание                     |
+===============+==============+==============================+
| RoomTypes     | Да           | Список типов номеров отеля   |
+---------------+--------------+------------------------------+

Элемент RoomTypes
---------------------

Содержит список всех найденных типов номеров отеля.

**Атрибуты:** нет.

**Дочерний элемент:**

+----------+--------------+-----------------------------------------------------------------------------+
| Имя      | Обязательный | Описание                                                                    |
+==========+==============+=============================================================================+
| RoomType | Нет          | Название типа номера                                                        |
+----------+--------------+-----------------------------------------------------------------------------+

Элемент RoomType
---------------------

**Атрибуты:**

+------------+-----------+----------------------+------------------------------+
| Имя        | Тип		 |  Обязательный        | Описание                     |
+============+===========+======================+==============================+
| id         | Число     |  Да                  | Идентификатор                |
+------------+-----------+----------------------+------------------------------+
| name       | Строка    |  Да                  | название типа                |
+------------+-----------+----------------------+------------------------------+