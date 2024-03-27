# SAP Commerce Cloud, open payment framework, opf payment mock provider
Learn how to integrate a Mock Gateway to SAP Commerce Cloud using Postman Collection.

## Before Importing
Create a merchant account in the OPF payment mock provider. The merchant acccount ID should used in the account ID created in OPF workbench.

## Procedure
1.	Download the postman collection of mock provider from [Open Payment Framework GitHub Repo](https://github.com/opf-postman/commerce-cloud-open-payment-integration/tree/main/postman/paymentmock/Full%20Page).
   
2.	Create a Payment Mock merchant account in OPF Payment Mock swagger UI, do the following to create a new merchant account.
   a.) Locate the Create Merchant account API.
   b.) Configure the request body.
   c.) Execute the API call.
  	The following is the response example retrieved:
  	``{
  "merchantId": "2a263ef2-13f2-4561-b05c-ebde41f08d13",
  "apiKey": "uBucbJJSyRhQ93hTdaSkm6M/cfSIWSbI1MD69fFkSWQ=",
  "enableOverCapture": false,
  "overCapturePercentage": 10
   }``
  d.) Note down the merchantId and apiKey. They cannot be retrieved again.

3. Create a Merchant Account Group in the open payment framework workbench. Refer to Create Merchant Account for detailed instructions.
4. Click **Configure** of the Test Payment account in the Merchant Account Group created in step 3.
5. Edit the Postman Collection.
6. Save and run the Postman Collection.
7. Set notification URL in the Payment Mock Swagger UI.






      





