Список аэропортов
#################

Описание XML схемы получения списка аэропортов
==============================================

Запрос на получение списка аэропортов формируется через URL (методом GET)

XSD-схема ответа :

:download:`www/xsd/dict/geo/AirportsResponse.xsd <../../themes/hotelbook/static/xsd/dict/geo/AirportsResponse.xsd>`

Запрос списка аэропортов
------------------------

В запросе можно передать параметры ``?country_id=id_страны``, или
``?resort_id=id_курорта``, или ``?city_id=id_города``, чтобы получить
список аэропортов только одной(одного) страны/курорта/города. Сейчас
запрос передаётся через URL вместе с учётными данными (``login``,
``password``, ``checksum``,..).

Запрос формируется по пути: ``/xml/airports``

Ответ на запрос списка аэропортов, AirportsResponse
---------------------------------------------------

::

    <?xml version="1.0" encoding="utf-8"?>
    <Response>
        <Airports>
            <Airport id="..." iata="..." country="..." resort="..." city="..." name_ru="..." gta="...">...</Airport> - список всех найденных аэропортов
        </Airports>
    </Response>

Элемент Response
----------------

Корневой элемент.

**Атрибуты:** нет.

**Дочерний элемент:**

+------------+----------------+---------------------+
| Имя        | Обязательный   | Описание            |
+============+================+=====================+
| Airports   | Да             | Список аэропортов   |
+------------+----------------+---------------------+

Элемент Airports
----------------

Содержит список всех найденных аэропортов.

**Атрибуты:** нет.

**Дочерний элемент:**

+-----------+----------------+----------------------+
| Имя       | Обязательный   | Описание             |
+===========+================+======================+
| Airport   | Нет            | Название аэропорта   |
+-----------+----------------+----------------------+

Элемент Airport
---------------

Содержит название аэропорта латинскими буквами (на английском,
французком, немецком, итальянском и т.д.).

Необязательный элемент (отсутствует, если ни одного аэропорта не
найдено).

**Атрибуты:**

+---------+--------+--------------+---------------------------------------------------+
| Имя     | Тип    | Обязательный | Описание                                          |
+=========+========+==============+===================================================+
| id      | Число  | Да           | id найденного аэропорта                           |
+---------+--------+--------------+---------------------------------------------------+
| iata    | Строка | Да           | iata-код найденного аэропорта                     |
+---------+--------+--------------+---------------------------------------------------+
| gta     | Число  | Да           | Имеет ли этот аэропорт связь с поставщиком GTA    |
+---------+--------+--------------+---------------------------------------------------+
| country | Число  | Да           | id страны, где находится аэропорт                 |
+---------+--------+--------------+---------------------------------------------------+
| resort  | Число  | Да           | id курорта                                        |
+---------+--------+--------------+---------------------------------------------------+
| city    | Число  | Да           | id города                                         |
+---------+--------+--------------+---------------------------------------------------+
| name_ru | Строка | Да           | Название аэропорта на русском (может быть пустым) |
+---------+--------+--------------+---------------------------------------------------+

**Дочерние элементы:** нет.