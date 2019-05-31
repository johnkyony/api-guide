Validate a User
===============

The technical specifications can be viewed on our
`API docs <https://api.tradesafe.co.za/#users-create-user-post>`_.

.. warning::
  You are responsible for providing the correct information.

Before creating a user you can check the data using the verify endpoint. On a successful validation the API will
return a 200 status code along with the data you posted.

PHP Example
-----------

.. code-block:: php
  :linenos:

  <?php

  // get cURL resource
  $ch = curl_init();

  // set url
  curl_setopt($ch, CURLOPT_URL, 'https://local.platform.tradesafe.dev/api/verify/user');

  // set method
  curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'POST');

  // return the transfer as a string
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

  // set headers
  curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwczpcL1wvd3d3LnRyYWRlc2FmZS5jby56YSIsImF1ZCI6IndvcmRwcmVzcy50cmFkZXNhZmUuY28uemEiLCJpYXQiOiIxNTQ3NTUwMjA3IiwibmJmIjoiMTU0NzU1MDIwNyIsInVzZXJfaWQiOiIxIn0.eqCqj2Z83Ri9ZoPTVoh6mU6ucf5MCWZjP22sxdqHHCM',
    'Content-Type: application/json; charset=utf-8',
    'Cookie: CAKEPHP=ck6l8sggd083505a8elrtmmme6',
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
