Creating a User
===============

The technical specifications can be viewed on our
`API docs <https://api.tradesafe.co.za/#users-create-user-post>`_.

.. warning::
  You are responsible for providing the correct information.

When creating a contract you need a user_id to identify the user. This can be done by either creating an account for
the user or allowing then you link their existing TradeSafe Account.

The example below will create a user in response you will receive a *user_id* that you can associate with the user
account on your system. This action only needs to be done once and the *user_id* can be user for all subsequent
transactions. A user can then manage their details from their TradeSafe account.

.. code-block:: php
  :linenos:

  <?php

  // get cURL resource
  $ch = curl_init();

  // set url
  curl_setopt($ch, CURLOPT_URL, 'https://local.platform.tradesafe.dev/api/user');

  // set method
  curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'POST');

  // return the transfer as a string
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

  // set headers
  curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...',
    'Content-Type: application/json; charset=utf-8',
  ]);

  // json body
  $json_array = [
    'id_number' => '8208014477088',
    'mobile_country' => 'ZA',
    'mobile' => '084 116 7762',
    'first_name' => 'Joe'
    'last_name' => 'Somebody',
    'email' => 'joe.sombody@example.com',
    'bank_account' => [
      'number' => '1234567890',
      'bank' => '123456',
      'type' => 'CHEQUE',
      'branch_code' => '123456'
    ],
    'company' => [
      'name' => 'Company Name',
      'reg_number' => '123/456/789',
      'type' => 'Company Type'
    ],
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
