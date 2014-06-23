TripAdvisor rating
##################

TripAdviser rating receiver XML scheme description
==================================================

A request is passed via URL (the GET method) with the basic authentication parameters (login, checksum, timestamp)

TripAdvisor rating list request
-------------------------------

(``login``, ``password``, ``checksum``, ...)

Request path: ``/xml/tripadvisor_rating_list``

Possible parameters:

-  ``hotel_id`` - id of the hotel

Or:

-  ``hotel_name`` - partial hotel name for LIKE search
-  ``country`` - country where hotel is situated
-  ``city`` - city where hotel is situated
-  ``from`` - minimal hotel id for the filter
-  ``limit`` - maximal search result amount

Response: RatingList
--------------------

::

        <?xml version="1.0" encoding="utf-8"?>
        <Response>
            <RatingList>
                <Hotel id="hotel id value" review_count="review amount value" average_rating="average rating value" rating_url="rating image url" hotel_url="hotel page url on TripAdvisor" />
                ...
            </RatingList>
        </Response>

Response node
-------------

Root node

**Attributes:** нет.

**Child node:**

+--------------+---------------+---------------------------------------+
| Name         | Is required   | Description                           |
+==============+===============+=======================================+
| RatingList   | Yes           | The hotel and rating list container   |
+--------------+---------------+---------------------------------------+

RatingList node
---------------

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

Possible returned errors
------------------------

There can be an error caused by non-set TripAdvisor usage permission ACL right

-  <Error>You have no ACL rights to use TripAdvisor API</Error>

