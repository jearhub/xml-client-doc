Order confirmation
=====================================

Description of XML schema
=========================

**Contents**

`Request <#h-2>`_

`Response, ConfirmOrderResponse <#h-3>`_

 A request is formed through URL (using GET method).
 XSD-schema response:

-  ``www/xsd/ConfirmOrderResponse.xsd``

Request
-------

The request must be an parameter - order\_id, taken from the response to
the AddOrder request. Request is passed via the URL with
credentials(``login``, ``password``, ``checksum``,..).
 If in response to the confirmation order, received a notice about the
change characteristics of the order item at the provider, then to
confirm the order item, you need to add one more parameter in confirm
request ``changes_confrim=1``. Now it applies to the **vehicle** only.
Notification will be in the ``Errors`` and ``Changes``.
 Request path: ``/xml/confirm_order``

Response, ConfirmOrderResponse
------------------------------

Response pattern is the same as in response to a request for information
about order (``OrderInfoResponse``).
 And now you only need to check item status from response.
