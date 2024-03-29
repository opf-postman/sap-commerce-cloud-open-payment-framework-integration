# Introduction
Learn how to integrate a Mock Gateway to SAP Commerce Cloud using Postman Collection.

## Procedure
1.	Download the postman collection of mock provider from [Open Payment Framework GitHub Repo](https://github.com/opf-postman/commerce-cloud-open-payment-integration/tree/main/postman/paymentmock/Full%20Page).
   
2.	Create a Payment Mock merchant account group in OPF Payment Mock swagger UI. The URL for test environment is: <https://opf-iss-d0.opf.commerce.stage.context.cloud.sap/opf-payment-mock/api/swagger-ui/index.html>. 
   
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

3. Create a Merchant Account Group in the open payment framework workbench. Refer to [Create Merchant Account](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/0996ba68e5794b8ab51db8d25d4c9f8a/20a64f954df1425391757759011e7e6b.html)  for detailed instructions.
4. Click **Configure** of the Test Payment account in the Merchant Account Group created in step 3.

   a.) Note down the ``accountId`` and the ``accountGroupId``. These two values identify the merchant account group, and can be found in the top left of your merchant configuration.
   
   b.) In the **General configuration** tab, set the Merchant ID of the Payment account to be the value which retrieved in step 2.

   c.) In the **Notification** tab, note down the URL for notification.
   
5. Edit the Postman Collection in the Postman app.

   a.) Import the two files at the same time to Postman.

   b.) Make sure to select the environment for Mock Gateway.

   c.) Edit the Postman environment file so the collection can be imported with all your OPF Tenant and Mock Gateway Test Account unique values.
   
| Name                                                                                 | Description                                                  
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| token                                                                                | Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit. **IMPORTANT**: Ensure the value is prefixed with Bearer. e.g. Bearer {{token}}.  |                  
| rootURL                                                                              | The ``rootUrl`` is the ``BASE URL`` of your OPF tenant.  E.g. if your workbench/OPF cockpit url was this … https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench. The base Url would be: https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.|                  
| accountGroupId                                                                       | The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.|                  
| accountId                                                                            | The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.|                                                                          
| authentication_inbound_basic_auth_username                                           | ``username``|                  
| authentication_inbound_basic_auth_password                                           | ``password``|                  
| capturePattern                                                                       | ``CAPTURE_PER_SHIPMENT``|                  
| supportOverCapture                                                                   | ``true``|                  
| enableOverCapture                                                                    | ``true``|                  
| authorizationTimeoutDays                                                             | 7   |                  
| apiKey                                                                               | The apiKey noted down in step 2.|                  
| host                                                                                 | The base URL of your tenant account in OPF payment mock service.|                  
              
6. Save and run the Postman Collection.
   
7. Set notification URL in the Payment Mock Swagger UI.
   
   a.) Locate the **Create Notification Configuration** API.
   
   b.) Fill the request parameters ``merchantId`` and ``apiKey`` use the value retrieved in step 2.
   
   c.) Set the url in the request body noted down in step 4.
   
   d.) Set the ``basicAuth.username`` and ``basicAuth.password`` to the ``authentication_inbound_basic_auth_username`` and ``authentication_inbound_basic_auth_password`` in step 5.
   
   e.) Execute the API call.

8. Validate the configuration in Open Payment Framework Workbench.

   a.) Go to **Payment Integrations**-> **Merchant account** and click **Configure**.

      **Note**
      If you are testing the integration, you must select the Test payment account.

    b.) The **General configuration** -> **Variables** values must be populated.

    c.) In Settlement method, make sure the right option is selected depending on your integration.
   
    d.) In **Authorization** -> **Front-end component configuration**, make sure the Payment Form Display is the one corresponding to your integration.





      





