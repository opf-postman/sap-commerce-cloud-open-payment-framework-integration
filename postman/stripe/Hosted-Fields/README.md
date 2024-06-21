## Introduction ##
The Postman Collection enables a [Stripe Payment Elements Form](https://docs.stripe.com/payments/payment-element?locale=en-GB) integration for payment processing through open payment framework(OPF). 

The integration supports:

* Authorization of  Payments using PCI SAQ-A Stripe Payments Element using the OPF "Hosted Fields" UX Pattern
* Deferred Capture support
* Refunds
* Reversals
* Reauthorization of saved payment

APMs Tested
* Klarna

## Known Issues ##
* Asynchronous refunds (pending) need to be manually acknowledged in OPF

## Setup Instructions ##

### Summary ###
In summary: to import the [Postman Collection](mapping_configuration.json) this page will guide you through the following steps: 

a) Create Your Stripe Test Account.

b) Create a Stripe payment integration in OPF workbench.

c) Set up Your Stripe Test Account to work with OPF.

d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Stripe Test Account unique values. 

### Create a Stripe Account ###
You can sign up for a free Stripe Test Account at https://dashboard.stripe.com/register.


### Creating the Stripe Payment Integration ###
Ceate a Stripe payment integration in the OPF Workbench. For detailed instructions, see [Creating Payment Integration
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/852d7d8437254529828351dbde217118.html?state=DRAFT).

### Preparing the Postman environment_configuration file ###

**1. Token**

Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

IMPORTANT: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}``.

**2. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …

<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>.

The base Url would be

https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.


**3. Integration ID and Configuration ID**

The ``integrationId`` and ``configurationId`` values identify the payment integration, which can be found in the top left of your configuration details page in the OPF workbench.

**4. Private Key**
The Secret (or Private) Key can be obtained here in the Stripe dashboard. In test it starts with **sk_test**.

<https://dashboard.stripe.com/test/apikeys>

![](images/stripe-elements-get-secret-key.png)

* Set private key as **value** for environment variable  ``authentication_outbound_basic_auth_username_export_67``.
* Set password as **empty string** ``""`` for environment variable : ``authentication_outbound_basic_auth_password_export_67``.

There are 2 occurrences of both in the environment file.

**5. Public Key**

The public (or Publishable) key can be obtained here in the Stripe dashboard. In Test it starts with **pk_test**

<https://dashboard.stripe.com/test/apikeys>

![](images/stripe-elements-get-public-key.png)

Replace the ``publickey`` variable value in the environment file with this value starting with **pk_test**.

**6. Webhook Secret**

IN OPF Workbench: For your new Stripe payment integration, navigate to the **General Information** section of the **Integration details** tab to copy the Notification URL.

In Stripe Dashboard: Navigate to <https://dashboard.stripe.com/test/webhooks> and click **Add an Endpoint**.

i) Paste in your endpoint URL copied from OPF.

![](images/stripe-elements-paste-webook.png)

ii) For simplicity, select “All events”.

![](images/stripe-elements-select-events.png)

iii) Click **Add Endpoint**.

![](images/stripe-elements-add-endpoint.png)

iv) Click **Reveal** the get the webhook secret, it starts with **whsec**.

![](images/stripe-elements-reveal-whsecret.png)

v) In the Environment file set the ``webhookSecret`` value to the key starting with **whsec_**.

### Summary

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

#### Common
- ``token``
- ``rootUrl``
- ``integrationId``
- ``configurationId``

#### Stripe Specific
- ``publicKey``
- ``secretKey``
- ``authentication_outbound_basic_auth_username_export_67``
- ``authentication_outbound_basic_auth_password_export_67``
- ``webhookSecret``
  
