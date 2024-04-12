## Introduction ##
The Postman Collection enables Worldpay to be used to take payments through OPF. 

The integration supports:

* Authorization of Worldpay Payments using the OPF "iFrame" UX Pattern
* Deferred Capture support
* Refunds
* Reauthorization of saved payment

**In summary**: to import the [Worldpay iFrame Postman Collection](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/worldpay/iFrame/Worldpay%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json) this page will guide you through the following steps: 

a) Create Your Worldpay Test Account.

b) Create a Merchant Account Group in OPF Workbench.

c) Set up Your Worldpay Test Account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/worldpay/iFrame/Worldpay%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Provider_Configuration.json) file so the collection can be imported with all your OPF Tenant and Worldpay Test Account unique values. 

e) Validate the configuration in Open Payment Framework Workbench.


## Create an Worldpay Account ##
You can sign up for a free Worldpay Test Account at <https://secure.worldpay.com/sso/public/auth/login.html>.


## Creating the Merchant Account Group 
Ceate a new Account Group in the OPF Workbench.

1. In payment integrations.. click **Create**.
![](images/cybersource-create-button.png)

2. Add account name (can be anything) and set payment gateway to Worldpay.
![](images/cybersource-create-account.png)

3. Click **configure** on Test column of newly created Account.

   **You must set a merchant ID first.**
   You can obtain your merchant ID in the Worldpay Dashboard.

     a.) Note down the ``accountId`` and the ``accountGroupId``. These two values identify the merchant account group, which can be found in the top left of your merchant configuration.
   
   b.) In the **General configuration** tab, set the Merchant ID of the Payment account using the value retrieved in Worldpay.

   c.) In the **Notification** tab, note down the URL for notification.


## Set up Your Worldpay Test Account to work with OPF

   Once you have created you Worldpay test account, do the following to set it up to work with OPF:

1. In the left navigation panel, choose **Integration** -> **Merchant Channel** to configure the messages and content settings at corresponding sections for Test and Production purposes.
   
   a) Enable XML message for HTTP notifications.
   
   b) Enter the notification URL previously saved in the **Address** field.
   
   c) Select the events that you want to receive.
   
   d) Save the settings.

2. In the left navigation panel, choose **Integration** -> **Apple Pay** to generate Apple Pay Certificate Sign Secret (CSR) if you want to enable Apple Pay payments via web or app.
   
    For detailed instructions to configure a direct Apple Pay integration to WorldPay, see <https://developer.worldpay.com/docs/wpg/mobilewallets/applepay>.
   

3. In the left navigation panel, choose **Integration** -> **Google Pay** to generate a unique merchant ID if you want to enable Google Pay payments via web or app.

   For detailed instructions to configure a direct Google Pay integration to WorldPay, see <https://developer.worldpay.com/docs/wpg/mobilewallets/googlepay>.
   

4. In the left navigation panel, choose **Integration** -> **Configuration Details** to deactivate the **Capture Delay** option.

5. In the left navigation panel, choose **Integration**-> **Installations** to copy the installation ID.



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

You can obtain your merchant ID in the Worldpay Dashboard.


**Summary**

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.
    

## Edit the Postman Collection in the Postman app.

   1. Import the two files at the same time to Postman.

   2. Make sure to select the environment for Worldpay.

   3. Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Worldpay Test Account unique values.

| Name                                                                                 | Description                                                  
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.  |                  
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.|                  
| service                                                                       | The ``service`` is the name of your OPF service in specific environment. This will usually be ``opf`` |
| accountGroupId                                                                       | The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.|                  
| accountId                                                                            | The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.|                                                                          
| authentication_inbound_basic_auth_username                                           | The username for basic authentication. Go to **Account** -> **Profile** to get the value.|                  
| authentication_inbound_basic_auth_password                                           | The password for basic authentication. Go to **Account** -> **Profile** to get the value.|                  
| capturePattern                                                                       | ``CAPTURE_PER_SHIPMENT``|                  
| supportOverCapture                                                                   | ``true``|                  
| enableOverCapture                                                                    | ``true``|                  
| authorizationTimeoutDays                                                             | 7   |                                  
|merchantCode                                                                          |Your merchant ID. Go to **Account** -> **Profile** to get the value.|
|installationId                                                                        |Go to **Integration** -> **Installations** to get the value.|
       
   5. Save and run the Postman collection.


## Validate the configuration in Open Payment Framework Workbench

   1. Go to **Payment Integrations**-> **Merchant account** and click **Configure**.

      **Note**
      If you are testing the integration, you must select the Test payment account.

   2. The **General configuration** -> **Variables** values must be populated.

   3. In **Settlement method**, make sure the right option is selected depending on your integration.
   
   4. In **Authorization** -> **Front-end component configuration**, make sure the Payment Form Display is the one corresponding to your integration.

