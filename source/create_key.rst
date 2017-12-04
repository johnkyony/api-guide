Creating your API Key
=====================

Once you have received notice that the API has been enabled, login and goto
**My Account**.

.. image:: static/user_links.png

On your account settings page you will now see a new section called
**API Access**.

.. image:: static/api_access.png

Fill in both the website url and :doc:`callback </callback>` url. You can use a
service like `mockbin <http://mockbin.org/>`_ for your callback url if your
don't have one yet.

Once you have saved the page a JSON Web Token (`JWT <https://jwt.io/>`_) will be
generated for you.

.. note::

  If you change the **Website URL** and new token will be generated for your
  account. You can change the callback url at any time.
