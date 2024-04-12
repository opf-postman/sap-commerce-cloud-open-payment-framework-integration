## Introduction ##
The Postman Collection enables Adyen to be used to take payments through OPF. 

The integration supports:

* Authorization of Adyen Payments using the OPF "Hosted Fields" UX Pattern
* Deferred Capture support
* Refunds
* Reauthorization of saved payment

**In summary**: to import the [Adyen Hosted Fields Postman Collection](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Hosted%20Fields/Adyen%20-%20HOSTED_FIELDS%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) this page will guide you through the following steps: 

a) Create Your Adyen Test Account.

b) Create a Merchant Account Group in OPF Workbench.

c) Set up Your Adyen Test Account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) file so the collection can be imported with all your OPF Tenant and Adyen Test Account unique values. 

e) Validate the configuration in Open Payment Framework Workbench.


## Create an Adyen Account ##
You can sign up for a free Adyen Test Account at <https://ca-test.adyen.com/ca/ca/login.shtml>.


## Creating the Merchant Account Group 
Ceate a new Account Group in the OPF Workbench.

1. In payment integrations.. click **Create**.
![](images/cybersource-create-button.png)

2. Add account name (can be anything) and set payment gateway to Adyen.
![](images/cybersource-create-account.png)

3. Click **configure** on Test column of newly created Account.

   **You must set a merchant ID first.**
   You can obtain your merchant ID in the Adyen Dashboard.

     a.) Note down the ``accountId`` and the ``accountGroupId``. These two values identify the merchant account group, which can be found in the top left of your merchant configuration.
   
   b.) In the **General configuration** tab, set the Merchant ID of the Payment account using the value retrieved in Adyen.

   c.) In the **Notification** tab, note down the URL for notification.


## Set up Your Adyen Test Account to work with OPF

   Once you have created you Adyen test account, do the following to set it up to work with OPF:

1. **Determine testing account structure**
   With Adyen, you have a single [company account](https://docs.adyen.com/account/account-structure/#company-account), and one or more sub-accounts called [merchant accounts](https://docs.adyen.com/account/account-structure/#company-account). Determine an initial structure for testing that will best represent what you will do once you are processing live. You will have another opportunity when going live to finalize your account structure.

2. **Create a user for yourself and your team members**
   
   You receive an admin user account for yourself when signing up. [Create additional users](https://docs.adyen.com/account/users/) for your team members as needed.

3. **Get API credentials**
   
   Get your test API key and client key, which you'll need when building your integration. You can refer to [Create an API credential](https://docs.adyen.com/development-resources/api-credentials/#new-credential) for detailed instructions.

4. **Add payment methods**
   
   [Add the payment methods](https://docs.adyen.com/payment-methods/add-payment-methods/) you want to accept with your integration.

## Preparing the Postman environment_configuration file

**1. Token**

Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

**IMPORTANT**: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}``.

**2. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>. The base Url would be https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.

**3. Account and Account Group**

The ``accountId`` and ``accountGroupId`` values identify the merchant account group, which can be found in the top left of your merchant configuration.

**4. merchantCode** 

You can obtain your merchant ID in the Adyen Dashboard.

**5. clientkey**

The secretKey can be obtained in the Adyen dashboard. 

Go to **Developers -> API credentials -> ws User** to copy the ``Client Key``.

**Summary**

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

## Add a Standard Notification for Your Merchant Account

Go to the Adyen Dashboard to Set up event notifications using the URL for Notification previsouly saved. For instructions, see [Set up event notifications in the Customer Area
](https://docs.adyen.com/point-of-sale/design-your-integration/notifications/event-notifications/#set-up-in-ca).
    

## Edit the Postman Collection in the Postman app.

   1. Import the two files at the same time to Postman.

   2. Make sure to select the environment for Adyen.

   3. Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Adyen Test Account unique values.

| Name                                                                                 | Description                                                  
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.  |                  
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.|                  
| service                                                                       | The ``service`` is the name of your OPF service in specific environment. This will usually always be ``opf``|
| accountGroupId                                                                       | The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.|                  
| accountId                                                                            | The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.|                                                                          
| authentication_inbound_basic_auth_username                                           | ``username``, your web service username in Adyen Dashboad.|                  
| authentication_inbound_basic_auth_password                                           | ``password``: the password that you can generate for Basic auth under **Configure API credential** -> **Server settings** |                  
| capturePattern                                                                       | ``CAPTURE_PER_SHIPMENT``|                  
| supportOverCapture                                                                   | ``true``|                  
| enableOverCapture                                                                    | ``true``|                  
| authorizationTimeoutDays                                                             | 7   |                  
| authentication_outbound_api_key_value_export                                         | The ``apiKey`` value saved from [Create an API credential](https://docs.adyen.com/development-resources/api-credentials/#new-credential).|                  
| googlePayGateway                                                                     | ``Adyen``| 
|checkoutPaymentHost                                                                   | ``checkout-test.adyen.com``|
|merchantCode                                                                          |            |
|serviceVersion                                                                        | v67|
|clientKey                                                                             | The ``clientKey`` saved from [Create an API credential](https://docs.adyen.com/development-resources/api-credentials/#new-credential).|  
|checkoutShopperHost                                                                   | ``checkoutshopper-test.adyen.com``|
| mode                                                                                 | ``test``|
| standardPaymentHost                                                                  | ``pal-test.adyen.com``|
| allow3DS2                                                                            | ``true``|
| notificationHmacKey                                                                  | |
      
   5. Save and run the Postman collection.


## Validate the configuration in Open Payment Framework Workbench

   1. Go to **Payment Integrations**-> **Merchant account** and click **Configure**.

      **Note**
      If you are testing the integration, you must select the Test payment account.

   2. The **General configuration** -> **Variables** values must be populated.

   3. In **Settlement method**, make sure the right option is selected depending on your integration.
   
   4. In **Authorization** -> **Front-end component configuration**, make sure the Payment Form Display is the one corresponding to your integration.
