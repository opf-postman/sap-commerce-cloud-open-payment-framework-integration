## Introduction ##
This Postman Collection aids in integrating [Payever](https://getpayever.com/) into the Open Payment Framework (OPF).

The integration supports:

* Authorize card using Hosted Page
* Settlement
* Refund
* Reversal

Payment options tested:
* Stripe
* Santander Installments

### Backlog
* Reauthorization
* Support for Finance options


### In summary ###
In summary, the integration shows how to integrate payever with their open sandbox. No account is required to use the sandbox. Production account requires contact with Payever.

To import the [Postman Collection](mapping_configuration.json), this page will guide you through the following steps:

a) Create a Payever payment integration in OPF.

b) Get the credentials for your Payever integration.

d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Payever Sandbox Account unique values. 


### Creating a Payever Payment Integration ###
Create a Payever payment integration in the OPF workbench. For reference, see [Creating Payment Integration
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/20a64f954df1425391757759011e7e6b.html?state=DRAFT).

**Note**:

The Merchant ID is the Business UUID provided by Payever. For the Sandbox you can use ``payever`` as per [Sandbox credentials](https://docs.payever.org/resources/dk/test-credentials/api-credentials/).


### Preparing the Postman environment_configuration file ###

**1. Token**

Get your access token by [creating an external app](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/d927d21974fe4b368e063f72733bf0fe.html?state=DRAFT) and [making authorized API calls](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/40c792e66e2942209dc853a43533d78d.html?state=DRAFT).

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

**IMPORTANT**: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}``.

**2. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …

<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>.

The base Url would be

https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.


**3. Integration ID and Configuration ID**

The ``integrationId`` and ``configurationId`` values identify the payment integration and payment configuration, which can be found in the top left of your **Configuration Details** page in the OPF workbench.

* ``integrationId`` maps to ``accountGroupId`` in postman
* ``configurationId`` maps to ``accountId`` in postman

**4. clientId**

The is the api Client Id which for the sandbox environment can be obtained [here](https://docs.payever.org/resources/dk/test-credentials/api-credentials/).

**5. secret**

The is the api Client Secret which for the sandbox environment can be obtained [here](https://docs.payever.org/resources/dk/test-credentials/api-credentials/).

**6. apiDomain**

This configured whether to target the production or sandbox environment.

``proxy.payever.org`` for production

``proxy.staging.devpayever.com`` for sandbox script element


### Allowlist
Add the following domains to the domain allowlist in OPF workbench. For instructions, see [Adding Tenant-specific Domain to Allowlist
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/a6836485b4494cfaad4033b4ee7a9c64.html?state=DRAFT).


``proxy.payever.org`` for production account

``proxy.staging.devpayever.com`` for test account


### Summary

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

#### Common
- ``token``
- ``rootUrl``
- ``accountGroupId``
- ``accountId`` 

#### Payever Specific
- ``clientId``
- ``secret``
- ``merchantId``
- ``apiDomain``
  
