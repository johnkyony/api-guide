Validate a Trade
================

The technical specifications can be viewed on our
`API docs <https://api.tradesafe.co.za/#contract-post>`_.

.. warning::
  You are responsible for providing the correct information.

Before creating a contract you can use the validate endpoint to ensure that the data is correct. On a successful
validation the API will return a 200 status code along with the data you posted.

PHP Example
-----------

.. code-block:: php
  :linenos:

  <?php

  // get cURL resource
  $ch = curl_init();

  // set url
  curl_setopt($ch, CURLOPT_URL, 'https://sandbox.tradesafe.co.za/api/validate/contract');

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
