## Introduction ##

The Postman Collection enables a [Braintree Hosted Fields](https://developer.paypal.com/braintree/docs/start/hosted-fields)) Payment Form to be used to Take Payments through OPF. 

The integration supports:

* Authorization of Card Payments using PCI SAQ-A Braintree Hosted Fields using the OPF "Hosted Fields" UX Pattern
* Deferred Capture (Single Capture per Order)
* Refunds

## Known Issues ##
* Refunds currently fail if initiated before they are sent to Settlement
** Workaround manual process of refunding in Braintree based on failed transactions in OPF, then manual update of stuck OPF transaction.
* Only supports a Single deferred Capture request per order
* Reversal not supported
* Paypal not tested


## Setup Instructions ##

### Summary ###
To import the [Braintree Hosted Field Postman Collection](mapping_configuration.json) this page will take you through the following steps

a) Sign up for a Braintree Sandbox Account
b) Create a Merchant Account Group in OPF Workbench.
c) Set up Your Brasintree Sandbox Account to work with OPF.
d) Prepare the [Postman Environment](environment_configuration.json) file so the collection can be imported with all your OPF Tenant and Braintree Sandbox Account unique values. 


### Create a Braintree Account ###
You can sign up for a free Braintree Sandbox Account at https://www.braintreepayments.com/sandbox

### Creating the Merchant Account Group ###
Ceate a new Account Group in the OPF Workbench and set the Merchant ID.




