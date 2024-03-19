## Introduction

The Postman Collection enables a [Braintree Hosted Fields](https://developer.paypal.com/braintree/docs/start/hosted-fields)) Payment Form to be used to Take Payments through OPF. 

The integration supports:

* Authorization of Card Payments using PCI SAQ-A Braintree Hosted Fields using the OPF "Hosted Fields" UX Pattern
* Deferred Capture (Single Capture per Order)
* Refunds
* Reversal

## Known Issues
* Refunds currently fail if initiated before they are sent to Settlement
** Workaround manual process of refunding in Braintree based on failed transactions in OPF, then manual update of stuck OPF transaction.

## Planned Backlog Items
* Paypal support
* Support reauthorisation on split settlment cades currently only support Single deferred Capture request per order

## Setup Instructions

### Overview
To import the [Braintree Hosted Field Postman Collection](mapping_configuration.json) this page will take you through the following steps

a) Sign up for a Braintree Sandbox Account
b) Create a Merchant Account Group in OPF Workbench.
c) Set up Your Brasintree Sandbox Account to work with OPF.
d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Braintree Sandbox Account unique values. 


### Create a Braintree Account
You can sign up for a free Braintree Sandbox Account at https://www.braintreepayments.com/sandbox

### Creating the Merchant Account Group
Ceate a new Account Group in the OPF Workbench and set the Merchant ID.

The Merchant ID can be found in the Settings -> Business Area of the Braintree Admin UI
![](images/Braintree-settings-business.png) ![](images/Braintree-merchantId.png)

### Preparing the Postman environment_configuration file

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


**3. Account and Account Group**

The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.


**4. API Credentials**

The Public and Private key can be obtained in the Settings -> API -> Keys section of the Braintree Dashboard

![](images/Braintree-apikeys.png)

* Set the public key **value** for environment variable ``authentication_outbound_basic_auth_username_export_51``
* Set the private key **value** for environment variable ``authentication_outbound_basic_auth_password_export_51``

### Summary

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

#### Common
- ``token``
- ``rootUrl``
- ``accountGroupId``
- ``accountId``

#### Braintree Specific
API Key Configuration
- ``authentication_outbound_basic_auth_username_export_51``
- ``authentication_outbound_basic_auth_password_export_51``

For sandbox testing, all other values can be left as defaults.
