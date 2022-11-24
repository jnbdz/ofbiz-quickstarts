# Services | EN | OFBiz
> Official documentation: https://cwiki.apache.org/confluence/display/OFBIZ/Service+Engine+Guide

> *Services require input parameters to be in a Map and the results are returned in a Map as well. This is nice since a Map can be serialized and stored or passed via HTTP (SOAP).* ~ OFBiz Doc

> Services are defined: Service Definition and assigned to a specific Service Engine.

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

When submitted action = `webtools/control/scheduledService` is caught by WebTools controller servlet with `controller.xml` file to determine how to handle this request.

```xml
<request-map uri="scheduleService">
    <security https="true" auth="true"/>
    <response>
```

The URL request is mapped to an OFBiz Event called `scheduleService`.

Inside this event a call is made to the Service Engine to call *testScv* using the Java Service implementation engine as shown in the *testScv* Service defintion file.

Once *testScv* is executed processing control returns to OFBiz request handler. Following that step the webapp is acalled as configured in the `controller.xml`.

## Calling asynchronous Services from HTML forms
- WebTools and HTML forms can also be used to run a Service asynchronously either one time or a recurring basis.
- https://localhost:8443/webtools/control/scheduleJob

1. **Service** form field enter in **testScv**
2. **Job** is left empty (a unique name will be picked)
3. Pick a date in **Start Date/Time**

- **Pool** - (default: one thread pool named **pool**) for more thread pools: `serviceengine.xml`
- **Frequency** - A frequency of **None** tells OFBiz to run this Service once
- **Interval** - To indicate how many times to invoke the Service
- **Count** - -1 indicates forever

4. Click **Submit** will return **Service Parameters** form (allows the called to provide other input parameters to the Service)
5. Add INPUT parameter: 
    - **defaultValue (Double)**
    - **message (String)**
6. Submit the **Service Parameters** (*testScv* will be scheduled to run at the specified time)

The calling program will run asynchronously with Scheduled Services.

Each scheduled Service is assigned a unique job identifier (`jobId`) and executed pool by the job scheduler.

The control is returned to the calling program after the Service is scheduled for execution.

> Using **Job List** web page you will find the scheduled jobs. You can also search those **Job List** the result will be in the **Job List Search Results** page.

> *testScv* only writes output to the logfile.

## Calling a Service many times from an HTML form
You might need to call a Service multiple times from a single HTML form for each row in a form. Using `service-multi` event type defined for the `controller.xml` request-map entry of the target Service.

1. Event type `service-multi` within the `controller.xml` request-map entry.
2. When using the Form Widget add a line similar to the one following the Form Widget definition. The `list-name` is the name of the list that is generating multiple rows for the HTML form: 
```html
<form name="someFormName" type="multi" use-row-submit="true" list-name="someList" target="someServiceName" ...
</form>
```
3. When using FreeMarker template: 
```html
<form name="mostrecent" mode="POST" action="<@ofbizUrl>someService</@ofbizUrl>"/>
   <#assign row=0/>
   <#list someList as listItem>
   <#-- HTML removed for reading clarity.
        Each row has a unique input name associated with it
        allowing this single Form to be submitted to the
       "someServiceName" Service from each row -->
   <input type="radio" name="someFormField_o_${row}" value="someValue" checked/>
   <input type="radio" name="someFormField_o_${row}" value="someValue"/>
   </#list>
</form>
```

- `service-multi` is a Event type provides a convenient shortcut for coding HTML forms that are embedded within lists
- Each item in the list is automatically conveted to a unique `form` field so that a single Service may be called from any row within a list

## Creating a new Service definition file
- Service definition are in XML document are located in a Component's `servicedef` directoryi (`ofbiz-component.xml`).

To define a new service definition file: 


## Creating a new Service definition

## Implementing Services

## Defining Service attributes (INPUT/OUTPUT)

## Service Event Condition Actions

## Service groups

## Handling Service errors

## Writing Groovy Services

## Mail Event Conditions Actions

## Entity Event Conditions Actions

