## Introduction ##
The Postman Collection enables the integration of Adyen for payment processing through open payment framework(OPF).

The integration supports:

* Authorization of Adyen payments using the OPF "Hosted Fields" UX Pattern
* Deferred Capture support
* Refunds
* Reauthorization of saved payment

**In summary**: to import the [Adyen Hosted Fields Postman Collection](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Hosted%20Fields/Adyen%20-%20HOSTED_FIELDS%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) this page will guide you through the following steps: 

a) Create your Adyen test account.

b) Create an Adyen payment integration in OPF workbench.

c) Set up your Adyen test account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) file so the collection can be imported with all your OPF tenant and Adyen test account unique values. 

e) Validate the configuration in OPF workbench.


## Create an Adyen Account ##
You can sign up for a free Adyen Test Account at <https://ca-test.adyen.com/ca/ca/login.shtml>.


## Creating an Adyen Payment Integration 
Create an Adyen payment integration in the OPF workbench. For detailed instructions, see [Creating Payment Integration
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/852d7d8437254529828351dbde217118.html?state=DRAFT).


## Setting up Your Adyen Test Account to Work with OPF

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

**3. Integration ID and Configuration ID**

The ``integrationId`` and ``configurationId`` values identify the payment integration, which can be found in the top left of your configuration details page in the OPF workbench.

**4. merchantCode** 

You can obtain your merchant ID in the Adyen Dashboard.

**5. clientkey**

The secretKey can be obtained in the Adyen dashboard. 

Go to **Developers -> API credentials -> ws User** to copy the ``Client Key``.

**Summary**

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

## Adding a Standard Notification for Your Merchant Account

Go to the Adyen Dashboard to Set up event notifications using the URL for Notification previsouly saved. For instructions, see <https://docs.adyen.com/issuing/set-up-webhooks/#configure-customer-area>.
    

## Editing the Postman Collection in the Postman App

   1. Import the two files at the same time to Postman.

   2. Make sure to select the environment for Adyen.

   3. Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Adyen Test Account unique values.

| Name                                                                                 | Description                                                  
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.  |                  
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.|                  
| service                                                                       | The ``service`` is the name of your OPF service in specific environment. This will usually always be ``opf``|
| integrationId                                                                       | The ``integrationId`` and ``configurationId`` values that identify the payment integration can be found in the top left of your configuration details page.|                  
| configurationId                                                                            | The ``integrationId`` and ``configurationId`` values that identify the payment integration can be found in the top left of your configuration details page.|                                                                          
| authentication_inbound_basic_auth_username                                           | The username for notification basic authentication. Set the value when configuring webhooks in your Balance Platform Customer Area.|                  
| authentication_inbound_basic_auth_password                                           | The password for notification basic authentication. Set the value when configuring webhooks in your Balance Platform Customer Area. |                  
| capturePattern                                                                       | ``CAPTURE_PER_SHIPMENT``|                  
| supportOverCapture                                                                   | ``true``|                  
| enableOverCapture                                                                    | ``true``|                  
| authorizationTimeoutDays                                                             | 7   |                  
| authentication_outbound_api_key_value_export                                         | The Webservice User API key. Go to **Developers** -> **API credentials** -> **ws User** -> **Authentication** to get the value.|                  
| googlePayGateway                                                                     | ``Adyen``| 
|checkoutPaymentHost                                                                   | ``checkout-test.adyen.com``|
|merchantCode                                                                          |  You can obtain your merchant ID in the Adyen Dashboard.|          |
|serviceVersion                                                                        | v67|
|clientKey                                                                             | Go to **Developers** -> **API credentials** -> **ws User** to copy Client Key.|  
|checkoutShopperHost                                                                   | ``checkoutshopper-test.adyen.com``|
| mode                                                                                 | ``test``|
| standardPaymentHost                                                                  | ``pal-test.adyen.com``|
| allow3DS2                                                                            | ``true``|
| notificationHmacKey                                                                  |The Notification HMAC, which is used for Hosted Field notification signature. Go to **Developers** ->  **Webhooks** to get the value.|
      
   5. Save and run the Postman collection.


## Validating the Configuration in Open Payment Framework Workbench

   1. Log in to the open payment framework workbench.
   2. Click **Payment Integrations** in the left navigation bar.
   3. Navigate to **Payment Integrations** -> **(your Adyen integration)** -> **Integration Details**.
   4. In the **Configuration section**, click **Show Details** to go to the configuration details page.
   5. In the **Settlement Method** section, make sure the right option is selected depending on your integration.
   6. In the **Authorization** section, click **Edit** to go to the authorization details page.
   7. In **Authorization** -> **Front-end component configuration**, make sure the Payment Form is the one corresponding to your integration.
