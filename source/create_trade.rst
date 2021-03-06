Creating a Trade
================

The technical specifications can be viewed on our
`API docs <https://api.tradesafe.co.za/#contract-post>`_.

.. warning::
  You are responsible for providing the correct information.

PHP Example
-----------

.. code-block:: php
  :linenos:

  <?php

  // get cURL resource
  $ch = curl_init();

  // set url
  curl_setopt($ch, CURLOPT_URL, 'https://sandbox.tradesafe.co.za/api/contract');

  // set method
  curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'POST');

  // return the transfer as a string
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

  // set headers
  curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIU...',
    'Content-Type: application/json; charset=utf-8',
  ]);

  // json body
  $json_array = [
    'name' => 'Contract Name',
    'description' => 'Description of the new Contract'
    'reference' => 'your_reference',
    'industry' => 'GENERAL_GOODS_SERVICES',
    'buyer' => '184c16a9-6013-4aaa-896d-2fab38adb603',
    'seller' => '9f816402-3f15-4a3d-be1a-8a16a67872e1',
    'agent' => 'a68f4d96-f94e-4a4c-8335-54f41d87b9a5',
    'beneficiary' => [
      [
        'value' => 50,
        'user_id' => '5cdbfa9d-2e40-4ca7-ae0f-1ba80ad33704',
        'type' => 'OTHER',
        'fee_type' => 0,
        'fee_allocation' => 3
      ]
    ],
    'value' => 10000,
    'agent_fee_type' => 0,
    'agent_fee' => '50',
    'agent_fee_allocation' => 0,
    'delivery_fee' => 123.45,
    'completion_days' => 30,
    'completion_months' => 12,
    'completion_years' => 5,
    'inspection_days' => 7,
    'fee_allocation' => 0,
    'delivery_required' => false,
  ];
  $body = json_encode($json_array);

  // set body
  curl_setopt($ch, CURLOPT_POST, 1);
  curl_setopt($ch, CURLOPT_POSTFIELDS, $body);

  // send the request and save response to $response
  $response = curl_exec($ch);

  // stop if fails
  if (!$response) {
    die('Error: "' . curl_error($ch) . '" - Code: ' . curl_errno($ch));
  }

  echo 'HTTP Status Code: ' . curl_getinfo($ch, CURLINFO_HTTP_CODE) . PHP_EOL;
  echo 'Response Body: ' . $response . PHP_EOL;

  // close curl resource to free up system resources
  curl_close($ch);

The Payment URL
---------------

When you create a trade a summary of the information you posted will be sent
back to you along with a **payment_url**
[/api/payment/eftsecure/YOUR-TRADE-ID]. This link can be embedded into your
website through an iframe and will allow users to access to our banking details
for EFT payment.

You wil also get a **payfast_payment_url**. This URL provides an html button formatted in JSON that you can embed on
your website.

Also included is a **withdraw_url** [/api/contracts/deposit/YOUR-TRADE-ID].
This allows sellers to add their own banking details to a trade.

.. warning::
  The **withdraw_url** been deprecated in favor of receiving the banking details
  during the create trade process.
