TripAdvisor rating and reviews
##############################

TripAdviser rating and reviews receiver XML scheme description
==============================================================

A request is passed via URL (the GET method) with the basic authentication parameters (login, checksum, timestamp)

TripAdvisor rating and reviews list request
-------------------------------------------

(``login``, ``password``, ``checksum``, ...)

Request path: ``/xml/tripadvisor_hotel_reviews``

Possible parameters:

-  ``hotel_id`` - hotel id

Or:

- ``hotel_name`` - partial hotel name for LIKE search
-  ``base64`` - the widget code is base64-encoded by default to prevent parser errors, so if ``base64`` is set to ``no`` there is no base64 encoding

Response: HotelReviews
----------------------

::

        <?xml version="1.0" encoding="utf-8"?>
        <Response>
            <HotelReviews>
                <Hotel id="hotel id value" review_count="review amount value" average_rating="average rating value" rating_url="rating image url" hotel_url="hotel page url on TripAdvisor">
                    <ReviewsWidgetBody encoded="base64 or no">
                        <![CDATA[
                            Base64 or raw TripAdvisor reviews widget code
                        ]]>
                    </ReviewsWidgetBody>
                </Hotel>
                ...
            </HotelReviews>
        </Response>

Response node
-------------

Root node

**Attributes:** нет.

**Child node:**

+----------------+---------------+---------------------------------------+
| Name           | Is required   | Description                           |
+================+===============+=======================================+
| HotelReviews   | Yes           | The hotel and rating list container   |
+----------------+---------------+---------------------------------------+

HotelReviews node
-----------------

The hotel and rating list container

**Attributes:** no.

**Child node:**

+-------+-----------+--------------------------------------------------+
| Name  | Mandatory | Description                                      |
+=======+===========+==================================================+
| Hotel | No        | Hotel and rating information                     |
|       |           |                                                  |
|       |           | Attributes:                                      |
|       |           |                                                  |
|       |           | -  ``id`` - hotel id                             |
|       |           | -  ``review_count`` - review amount value        |
|       |           | -  ``average_rating`` - average rating value     |
|       |           | -  ``rating_url`` - TripAdvisor rating image url |
|       |           | -  ``hotel_url`` - TripAdvisor hotel page url    |
+-------+-----------+--------------------------------------------------+

Hotel node
----------

Contains a TripAdvisor reviews widget code

**Attributes:**

-  ``id`` - hotel id
-  ``review_count`` - review amount value
-  ``average_rating`` - average rating value
-  ``rating_url`` - TripAdvisor rating image url
-  ``hotel_url`` - TripAdvisor hotel page url

**Child node:**

+-------------------+-----------+---------------------------------------------------------------------+
| Name              | Mandatory | Description                                                         |
+===================+===========+=====================================================================+
| ReviewsWidgetBody | No        | Base64-encoded or raw CDATA-wrapped TripAdviser reviews widget code |
|                   |           |                                                                     |
|                   |           | Attributes:                                                         |
|                   |           |                                                                     |
|                   |           | -  ``encoded`` — shows if the widget code is Base64-encoded or not; |
|                   |           | possible values: ``base64`` or ``no``                               |
+-------------------+-----------+---------------------------------------------------------------------+

Possible returned errors
------------------------

There can be an error caused by non-set TripAdvisor usage permission ACL right

-  <Error>You have no ACL rights to use TripAdvisor API</Error>

