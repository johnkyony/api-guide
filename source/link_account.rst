Linking a User Account
======================

In some cases a user might already have a user account. I  this case you can request that they link their TradeSafe
account. This is a two step process.

Request Auth Token
------------------

You first need to generate an auth token. This is used to identify your platform an validate the request is valid.

.. code-block:: php
  :linenos:

  <?php

  // get cURL resource
  $ch = curl_init();

  // set url
  curl_setopt($ch, CURLOPT_URL, 'https://sandbox.tradesafe.co.za/api/authorize/token');

  // set method
  curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'GET');

  // return the transfer as a string
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

  // set headers
  curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...',
  ]);

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

You will get a response with the token, created time and expiry time. If the token expires before the user links their
account a new token will be required.

.. code-block:: json
  :linenos:

  {
    "token": "6855476e6f64b280b5f8be63f58f422cdd22072faa89710ddd3f623721944223",
    "created": 1559296474,
    "expire": 1559300074
  }

Create Authorization Request
----------------------------

Once you have the token it can be used to create a form request to /api/authorize

.. code-block:: html
  :linenos:

  <form action="https://sandbox.tradesafe.co.za/api/authorize" method="post" target="_blank">
      <input type="hidden" name="auth_key" value="39abf0e5-8468-4989-ae98-470a76e0b4a3">
      <input type="hidden" name="auth_token" value="6855476e6f64b280b5f8be63f58f422cdd22072faa89710ddd3f623721944223">
      <input type="hidden" name="success_url" value="https://example.com/success">
      <input type="hidden" name="failure_url" value="https://example.com/failure">
      <input type="hidden" name="parameters[name1]" value="value1">
      <input type="hidden" name="parameters[name2]" value="value2">
      <input type="submit" value="Link Your TradeSafe Account">
  </form>

auth_key
    This is your user_id

auth_token
    This is the token generated using /api/authorize/token

success_url
    Where should the user be redirected if successful

failure_url
    Where should the user be redirected if they cancel

parameters[name]
    You can define several parameters that will be sent to you along with the user_id in a callback. For example the
    username or ID od the current user account.

If the user successfully authorizes the request a callback will be sent to the URL defined in your account along with
any parameters you defined.