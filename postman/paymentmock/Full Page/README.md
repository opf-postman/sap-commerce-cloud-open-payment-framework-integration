# Introduction
Learn how to integrate a Payment Mock Gateway to open payment framework using Postman collection.

## Procedure
1.	Download the Postman collection of Payment Mock Gateway from [Open Payment Framework GitHub Repo](https://github.com/opf-postman/commerce-cloud-open-payment-integration/tree/main/postman/paymentmock/Full%20Page).
   
2.	Create a Payment Mock integration in OPF Payment Mock swagger UI. The URL for test environment is: <https://opf-iss-d0.opf.commerce.stage.context.cloud.sap/opf-payment-mock/api/swagger-ui/index.html>. 
   
    a.) Locate the Create Merchant Account Group API.
   
    b.) Configure the request body.
   
    c.) Execute the API call.
  	
   	The following is the response example retrieved:
  	
  	``{
  "merchantId": "2a263ef2-13f2-4561-b05c-ebde41f08d13",
  "apiKey": "uBucbJJSyRhQ93hTdaSkm6M/cfSIWSbI1MD69fFkSWQ=",
  "enableOverCapture": false,
  "overCapturePercentage": 10
  }
``
  	
    d.) Note down the ``merchantId`` and ``apiKey``. They cannot be retrieved again.

3. Create a payment integration for Payment Mock in the open payment framework workbench. For detailed instructions, see [Creating Payment Integration
](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/852d7d8437254529828351dbde217118.html?state=DRAFT).

4. Under the **General Information** section of the **Integration details** tab, copy the Notification URL for later use.

**Remember**
To ensure you receive timely updates on transactions and other important events, this URL is essential for configuring event notifications from Payment Mock.

5. Click **Configure** under the **Configuration** section.

6. Set the Merchant ID of the payment account using the value retrieved in step 2, and select a settlement method for your payment integration.
7. Click **Save**.
8. Note down the ``integrationId`` and the ``configurationId``. These two values identify the payment integration, and can be found in the top left of your configuration details page.
9. Edit the Postman Collection variables in the Postman app.

   a.) Import the two files at the same time to Postman.

   b.) Make sure to select the environment for Mock Gateway.

   c.) Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Payment Mock Gateway Test Account unique values.
   
| Name                                                                                 | Description                                                  
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.  |                  
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.| 
| service                                                                              | The ``service`` is the name of your OPF service in specific environment. This will usually just be ``opf``. |                 
| integrationId                                                                       | The ``integrationId`` and ``configurationId`` values that identify the payment integration can be found in the top left of your configuration details page.|                  
| configurationId                                                                            | The ``integrationId`` and ``configurationId`` values that identify the payment integration can be found in the top left of your configuration details page.|                                                                          
| authentication_inbound_basic_auth_username                                           | ``username``|                  
| authentication_inbound_basic_auth_password                                           | ``password``|                  
| capturePattern                                                                       | ``CAPTURE_PER_SHIPMENT``|                  
| supportOverCapture                                                                   | ``true``|                  
| enableOverCapture                                                                    | ``true``|                  
| authorizationTimeoutDays                                                             | 7   |                  
| apiKey                                                                               | The ``apiKey`` noted down in step 2.|                  
| host                                                                                 | The base URL of your tenant account in OPF payment mock service.|                  
              
10. Save and run the Postman Collection.
   
11. Set notification URL in the Payment Mock Swagger UI.
   
   a.) Locate the **Create Notification Configuration** API.
   
   b.) Fill the request parameters ``merchantId`` and ``apiKey`` use the value retrieved in step 2.
   
   c.) Set the url in the request body noted down in step 4.
   
   d.) Set the ``basicAuth.username`` and ``basicAuth.password`` to the ``authentication_inbound_basic_auth_username`` and ``authentication_inbound_basic_auth_password`` in step 5.
   
   e.) Execute the API call.

12. Validate the configuration in Open Payment Framework Workbench

   a.) Log in to the open payment framework workbench.
   
   b.) Click **Payment Integrations** in the left navigation bar.
   
   c.) Navigate to **Payment Integrations** -> **(your Adyen integration)** -> **Integration Details**.
   
   d.) In the **Configuration section**, click **Show Details** to go to the configuration details page.
   
   e.) In the **Settlement Method** section, make sure the right option is populated depending on your integration.
   
   f.) In the **Authorization** section, click **Edit** to go to the authorization details page.
   
   g.) In **Authorization** -> **Front-end component configuration**, make sure the Payment Form is the one corresponding to your integration.


      





