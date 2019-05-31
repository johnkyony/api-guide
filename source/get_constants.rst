Get Constants from the API
==========================

There are a number of constants that are used to create a contract ranging from industry to a list of steps and many
more. You can always get the most recent values using the *constant* endpoint.

Below is an example to retrieve a list of industries.

.. code-block:: php
  :linenos:

  <?php

  // get cURL resource
  $ch = curl_init();

  // set url
  curl_setopt($ch, CURLOPT_URL, 'https://sandbox.tradesafe.co.za/api/constant/industry-types');

  // set method
  curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'GET');

  // return the transfer as a string
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

  // set headers
  curl_setopt($ch, CURLOPT_HTTPHEADER, [
    'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...',
    'Content-Type: application/json; charset=utf-8',
  ]);

  // json body
  $json_array = [

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

Example Response:

.. code-block:: json
  :linenos:

  {
    "GENERAL_GOODS_SERVICES": "General Goods & Services",
    "AGRICULTURE_LIVESTOCK_GAME": "Agriculture, Livestock & Game",
    "ART_ANTIQUES_COLLECTIBLES": "Art, Antiques & Collectibles",
    "BUSINESS_SALE_BROKING": "Business Sale & Broking",
    "VEHICLES_WATERCRAFT": "Cars, Bikes & Watercraft",
    "CONSTRUCTION": "Construction",
    "CONTRACT_WORK_FREELANCING": "Contract Work & Freelancing",
    "FUEL": "Diesel, Petroleum & Biofuel (Local)",
    "FUEL_INTERNATIONAL": "Diesel, Petroleum & Biofuel (Cross-Border)",
    "DONATIONS_TRUSTS": "Donations & Trusts",
    "FILMS_PRODUCTION": "Films & Production",
    "HOLIDAY_LETS_DEPOSITS": "Holiday Lets & Deposits",
    "INVESTMENTS_EXITS": "Investments & Exits",
    "MINING": "Mining, Metals & Minerals",
    "LEASES_RENTAL_DEPOSITS": "Rental Deposits",
    "USED_PARTS": "Used Parts",
    "SOFTWARE_DEV_WEB_DOMAINS": "Web Domain Purchases & Transfers",
    "WEDDINGS_FUNCTIONS": "Weddings & Functions"
  }

There are several other constants available:

.. note::
  Replace *{constant-type}* in /api/constant/{constant-type} with any of the values below.

industry-types
  A list of available industries

step-types
  A list of all the steps

beneficiary-types
  A list of different types of beneficiaries

fee-allocation-types
  A list of types of fee allocations

company-types
  A list of company types

company-suffix-types
  A list of company suffixes

bank-account-types
  A list of bank account types