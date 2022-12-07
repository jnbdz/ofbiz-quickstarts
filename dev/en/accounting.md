# Accounting | Dev | OFbiz | Quickstarts
## CLASSES
Source: https://nightlies.apache.org/ofbiz/stable/javadoc/

- `org.apache.ofbiz.accounting`
    - `org.apache.ofbiz.accounting.GlEvents`
        - `public static java.lang.String createReconcileAccount(HttpServletRequest request, HttpServletResponse response)`
            - Unknown
    - `org.apache.ofbiz.accounting.agreement`
        - `org.apache.ofbiz.accounting.agreement.AgreementServices`
            - `getCommissionForProduct(DispatchContext ctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - Determines commission receiving parties (*maybe useful for an online-marketplace*) (used for sellers) and amounts for the provided product, price, and quantity
                - Returns: Map with the result of the service, the output parameters. commissions List List of Maps each containing partyIdFrom String commission paying party partyIdTo String commission receiving party commission BigDecimal Commission days Long term days currencyUomId String Currency productId String Product Id
    - `org.apache.ofbiz.accounting.finaccount`
        - `org.apache.ofbiz.accounting.finaccount.FinAccountPaymentServices`
            - FinAccountPaymentServices - Financial account used as payment method
            - Methods: 
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountCapture(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountDeposit(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountPreAuth(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountRefund(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountReleaseAuth(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountReplenish(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	finAccountWithdraw(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
        - `org.apache.ofbiz.accounting.finaccount.FinAccountProductServices`
            - `FinAccountProductServices - Financial Accounts created from product purchases (i.e. gift certificates)`
            - Methods: 
                - `static java.util.Map<java.lang.String, java.lang.Object>	createPartyFinAccountFromPurchase(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
        - `org.apache.ofbiz.accounting.finaccount.FinAccountServices`
            - Methods: 
                - `static java.util.Map<java.lang.String, java.lang.Object>	checkFinAccountBalance(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	checkFinAccountStatus(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	createAccountAndCredit(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	createFinAccountForStore(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`
                - `static java.util.Map<java.lang.String, java.lang.Object>	refundFinAccount(DispatchContext dctx, java.util.Map<java.lang.String, java.lang.Object> context)`

## Paypal
1. To activate you need to take out: `org/apache/ofbiz/accounting/thirdparty/paypal/PayPalServices.java` from the list of `excludedJavaSources`. So that the Paypal service Java code can be loaded.

### Files
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
- `applications/accounting/src/main/java/org/apache/ofbiz/accounting/thirdparty/verisign/PayflowPro.java`
- `applications/order/src/main/java/org/apache/ofbiz/order/order/OrderReturnServices.java`
- `applications/order/src/main/java/org/apache/ofbiz/order/shoppingcart/CheckOutEvents.java`
- `applications/order/src/main/java/org/apache/ofbiz/order/shoppingcart/CheckOutHelper.java`
- `applications/order/src/main/java/org/apache/ofbiz/order/thirdparty/paypal/ExpressCheckoutEvents.java`
- `applications/accounting/config/AccountingEntityLabels.xml`
- `applications/accounting/config/AccountingErrorUiLabels.xml`
- `applications/accounting/config/AccountingUiLabels.xml`
- `applications/accounting/src/main/java/org/apache/ofbiz/accounting/thirdparty/paypal/PayPalEvents.java`
- `applications/accounting/src/main/java/org/apache/ofbiz/accounting/thirdparty/paypal/PayPalServices.java`
- `applications/order/src/main/java/org/apache/ofbiz/order/order/OrderReturnServices.java`

### Templates
- `applications/order/template/entry/CheckoutOptions.ftl`
- `applications/order/template/entry/CheckoutPayment.ftl`
- `applications/order/template/order/OrderPaymentInfo.ftl`

