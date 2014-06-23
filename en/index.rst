.. XML Client API documentation master file, created by
   sphinx-quickstart on Mon May  5 12:59:02 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
  
XML API HotelBook.ru
####################

Protocol
========

Used communication protocol based on XML for querying and HTTP to pass the basic parameters. Reasons: HTTP need to simplify what can be simple - to provide simple information. XML need to be able to pass complex structures as parameters input / output. For sending xml-request need to use  POST method parameter "request".

| Life XML Server URL : http://www.hotelbook.ru/xml
| Test XML Server URL: http://www.test.hotelbook.vsespo.ru/xml
| XSD schema: http://www.hotelbook.ru/xsd

 

| Test web-interface http://test.hotelbook.vsespo.ru/xml-test.php?language=en with test data. You can search and book hotels.
| Web-interface http://www.hotelbook.ru/xml-test.php?language=en with live data.


Authorization
=============

Authorization parameters in the URL: login, time, checksum.

- login – user login
- time – unix timestamp (number of seconds from 01.01.1970, use UTC time.
- checksum = md5($password_hash.$time). $password_hash = md5(‘real_password’)

Server also checks that the time is within 60 seconds from the time server, so the time difference may be the cause of the authorization process fails. Current server time can be checked against the address /xml/time or /xml/unix_time
To access /xml/time and /xml/unix_time authorization is not required and you can check it right now http://hotelbook.ru/xml/time

Language
========

| For the English version you must specify parameters language=”en” and currency – USD or EUR.
| For example, your request path like http://www.hotelbook.ru/xml/hotel_search?language=en&currency=usd

Static data
===========

| For get countries, hotels, cities data and the types / views / sizes of rooms, meal types, locations, rather a simple HTTP request.
| Response format is not currently described.

List of dictionaries:

+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| Address                                               | Description                                                   | Additional                           |
+=======================================================+===============================================================+======================================+
| /xml/time                                             | Time server in the format “Y-m-d H:i:s”                       | without authorization                |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/unix_time                                        | Unix time (number of seconds) in the plain (simple text)      | without authorization                |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/countries                                        | All countries                                                 |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/resorts                                          | Resorts                                                       | Optional parameter                   |
|                                                       |                                                               | ?country_id=id will limit            |
|                                                       |                                                               | resorts list with specified country  |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/cities                                           | Cities                                                        | Optional parameters ?country_id=id,  |
|                                                       |                                                               | ?resort_id=id will limit cities list |
|                                                       |                                                               | with specified country/resort        |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/location                                         | Hotel locations. If is_global=1, then                         |                                      |
|                                                       | the location is applicable to all cities                      |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/room_size                                        | Room sizes with id, number of possible adults, children, cots |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/room_type                                        | Rooms types with id, name                                     |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/room_view                                        | Rooms views with id, name                                     |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/meal                                             | Meal types                                                    |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/meal_breakfast                                   | Breakfast types                                               |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/hotel_cat                                        | Hotel categories. (stars)                                     |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/hotel_type                                       | Hotel types                                                   |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/hotel_facility                                   | Hotel facilities                                              |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/room_amenity                                     | Room amenities                                                |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/hotel_list                                       | Hotels list. Contain id, city id, hotel category              |                                      |
| Optional parameter ?city_id=id                        | id, last update time(unix time)                               |                                      |
|                                                       | will limit hotel list with specified city                     |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| Optional parameter ?update=date                       | will limit hotel list with hotels updated                     |                                      |
|                                                       | from specified date. Date pattern “Y-m-d H:i:s”               |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| /xml/hotel_detail                                     | Detailed information about the hotel                          | You shoul specify mandatory          |
|                                                       |                                                               | parameter hotel_name or hotel_id.    |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| ?hotel_id – hotel id                                  |                                                               |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| ?hotel_name – hotel name                              |                                                               |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+
| You can get a list of hotels by query /xml/hotel_list |                                                               |                                      |
+-------------------------------------------------------+---------------------------------------------------------------+--------------------------------------+

Every element, e.g. hotel, room, hotel facility, room amenity, city, 
resort and etc has own unique ID. In response to the request of any 
of the dictionaries in the table above, this identifier is present.

Search hotels request
---------------------

| Address - /xml/hotel_search.
| For details see HotelSearch.htm

Asynchronous search hotels request
----------------------------------

| Address - /xml/hotel_search?async=1 (parameter ?async=1).
| Request /xml/hotel_search_async?login=&search_id= returns found to date hotels.
| For details see HotelSearch.htm

Request additional search details (prices, cancellation policies)
-----------------------------------------------------------------

| Address - /xml/hotel_search_details
| For details see HotelSearchDetails.htm

Create order  (or add new hotel to the order)
---------------------------------------------

| Address - /xml/add_order
| For details see AddOrder.htm
| To send order for processing it you must confirm order

Modify order (modify existing elements)
---------------------------------------

| Address -  /xml/modify_order
| For details see ModifyOrder.htm
| To send changings for processing them you must confirm order

Confirm order (booking)
-----------------------

| Address - /xml/confirm_order
| For details see ConfirmOrder.htm

Order information
-----------------

| Address - /xml/order_info
| For details see OrderInfo.htm

Order item(hotel) information
-----------------------------

| Address - /xml/order_item_info
| For details see OrderItemInfo.htm
| Cancellation order

| Address - /xml/cancellation_order
| For details see CancellationOrder.htm

Orders list
-----------

| Address - /xml/order_list
| For details see OrderList.htm

Voucher information about order
-------------------------------

| Address - /xml/voucher_info
| For details see VoucherInfo.htm

Billing 1C
----------

| Address - /xml/request_1c
| For details see Request1C.htm

TripAdvisor ratings and reviews
-------------------------------

| Addresses: /xml/tripadvisor_get_ratings and /xml/tripadvisor_get_rating_and_reviews_by_hotel
| For details see TripAdvisorGetRatings и TripAdvisorGetRatingsAndReviews