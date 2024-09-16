## Introduction ##

This Postman Collection aids in integrating Nexi payment gateway into the Open Payment Framework (OPF).

Currently, the integration supports:

* Authorization of Nexi payments using the OPF "Payment Page" UX pattern
* Refunds

**In summary**:
To import the [Nexi Payment Page Collection](https://github.com/opf-postman/sap-commerce-cloud-open-payment-framework-integration/tree/main/postman/nexi/PAYMENT_PAGE), this page will guide you through the following steps:

a) Create your Nexi test account.

b) Create a Nexi payment integration in OPF workbench.

c) Set up your Nexi test account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/sap-commerce-cloud-open-payment-framework-integration/blob/main/postman/nexi/PAYMENT_PAGE/environment_configuration.json) file so the collection can be imported with all your OPF tenant and Nexi test account unique values.

e) Validate the configuration in OPF workbench.

## Creating a Nexi Account ##

You can sign up for free and access Nexi test-area at <https://ecommerce.nexi.it/area-test>.

## Creating a Nexi-XPay payment integration ##

Create a Nexi-XPay payment integration in the OPF workbench. For detailed instructions, see [Creating Payment Integration](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/852d7d8437254529828351dbde217118.html?state=DRAFT).

**Note**: 

1. When creating the payment integration, be sure to set the **Payment integration** to **Payment Gateway**. 
2. The default configuration supports only **Immediate Capture** as the settlement method. To switch to other methods, technical support from Nexi is required. For more details, search for the **TCONTAB** keyword in the [Nexi Documentation](https://ecommerce.nexi.it/specifiche-tecniche/codicebase/introduzione.html).

## Setting up Your Nexi Test Account to work with OPF ##

Once you have created you Nexi test account, do the following to set it up to work with OPF:

1. **Determine testing account structure**

   **merchant account** is used to login test-area to get some key info about integration(e.g. merchant ID, signature secret) and other data about current merchant(e.g. ADMIN login info).

   **admin account** is used to login back office to do detailed management with current merchant.

   **user account** The admin can add users to the **User Management** section in the back office to facilitate collaborative work among multiple users within the user account.
   
3. **Get API credentials**

   Get your test API data in [Test-area welcome page](https://ecommerce.nexi.it/area-test) after you login successfully.

   Example:
   * Alias: ALIAS_WEB_xxxxxxx
   * Key for mac calculation: MQY8KWXXXXXXXXXXXXXNDJK1
   * Group: GRP_xxxxxxx
  
5. **Add payment methods**
   Not involved yet.

## Preparing the Postman environment_configuration file ##

**1. fetch credential from SAP PassVault**

you need 4 keys to generate Token, both "client_id" and "client_secret" keys are fetched from [SAP PassVault](https://password.wdf.sap.corp/passvault/#/pw/0000399982),the "grant_type" key value should be "client_credentials", the last key "resource" value is "urn:sap:identity:application:provider:name:opf-int-mgt".

**2. Token**

Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained in step 1.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

**IMPORTANT**: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}`` and when do test watch the expiration of token.

**3. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>. The base Url would be ``https://opf-iss-d0.uis.commerce.stage.context.cloud.sap``.

**4. service**

The ``service`` represents the name of your OPF service within a specific environment, which typically defaults to ``opf``.

**5. Integration ID and Configuration ID**

The ``integrationId`` and ``configurationId`` values that identify the payment integraiton can be found in the top left of your configuration details page.

**Note**: 

In the environment_configuration.json, ``accountGroupId`` matches ``integrationId`` and ``accountId`` matches ``configurationId`` mentioned above.

**6. alias, gruppo and secret**

As listed in Step 3.

## Summary ##

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the **correct environment** before running the collection in Postman.

## Allowlist ##

Depending on your environment, add the following domains to the domain allowlist in OPF workbench. For instructions, see [Adding Tenant-specific Domain to Allowlist
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/a6836485b4494cfaad4033b4ee7a9c64.html?state=DRAFT).

``int-ecommerce.nexi.it`` for test
``ecommerce.nexi.it`` for production

## Other configurations about Domain ##

If your can not send a refund request successfully and get an error of code 500, you need to add provider's domain into a permission list on [cx-commerce/cds-configuration](https://github.tools.sap/cx-commerce/cds-configuration/blob/main/istio/service-entries/cds-b-sus.yaml)

## Editing the Postman Collection in the Postman App ##

   1. Import the two files at the same time to Postman.

   2. Make sure to select the environment for Nexi.

   3. Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Nexi Test Account unique values.(For other variables, please refer to the table below)
      
   4. Save and run the Postman collection.

| Name                                                                                 | Description
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.|
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.|
| service                                                                       | The ``service`` represents the name of your OPF service within a specific environment, which typically defaults to ``opf``. |
| accountGroupId                                                                       | The ``integrationId`` and ``configurationId`` values that identify the payment integraiton can be found in the top left of your configuration details page.|
| accountId                                                                     | The ``integrationId`` and ``configurationId`` values that identify the payment integration can be found in the top left of your configuration details page.|
| capturePattern                                           | Defaults to ``AUTO_CAPTURE``. |
| supportOverCapture                                           | ``false`` |
| enableOverCapture                                                                       | ``false``|
| authorizationTimeoutDays                                                                   | ``7``|
| apiEnv| ``int-ecommerce.nexi.it`` You can get this from Nexi's Doc, for prod Env the value is ``ecommerce.nexi.it`` |
| alias                                                                    | You can obtain your alias from the test-area welcome page. |
|gruppo| ou can obtain your alias from test-area welcome page. |
|TCONTAB                                                                   |``C``, The field identifies the collection mode that the merchant wants to apply to the individual transaction, check details in [Nexi Documentation](https://ecommerce.nexi.it/specifiche-tecniche/codicebase.html).|
| secret                                                             | You can obtain ``Key for mac calculation`` in test-area welcome page, which is equivalent to secret. |

## Validating the Configuration in OPF Workbench ##

   1. Log in to the OPF workbench.
   2. Click **Payment Integrations** in the left navigation bar.
   3. Navigate to **Payment Integrations** -> **(your Nexi integration)** -> **Integration Details**.
   4. In the **Configuration section**, click **Show Details** to go to the configuration details page.
   5. In the **Settlement Method** section, make sure the right option is populated depending on your integration.
   6. In the **Authorization** section, click **Edit** to go to the authorization details page.
   7. In **Authorization** -> **Front-end component configuration**, make sure the Payment Form is the one corresponding to your integration.

## Additional information ##

Nexi can only support ``EUR`` as the currency for settlement. Using any other currency will result in a runtime error. Therefore, when testing this integration, ensure that you switch the currency to EUR before placing an order.
