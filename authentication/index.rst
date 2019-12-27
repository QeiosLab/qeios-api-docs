Authentication
==============

Authentication to the Qeios API is made by sending a personal access token together with each API request.

What's a personal access token?
-------------------------------

An access token is a string that is related to a specific account on `Qeios <https://www.qeios.com/>`_. When you use the access token, you are automatically authenticating as a user and are able to make all the actions a user can make via API.

Obtaining an access token
-------------------------

At the moment, the only way to get an access token is by contacting Qeios directly, e.g. by sending an email to info@qeios.com.

Using an access token
---------------------

Once you've obtained your access token, you'll be able to use it to make API requests as an authenticated user.

In order to use the access token when you make a request, just specify the access token as a ``Bearer`` token in the ``Authorization`` header of your request. For example, when using the Guzzle HTTP library (in PHP):

.. code-block:: php

    $response = $client->request('GET', 'http://example.com/api/endpoint', [
        'headers' => [
            'Accept' => 'application/json',
            'Authorization' => 'Bearer ' . $accessToken,
        ],
    ]);

Notes on security
-----------------

Treat your tokens like passwords and keep them secret. When working with the API, use tokens as environment variables instead of hardcoding them into your programs.