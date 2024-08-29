# ReadMe #

## Introduction ##

This Postman Collection is helping with integrating Nexi into open payment framework(OPF).

 Currently, the integration temporarily supports:

* Authorization of Nexi payments using the OPF "Payment Page" UX pattern
* Refunds

**In summary**:
to import the [Nexi Payment Page](https://github.com/opf-postman/commerce-cloud-open-payment-integration/tree/main/postman/adyen/Hosted-Payment-Page), this page will guide you through the following steps:

a) Create your Nexi test account.

b) Create an Nexi payment integration in OPF workbench.

c) Set up your Nexi test account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) file so the collection can be imported with all your OPF tenant and Nexi test account unique values.

e) Validate the configuration in OPF workbench.

## Creating an Nexi Account ##

You can sign up for free and access Nexi test-area at <https://ecommerce.nexi.it/area-test>.

## Creating a Nexi-XPay payment integration ##

Create an Nexi-XPay payment integration in the OPF workbench. For detailed instructions, see [Creating Payment Integration](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/852d7d8437254529828351dbde217118.html?state=DRAFT).

PS. Default configuration only support **Immediate Capture**, switch to other mode you may need ask PSP for technical support. Searching **TCONTAB** keyword in [Doc](https://ecommerce.nexi.it/specifiche-tecniche/codicebase/introduzione.html), for more details.

## Setting up Your Nexi Test Account to work with OPF ##

   Once you have created you Nexi test account, do the following to set it up to work with OPF:

1. **Determine testing account structure**

   **merchant account** is used to login test-area to get some key info about integration(e.g. merchant ID, signature secret) and other data about current merchant(e.g. ADMIN login info).

   **admin account** is used to login back office to do detailed management with current merchant.

   **user account** admin can add Users in the <u>User management</u> tag of back office to support multiple user working collaboratively(But util now i haven't successfully create an extra user account, I'm not sure whether it's a test-area error, in this article we will use ADMIN account to do configuration temperarily)

2. **Get API credentials**

   Get your test API data in [Test-area welcome page](https://ecommerce.nexi.it/area-test) after you login successfully.
   Example:
   * Alias: ALIAS_WEB_xxxxxxx
   * Key for mac calculation: MQY8KWXXXXXXXXXXXXXNDJK1
   * Group: GRP_xxxxxxx
  
3. **Add payment methods**
   Not involved yet.

## Preparing the Postman environment_configuration file ##

**1. Token**
Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

**IMPORTANT**: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}`` and when do test watch the expiration of token.

**2. Root url**
The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>. The base Url would be https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.

**IMPORTANT**: The default environment value which export from workbench may not the right root url, you'd better filling the root url manually according the environment you want to configure, especially when you meet a 404 error when send requests.

**3. service**
The ``service`` is the name of your OPF service in specific environment. This will usually be ``opf``

**4. Integration ID and Configuration ID**
The ``integrationId`` and ``configurationId`` values that identify the payment integraiton can be found in the top left of your configuration details page.

PS. In the environment_configuration.json, ``accountGroupId`` matches ``integrationId`` and ``accountId`` matches ``configurationId`` we referred above.

**5. alias, gruppo and secret**
We referred above.

## Summary ##

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the ```correct environment```  before running the collection in Postman.

## Allowlist ##

Depending on your environment, add the following domains to the domain allowlist in OPF workbench. For instructions, see [Adding Tenant-specific Domain to Allowlist
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/a6836485b4494cfaad4033b4ee7a9c64.html?state=DRAFT).

``int-ecommerce.nexi.it`` this one is for test
``ecommerce.nexi.it`` this one is for prod

## Other config about Domain ##

If your can not send a refund request successfully and get an error of code 500, you may need to add provider's domain into a permission list on [cx-commerce/cds-configuration](https://github.tools.sap/cx-commerce/cds-configuration/blob/main/istio/service-entries/cds-b-sus.yaml)

## Editing the Postman Collection in the Postman App ##

   1. Import the two files at the same time to Postman.

   2. Make sure to select the environment for Nexi.

   3. Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Nexi Test Account unique values.(Other variables please refer to the table below)
   4. Save and run the Postman collection.

| Name                                                                                 | Description
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.|
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.|
| service                                                                       | The ``service`` is the name of your OPF service in specific environment. This will usually be ``opf`` |
| accountGroupId                                                                       | The ``accountGroupId`` equals ``integrationId``. The ``integrationId`` and ``configurationId`` values that identify the payment integraiton can be found in the top left of your configuration details page.|
| accountId                                                                     | The ``accountId`` equals ``configurationId``. The ``integrationId`` and ``configurationId`` values that identify the payment integration can be found in the top left of your configuration details page.|
| capturePattern                                           | ``AUTO_CAPTURE``, this is Determine OPF side capture mode |
| supportOverCapture                                           | ``false`` |
| enableOverCapture                                                                       | ``false``|
| authorizationTimeoutDays                                                                   | ``7``|
| apiEnv| ``int-ecommerce.nexi.it`` You can get this from Nexi's Doc, for prod Env the value is ``ecommerce.nexi.it`` |
| alias                                                                    | You can obtain your alias from test-area welcome page. |
|gruppo| ou can obtain your alias from test-area welcome page. |
|TCONTAB                                                                   |``C``, The field identifies the collection mode that the merchant wants to apply to the individual transaction, check details in [Nexi Doc](https://ecommerce.nexi.it/specifiche-tecniche/codicebase.html)|
| secret                                                             | You can obtain ``Key for mac calculation`` in test-area welcome page, which equivalent to secret. |

## Validating the Configuration in OPF Workbench ##

   1. Log in to the OPF workbench.
   2. Click **Payment Integrations** in the left navigation bar.
   3. Navigate to **Payment Integrations** -> **(your Nexi integration)** -> **Integration Details**.
   4. In the **Configuration section**, click **Show Details** to go to the configuration details page.
   5. In the **Settlement Method** section, make sure the right option is populated depending on your integration.
   6. In the **Authorization** section, click **Edit** to go to the authorization details page.
   7. In **Authorization** -> **Front-end component configuration**, make sure the Payment Form is the one corresponding to your integration.

## Key Notes ##

**SOME IMPORTANT PROBLEM NEED TO EXPLAIN**
When we do integration, found some problems may cause some confusion for our customer.

### PROBLEM 1 ###

When customer Place Order and jump to Payment page, he will find a order Id, when succussfully finishing payment he will find another order Id in merchant's page, but the two ids do not match, that may make customer felling confused.

**EXPLANATION**
The root cause for this phenomenon is that OPF will send PSP an ID as current payment Order's identification(codTrans), So this id will present at payment page. But after payment finished successfully, merchant's front page will ask Commerce Cloud for checking order info, at this moment, Commerce Cloud will generate the real order id and deliver it back to front page, then the second id show up and confusion arising.

**Solution 1**
To solve probem 1, we tried to set cartId as the identify Id(codTrans). if any error occurs when customer processing payment authorization, this cartId will cause a reduplicate error on PSP side, and can not visit payment page any more until customer clean their cart and restart adding goods to create a new cart.

> Although follow Nexi's documentation, under the default configuration, the same codTrans can be passed in at most three times. But in  actual testing we found that doesn't work.

**Solution 2**
According to the pre solution, we made a decision of using transaciton id as the codTrans. When we send a refund request, new problem occured. For CCV2, the refund work is regarded as a new <i> **Transaction** </i>, so directlly fetching and sending transaction id to provider in refund flow, will getting the FAILED response from provider because of MAC mismatching.

**Solution 3**
Finally, we choose custom mapping field as the solution currently.When recieved providers Authentication Notification, We pick up the codTrans and create a custom field to store the Id, then use this id to calculate signature and send it back to provider in refund flow.

### PROBLEM 2 ###

Nexi can ``ONLY`` support ``EUR`` as the currency of settlement, ANY other currency will cause a runtime error, when you test this integration, must switch the currency to EUR before you place order.
