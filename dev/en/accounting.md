# Accounting | Dev | OFbiz | Quickstarts
## Paypal
1. To activate you need to take out: `org/apache/ofbiz/accounting/thirdparty/paypal/PayPalServices.java` from the list of `excludedJavaSources`. So that the Paypal service Java code can be loaded.

## Files
- `applications/accounting/src/main/java/org/apache/ofbiz/accounting/thirdparty/paypal/PayPalServices.java` is the path to the Paypal service.
- `applications/accounting/servicedef/services_paymentmethod.xml`
- `applications/accounting/servicedef/services_paymentgateway.xml`
- `applications/accounting/servicedef/services_paypal.xml`
- `applications/accounting/src/main/java/org/apache/ofbiz/accounting/thirdparty/paypal/PayPalEvents.java`
- `applications/datamodel/data/demo/AccountingDemoData.xml` - Payment gateway configurations.
- `applications/datamodel/entitydef/accounting-entitymodel.xml` - DB entity models:
    - PaymentGatewayPayPal 
    - PayPalPaymentMethod 
- `applications/order/src/main/java/org/apache/ofbiz/order/shoppingcart/CheckOutHelper.java`
- `applications/commonext/data/OfbizSetupProductStoreData.xml`
- `applications/product/minilang/product/test/GroupOrderTest.xml`
- `applications/accounting/config/payment.properties`

### Templates
- `applications/order/template/entry/CheckoutOptions.ftl`
- `applications/order/template/entry/CheckoutPayment.ftl`
- `applications/order/template/order/OrderPaymentInfo.ftl`
