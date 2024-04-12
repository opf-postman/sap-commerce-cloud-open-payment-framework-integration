[Draft]

We integrate worldpay with WPG(worldwide payment gateway)
WPG doc: https://developerengine.fisglobal.com/apis/wpg

Before you import this to your system, you should create your payment acccount in opf workbench

important variables in environment configuration:
authentication_outbound_basic_auth_username_export_10: the username of basic auth to call worldpay api
authentication_outbound_basic_auth_password_export_10: the password of basic auth to call worldpay api
installationId: after you login into merchant admin interface, you can get from INTEGRATION->Installations
merchantCode: ditto
