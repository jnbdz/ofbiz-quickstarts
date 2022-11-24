# Services | EN | OFBiz
- Context-aware Service Engine
    - Used across the entire framework
    - Or externally through network interface
    - Consumers need not to concern themselves with the location of the Service or other details related to the implementation of the service
- Multiple invocation methods
    - inline or synchronous with the calling program
    - out-of-band or asynchronous from the the caller's processing logic
    - Scheduled job
- Chaining of Services
    - Event-driven Service
    - Services can be configured to be invoked based on external events or triggers
    - The Service can also call other Service(s) based on the additional triggering Events and/or conditins
    - Services chanin together form: **Service Event Condition Action(s) or SECAs**
- Job scheduler
    - Calendar lookups
    - Frequency
    - Interval timing
- Selectable input and output validations
    - Confgured parameter types
    - Authentication and authorization (login processing with OFBiz)
    - Localization preservation across Service calls

> OFBiz Service Engine uses the factory pattern.

- Third-Party execution engines including, but not limited to: 
    - Java
    - Groovy
    - JavaScript
    - JPython
    - OFBiz "simple" Service (based on the OFBiz Mini-Language)
    - The services can be pretty much be written in any language (offloading)

> The Service Engine can be called from anywhere in the framework.

> Many services come out of the box with OFBiz

![OFBiz Service Engine](../assets/OFBiz-Service-engine.svg)

## Managing existing OFBiz Services
- https://localhost:8443/webtools/control/ServiceList
- Access by privileged users
- Control via OFBiz WebTools toolkit

> It is possible to navigate by filtering by **alphabetic** order, **Service Name**, **Engine Name** (Service Engine Type), what is **Invoke**, **Location**.

- Asynchronous and scheduled Service request
    - Managed by OFBiz job scheduler
    - `~/framework/service/config/serviceengine.xml`
    - Threads run from one or more thread "pools"
    - 

## Calling a Service from an HTML form
- By setting the HTML form *action* element to point to the URL of a `controller.xml` request-map that resolves to either an OFBiz Event that calls a Service or directly to a Service

The example here uses the WebTool's **Run Service** HTML form to invoke a Service.

In this example the *testScv* will be used.

To view the results of *testScv* you can use `tail` command on the OFBIz log: `tail -f ${OFBIZ_HOME}/runtime/ofbiz.log`

### To call a service
1. Go to **Run Service** WebTools: https://localhost:8443/webtools/control/runService
2. In **Run Service**, enter **testScv** in the field labeled **Service**
3. **Pool** field keeps its default value
4. Click on **Submit** it will redirect to the **Schedule Job** page
5. On the **Schedule Job** page, input in the any values for the requested form fields (e.g.: 8888.222).
6. Click **Submit** (*testScv* is called)
7. Inspect the `ofbiz.log` file you should see the number you have input in

### Explanation
1. In a HTML form an *action* attribute URL for the target Service
2. Adding to a `controller.xml` a entry with a request-map for the target Service that matches the HTML form's *action* URL.

Example for **Run Service**: 
```html
<form name="scheduleForm" method="POST" action="/webtools/control/scheduleService">
    <input type="text" name="testScv" />
    <!-- and more stuff -->
</form>
```

```xml
<request-map uri="scheduleService">
    <security https="true" auth="true"/>
    <response>
```

## Calling asynchronous Services from HTML forms

## Calling a Service many times from an HTML form

## Creating a new Service definition file

## Creating a new Service definition

## Implementing Services

## Defining Service attributes (INPUT/OUTPUT)

## Service Event Condition Actions

## Service groups

## Handling Service errors

## Writing Groovy Services

## Mail Event Conditions Actions

## Entity Event Conditions Actions

