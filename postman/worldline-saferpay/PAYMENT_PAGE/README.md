## Introduction ##
This Postman Collection aids in integrating [Worldine Saferpay](https://worldline.com/en-ch/home/main-navigation/solutions/merchants/solutions-and-services/e-commerce/saferpay-payment-solution) into the Open Payment Framework (OPF).

The integration supports:

* Authorize card using [Payment Page](https://docs.saferpay.com/home/integration-guide/licences-and-interfaces/payment-page)
* Settlement - Delayed Capture Pattern
* Refund
* Reversal
* Reauthorization

## Known Issues ##
The Saferpay mechanism for [Server to Server notifications](https://docs.saferpay.com/home/integration-guide/licences-and-interfaces/payment-page#handling-notifications) is not currently supported by OPF.

### In summary ###
In summary, to import the [Postman Collection](mapping_configuration.json), this page will guide you through the following steps:

a) [Create your Worldine Saferpay test account](https://test.saferpay.com/BO/SignUp?lang=en).

b) Create a Worldine payment integration in OPF

c) Get the credentials of your Worldine Saferpay integration.

d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Wordline Saferpay Test Account unique values. 

### Creating a Worldline Saferpay Account ###
You can sign up for a free Worldline Saferpay test account at [Create your Worldine Saferpay test account](https://test.saferpay.com/BO/SignUp?lang=en).


### Creating a Worldline Saferpay Payment Integration ###
Create a Worldline Saferpay payment integration in the OPF workbench. For reference, see [Creating Payment Integration
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/20a64f954df1425391757759011e7e6b.html?state=DRAFT).

The Merchant ID is the Customer ID found in the header of Saferpay Backoffice.

![](../images/saferpay-merchant-id.png)


### Setting up Your Worldine Saferpay Test Account to work with OPF ###
Once you have created you Saferpay test account, do the following to set it up to work with OPF:
1. Create a **JSON API Basic Authentication Login** and note down the user name and set a strong password as directed.

   ![](../images/saferpay-json-api.png)
   
3. Note down the **Saferpay Ecommerce terminal ID**.

   ![](../images/saferpay-terminal.png)

### Preparing the Postman environment_configuration file ###

**1. Token**

Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

**IMPORTANT**: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}``.

**2. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …

<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>.

The base Url would be

https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.


**3. Integration ID and Configuration ID**

The ``integrationId`` and ``configurationId`` values identify the payment integration, which can be found in the top left of your **Configuration Details** page in the OPF workbench.

* ``integrationId`` maps to ``accountGroupId`` in postman
* ``configurationId`` maps to ``accountId`` in postman

**4. authentication_outbound_basic_auth_username_export_211**

The value of this variable is the JSON API Username, this usually starts with ``API_`` in Saferpay.

**5. authentication_outbound_basic_auth_password_export_211**

This is the password you set for the corresponding JSON API User.

**6. terminalIdCommerce**

This is the Saferpay Terminal ID noted down earlier.

### Allowlist
Add the following domains to the domain allowlist in OPF workbench. For instructions, see [Adding Tenant-specific Domain to Allowlist
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/a6836485b4494cfaad4033b4ee7a9c64.html?state=DRAFT).


``www.saferpay.com`` for production

``test.saferpay.com`` for test


### Summary

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

#### Common
- ``token``
- ``rootUrl``
- ``accountGroupId``
- ``accountId`` 

#### Worldline Saferpay Specific
- ``authentication_outbound_basic_auth_username_export_211``
- ``authentication_outbound_basic_auth_password_export_211``
- ``terminalIdCommerce`` 
  
