======
Stripe
======

`Stripe <https://stripe.com/>`_ is a United States-based online payment solution provider, allowing
businesses to accept **credit cards** and other payment methods.

Configuration
=============

.. seealso::
   - :ref:`payment_acquirers/add_new`

Credentials tab
---------------

The method to acquire your credentials depends on your hosting type:

- On Odoo Online, please follow the onboarding.
- On Odoo.sh and On-premise, extra steps are required.

Odoo Online
~~~~~~~~~~~

#. Go to the **eCommerce** or the **Sales** app and click on the *Activate Stripe* or the *Set
   payments* button on the onboarding banner.
#. Fill in the requested information and submit the form.
#. Confirm your email address when Stripe sends you a confirmation email.
#. At the end of the process, you are redirected to Odoo. If you submitted all the requested
   information, you are all set and your payment acquirer is enabled.

.. tip::
   To connect your Stripe account after the onboarding is already completed, go to
   :menuselection:`Accounting --> Configuration --> Payment Acquirers --> Stripe` and click on the
   *Connect Stripe* button.

.. tip::
   To use your own :ref:`API keys <stripe/api_keys>`, :ref:`activate the Developer mode
   <developer-mode>` and :ref:`enable Stripe manually <payment_acquirers/add_new>`.

Odoo.sh or On-premise
~~~~~~~~~~~~~~~~~~~~~

#. Go to the **eCommerce** or the **Sales** app and click on the *Activate Stripe* or the *Set
   payments* button on the onboarding banner.
#. Fill in the requested information and submit the form.
#. Confirm your email address when Stripe sends you a confirmation email.
#. At the end of the process, you are redirected to the payment acquirer **Stripe** on Odoo.
#. :ref:`Fill in your credentials <stripe/api_keys>` and :ref:`generate a webhook <stripe/webhook>`.
   Then, enable the payment acquirer.

.. tip::
   To connect your Stripe account after the onboarding is already completed, go to
   :menuselection:`Accounting --> Configuration --> Payment Acquirers --> Stripe` and click on the
   *Connect Stripe* button.

.. important::
   If you are testing Stripe (in **test mode**), change the **State** to *Test Mode*. We recommend
   doing this on a test Odoo database rather than on your main database.

.. _stripe/api_keys:

Publishable and Secret keys
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Odoo needs your **API Credentials** to connect with your Stripe account, which comprises:

- :ref:`Publishable Key <stripe/api_keys>`: The key solely used to identify the account with Stripe.
- :ref:`Secret Key <stripe/api_keys>`: The key to sign the merchant account with Stripe.
- :ref:`Webhook Signing Secret <stripe/webhook>`: When you enable your webhook on your Stripe
  account, this signing secret must be set to authenticate the messages sent from Stripe to Odoo.

To retrieve the publishable and secret keys, follow this `link to your API keys
<https://dashboard.stripe.com/account/apikeys>`_, or log into your Stripe dashboard and go to
:menuselection:`Developers --> API Keys --> Standard Keys`.

.. _stripe/webhook:

Webhook Signing Secret
~~~~~~~~~~~~~~~~~~~~~~

To retrieve the webhook signing secret, create a webhook either automatically or manually.

Create the webhook automatically
********************************

Make sure your :ref:`Publishable and Secret keys <stripe/api_keys>` are filled in, then click on the
*Generate your Webhook* button.

Create the webhook manually
***************************

Visit the `webhooks page on Stripe <https://dashboard.stripe.com/webhooks>`_, or log into your
Stripe dashboard and go to :menuselection:`Developers --> Webhooks`. Then, click on **Add endpoint**
in your **Hosted endpoints** and insert the following data into the pop-up form:

- | In the **Endpoint URL**, enter your Odoo database's URL followed by `/payment/stripe/webhook`.
  | For example: `https://yourcompany.odoo.com/payment/stripe/webhook`
- At the end of the form, you can **Select events** to listen to. Click on it and, in the
  **Checkout** section, select **checkout.session.completed**.

.. note::
   It is possible to select other events, but they are currently not processed by Odoo.

When you click on **Add endpoint**, your Webhook is configured. You can then click on **reveal** to
display your signing secret.

.. _stripe/local-payment-methods:

Enable local payment methods
----------------------------

Local payment methods are payment methods that are only available for certain merchants and
customers countries and currencies.

Odoo supports the following local payment methods:

- Bancontact
- EPS
- giropay
- iDEAL
- Przelewy24 (P24)

To enable specific local payment methods with Stripe, list them as supported payment icons. To do
so, go to :menuselection:`Payment Acquirers --> Stripe --> Configuration` and add the desired
payment methods in the **Supported Payment Icons** field. If the desired payment method is already
listed, you don't have anything to do. If a payment icon record doesn't exist in the database, its
related payment method is considered enabled with Stripe.

.. image:: media/stripe_enable_local_payment_method.png
   :align: center
   :alt: Select and add icons of the payment methods you want to enable

.. seealso::
   - :doc:`../payment_acquirers`
