Receiving a Callback
====================

All callbacks include the following data. When receiving a callback you must
return a
`200 response <https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#200>`_
code, TradeSafe will continue retry the callback until a
200 response code is received or the timeout condition it met.

Example of the callback data
----------------------------

.. code-block:: json
  :linenos:

  {
   "id":"5899715f-bda4-4c91-b78c-033aac102991",
   "transaction_id":"123456",
   "buyer_id":"1",
   "seller_id":"2",
   "owner_id":"2",
   "litigation_initiator_id":"0",
   "negotiation_id":null,
   "step":"FUNDS_RECEIVED",
   "sent_started":null,
   "industry":"GENERAL_GOODS_SERVICES",
   "meta":{
      "reference":"my_reference"
   },
   "name":"Trade Name",
   "description":"Trade Description",
   "fee_allocation":"1",
   "value":"10000.00",
   "value_total":"0.00",
   "renegotiated_value":null,
   "buyer_cost":"0.00",
   "seller_cost":"0.00",
   "admin_cost":null,
   "completion_total_days":"0",
   "completion_days":"5",
   "completion_months":"0",
   "completion_years":"0",
   "inspection_days":"5",
   "counterparty_email":"",
   "tracking_number":null,
   "courier":null,
   "delivery_required":false,
   "delivery_type":"not_required",
   "delivery_address":null,
   "delivery_start_date":null,
   "delivery_street":null,
   "delivery_extra":null,
   "delivery_suburb":null,
   "delivery_city":null,
   "delivery_country":null,
   "delivery_zip":null,
   "delivery_comment":null,
   "review":false,
   "amendment":false,
   "updated":"2016-06-04 14:52:00",
   "created":"2016-06-04 07:03:59"
  }
