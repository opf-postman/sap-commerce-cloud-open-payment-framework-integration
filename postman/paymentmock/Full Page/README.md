# Introduction
Learn how to integrate a Mock Gateway to SAP Commerce Cloud using Postman Collection.

## Procedure
1.	Download the postman collection of mock provider from [Open Payment Framework GitHub Repo](https://github.com/opf-postman/commerce-cloud-open-payment-integration/tree/main/postman/paymentmock/Full%20Page).
   
2.	Create a Payment Mock merchant account group in OPF Payment Mock swagger UI, do the following to create a new merchant account group.
   
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
   b.) 
   
6. Edit the Postman Collection.
7. Save and run the Postman Collection.
8. Set notification URL in the Payment Mock Swagger UI.






      





