Order confirmation
##################

Description of XML schema
=========================

A request is formed through URL (using GET method).

XSD-schema response:

-  ``www/xsd/ConfirmOrderResponse.xsd``

Request
-------

The request must be an parameter - order\_id, taken from the response to
the AddOrder request. Request is passed via the URL with
credentials(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/confirm_order``

Response, ConfirmOrderResponse
------------------------------

Response pattern is the same as in response to a request for information
about order (``OrderInfoResponse``).

And now you only need to check item status from response.