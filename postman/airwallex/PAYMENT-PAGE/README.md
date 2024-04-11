## Introduction

The Postman Collection enables a [Airwallex Hosted Page](https://developer.paypal.com/braintree/docs/start/hosted-fields) Payment Form to be used to Take Payments through OPF. 

The integration supports:

* Authorization of Card Payments using PCI SAQ-A Airwallex Hosted Page using the OPF "Hosted Patters" UX Pattern
* Deferred Capture 
* Refunds
* Reversal
* Recurrent Authorization

## Known Issues
* Auto currency conversion should be disabled


## Planned Backlog Items


## Setup Instructions

### Overview
To import the [Aiwallex Hosted Page Postman Collection](mapping_configuration.json) this page will take you through the following steps

a) Sign up for a Airwallex Demo Account
b) Create a Merchant Account Group in OPF Workbench.
c) Set up Your Airwallex Sandbox Account to work with OPF.
d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Airwallex Sandbox Account unique values. 


### Create a Airwallex Account
You can sign up for a free Airwallex Demo Account at https://demo.airwallex.com/signup.
To activate the account without completeting the company onboarding you will need to contact Airwallex support.




### Creating the Merchant Account Group
Create a new Account Group in the OPF Workbench and set the Merchant ID.

The Merchant ID can be found in the Account -> 

https://demo.airwallex.com/app/account/details


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


### Summary

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

#### Common
- ``token``
- ``rootUrl``
- ``service``
- ``accountGroupId``
- ``accountId``

#### Airwallex Specific
API Key Configuration

For sandbox testing, all other values can be left as defaults.  



### Airwallex Setup



