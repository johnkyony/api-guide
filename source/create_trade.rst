Creating a Trade
================

The technical specifications can be viewed on our
`API docs <https://api.tradesafe.co.za/#contract-post>`_.

.. warning::
  You are resposible for providing the correct information.

PHP Example
-----------

.. code-block:: php
  :linenos:

  <?php
  # The JWT for your account
  $json_token = 'your_jwt_token';

  # The url of the API
  $service_url = 'https://sandbox.tradesafe.co.za/api/contract.json';

  $curl = curl_init($service_url);

  $postfields = array(
    "name" => "Short description of trade",
    "reference" => "A unique identifier",
    "industry" => "GENERAL_GOODS_SERVICES",
    "description" => "Description of the trade",
    "buyer" => array(
      "first_name" => "John",
      "email" => "user@example.net",
      "mobile_country" => "ZA",
      "mobile" => "0123456789",
      "id_number" => "0000001111223"
    ),
    "seller" => array(
      "first_name" => "Jane",
      "email" => "user@example.com",
      "mobile_country" => "ZA",
      "mobile" => "0123456789",
      "id_number" => "0000001111223"
    ),
    "value" => 10000,
    "fee_allocation" => 10,
    "completion_days" => 30,
    "completion_months" => 12,
    "completion_years" => 5,
    "inspection_days" => 7,
    "delivery_required" => false,
    "seller_bank_account": {
      "number": "0123456789",
      "branch_code": "123456",
      "type": "Cheque"
    }
  );

  curl_setopt_array($curl, array(
    CURLOPT_POST => TRUE,
    CURLOPT_RETURNTRANSFER => TRUE,
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer ' . $json_token,
      'Content-Type: application/json'
    ),
    CURLOPT_POSTFIELDS => json_encode($postfields)
  ));

  $curl_response = curl_exec($curl);
  curl_close($curl);

  $response = json_decode($curl_response);

  print_r($response);
  ?>

The Payment URL
---------------

When you create a trade a summary of the information you posted will be sent
back to you along with a **payment_url**
[/api/contracts/deposit/YOUR-TRADE-ID]. This link can be embeded into your
website through an iframe and will allow users to access to our banking details
for EFT payment.

Also included is a **withdraw_url** [/api/contracts/deposit/YOUR-TRADE-ID].
This allows sellers to add their own banking details to a trade.

.. warning::
  The **withdraw_url** been depricated in favor of reciving the banking details
  during the create trade process.
