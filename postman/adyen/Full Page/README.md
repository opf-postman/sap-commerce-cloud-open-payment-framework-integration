## Introduction ##
The Postman Collection enables Adyen to be used to take payments through OPF. 

The integration supports:

* Authorization of Adyen Payments using the OPF "Full Page" UX Pattern
* Deferred Capture support
* Refunds
* Reauthorization of saved payment

In summary: to import the [Adyen Full Page Postman Collection](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Provider_Configuration.json) this page will guide you through the following steps: 

a) Create Your Adyen Test Account.

b) Create a Merchant Account Group in OPF Workbench.

c) Set up Your Adyen Test Account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) file so the collection can be imported with all your OPF Tenant and Adyen Test Account unique values. 

## Create an Adyen Account ##
You can sign up for a free Adyen Test Account at <https://ca-test.adyen.com/ca/ca/login.shtml>.


## Creating the Merchant Account Group 
Ceate a new Account Group in the OPF Workbench.

1. In payment integrations.. click **Create**.
![](images/cybersource-create-button.png)

2. Add account name (can be anything) and set payment gateway to Adyen.
![](images/cybersource-create-account.png)

3. Click **configure** on Test column of newly created Account.
![](images/opf-account-group-id.png)

**You must set a merchant ID first.**
You can obtain your merchant ID in the Adyen Dashboard.
![](images/cybersource-get-merchant-id.png)

## Set up Your Adyen Test Account to work with OPF

   Once you have created you Adyen test account, do the following to set it up to work with OPF:

1. **Determine testing account structure**
   With Adyen, you have a single [company account](https://docs.adyen.com/account/account-structure/#company-account), and one or more sub-accounts called [merchant accounts](https://docs.adyen.com/account/account-structure/#company-account). Determine an initial structure for testing that will best represent what you will do once you are processing live. You will have another opportunity when going live to finalize your account structure.

2. **Create a user for yourself and your team members**
   
   You receive an admin user account for yourself when signing up. [Create additional users](https://docs.adyen.com/account/users/) for your team members as needed.

4. **Get API credentials**
   
   Get your test [API key](https://docs.adyen.com/account/users/) and [client key](https://docs.adyen.com/account/users/), which you'll need when building your integration.

6. **Add payment methods**
   
   [Add the payment methods](https://docs.adyen.com/payment-methods/add-payment-methods/) you want to accept with your integration.


## Preparing the Postman environment_configuration file

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

**3. Account and Account Group**

The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.

![](images/cybersource-get-group-id.png)

**4. merchantCode** 

You can obtain your merchant ID in the Adyen Dashboard.

![](images/cybersource-get-merchant-id.png)

**5. clientkey**

The secretKey can be obtained in the Adyen dashboard. 

Go to **Developers -> API credentials -> ws User** to copy the ``Client Key``.


**Summary**

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

## Edit the Postman Collection in the Postman app.

   1. Import the two files at the same time to Postman.

   2. Make sure to select the environment for Mock Gateway.

   3. Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Adyen Test Account unique values.
      

## Validate the configuration in Open Payment Framework Workbench.

   1. Go to **Payment Integrations**-> **Merchant account** and click **Configure**.

      **Note**
      If you are testing the integration, you must select the Test payment account.

   2. The **General configuration** -> **Variables** values must be populated.

   3. In Settlement method, make sure the right option is selected depending on your integration.
   
   4. In **Authorization** -> **Front-end component configuration**, make sure the Payment Form Display is the one corresponding to your integration.
