Cancellation
############

Description of XML schema
=========================

A request is formed through URL (using GET method)

XSD-schema response :

-  ``www/xsd/CancellationOrderResponse.xsd``

Request
-------

Mandatory parameters:

-  ``order_id`` – order id
-  ``item_id`` – id order item(hotel), which to be cancelled

Request is passed via the URL with credentials(``login``, ``password``, ``checksum``,..).

Request path: ``/xml/cancellation_order``.

If the item can be cancelled, then it will be delivered in the queue
for cancellation (status «Pending cancellation»). It means, that
cancellation will not be sent to work. To send the cancellation to work
you should request /xml/confirm_order?order_id=..., where order_id -
order id to be cancelled.

.. note:: **Note:** You shouldn't confirm_order request after
cancellation\_order request in case of the order item haven't been sent
ro work. You can check it by order item's state in cancellation_order
response - it will be "Cancelled"

Response, CancellationOrderResponse
-----------------------------------

Response pattern is the same as in response to a request for information
about order (``OrderInfoResponse``).
And now you only need to check item status from response.