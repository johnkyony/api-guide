Retrieve Trade Information
==========================

The technical specifications can be viewed on our
`API docs <https://api.tradesafe.co.za/#contract-get>`_.

PHP Example
-----------

.. code-block:: php

  <?php
  # The JWT for your account
  $json_token = 'your_jwt_token';

  # The url of the API
  $service_url = 'https://sandbox.tradesafe.co.za/api/contract/{ID_OF_THE_TRADE}.json';

  $curl = curl_init($service_url);

  curl_setopt_array($curl, array(
    CURLOPT_HTTPHEADER => array(
      'Authorization: Bearer ' . $json_token,
      'Content-Type: application/json'
    )
  ));

  $curl_response = curl_exec($curl);
  curl_close($curl);

  $response = json_decode($curl_response);

  print_r($response);
  ?>

This allows you to query any trade you have created at any time, the data is
similar to what you receive when creating a trade.

This can be useful for recovering from an outage for example. We recommend that
you cache this data and only make requests when necessary. As the callback will
send through data every time the trade is transitioned to a new step.
