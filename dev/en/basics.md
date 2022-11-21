# Basics | Dev | OFBiz | Quickstarts
- OFBiz is a MVC (Model View Controller)
    - Helps build web-based software quickly 
    - Keep your code organized
- Many ready-mande ERP (Enterprise Resource Planning) components

## Other documentation sources

## Download
The two ways you can download [OFBiz](https://ofbiz.apache.org/): 
1. Zip file: https://ofbiz.apache.org/download.html
    - Multiple sources: https://www.apache.org/dyn/closer.lua/ofbiz/apache-ofbiz-18.12.05.zip
    - One of the sources: https://dlcdn.apache.org/ofbiz/apache-ofbiz-18.12.05.zip
    - Ways to verify what you downloaded: https://www.apache.org/info/verification.html
2. GitHub: https://github.com/apache/ofbiz-framework
    ```bash
    git clone git@github.com:apache/ofbiz-framework.git && cd ofbiz-framework && git fetch --all && git checkout release18.12
    ```
    > https://github.com/apache/ofbiz is an old repo; do not use.
    > https://github.com/apache/ofbiz-plugins this the repo for the plugins. I document how to use them later.

## Install

### Install plugins
```bash
./gradlew createPlugin -PpluginId=ofbizDemo
```

### Hello World!
1. Edit `$OFBIZ_HOME/plugins/ofbizDemo/widget/OfbizDemoScreens.xml` and add `<label text="Hello World!! :)"/>`
```xml
<?xmlversion="1.0"encoding="UTF-8"?>
<screens xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://ofbiz.apache.org/Widget-Screen" xsi:schemaLocation="http://ofbiz.apache.org/Widget-Screen http://ofbiz.apache.org/dtds/widget-screen.xsd">
    <screen name="main">
        <section>
            <actions>
                <set field="headerItem" value="main"/><!-- this highlights the selected menu-item with name "main" -->
            </actions>
            <widgets>
                <decorator-screen name="OfbizDemoCommonDecorator" location="${parameters.mainDecoratorLocation}">
                    <decorator-section name="body">
                        <label text="Hello World!! :)"/>
                    </decorator-section>
                </decorator-screen>
            </widgets>
        </section>
    </screen>
</screens>
```
2. `$ ./gradlew loadAll ofbiz`
3. Go here https://localhost:8443/ofbizDemo
4. Login with user: **admin** password: **ofbiz**

### Creating First Database Entity (similar to a SQL Table)

> Entities == Tables

1. Defining entity `$OFBIZ_HOME/plugins/ofbizDemo/entitydef/entitymodel.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
  
<entitymodel xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="http://ofbiz.apache.org/dtds/entitymodel.xsd">
  
    <title>Entity of an Open For Business Project Component</title>
    <description>None</description>
    <version>1.0</version>
  
    <entity entity-name="OfbizDemoType" package-name="org.apache.ofbiz.ofbizdemo" title="OfbizDemo Type Entity">
        <field name="ofbizDemoTypeId" type="id"><description>primary sequenced ID</description></field>
        <field name="description" type="description"></field>
        <prim-key field="ofbizDemoTypeId"/>
    </entity>
  
    <entity entity-name="OfbizDemo" package-name="org.apache.ofbiz.ofbizdemo" title="OfbizDemo Entity">
        <field name="ofbizDemoId" type="id"><description>primary sequenced ID</description></field>
        <field name="ofbizDemoTypeId" type="id"></field>
        <field name="firstName" type="name"></field>
        <field name="lastName" type="name"></field>
        <field name="comments" type="comment"></field>
        <prim-key field="ofbizDemoId"/>
        <relation type="one" fk-name="ODEM_OD_TYPE_ID" rel-entity-name="OfbizDemoType">
            <key-map field-name="ofbizDemoTypeId"/>
        </relation>
    </entity>
  
</entitymodel>
```

2. Edit `$OFBIZ_HOME/plugins/ofbizDemo/ofbiz-component.xml`: 

```xml
<entity-resource type="model" reader-name="main" loader="main" location="entitydef/entitymodel.xml"/>
```

3. `./gradlew ofbiz`

4. https://localhost:8443/webtools/control/entitymaint

### Preparing data for an entity

1. Edit `$OFBIZ_HOME/plugins/ofbizDemo/data/OfbizDemoTypeData.xml`: 

**OfbizDemoTypeData.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<entity-engine-xml>
    <OfbizDemoType ofbizDemoTypeId="INTERNAL" description="Internal Demo - Office"/>
    <OfbizDemoType ofbizDemoTypeId="EXTERNAL" description="External Demo - On Site"/>
</entity-engine-xml>
```

**OfbizDemoDemoData.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<entity-engine-xml>
    <OfbizDemo ofbizDemoId="SAMPLE_DEMO_1" ofbizDemoTypeId="INTERNAL" firstName="Sample First 1" lastName="Sample Last 1" comments="This is test comment for first record."/>
    <OfbizDemo ofbizDemoId="SAMPLE_DEMO_2" ofbizDemoTypeId="INTERNAL" firstName="Sample First 2" lastName="Sample last 2" comments="This is test comment for second record."/>
    <OfbizDemo ofbizDemoId="SAMPLE_DEMO_3" ofbizDemoTypeId="EXTERNAL" firstName="Sample First 3" lastName="Sample last 3" comments="This is test comment for third record."/>
    <OfbizDemo ofbizDemoId="SAMPLE_DEMO_4" ofbizDemoTypeId="EXTERNAL" firstName="Sample First 4" lastName="Sample last 4" comments="This is test comment for fourth record."/>
</entity-engine-xml>
```

2. Edit `$OFBIZ_HOME/plugins/ofbizDemo/ofbiz-component.xml`: 

```xml
<entity-resource type="data" reader-name="seed" loader="main" location="data/OfbizDemoTypeData.xml"/>
<entity-resource type="data" reader-name="demo" loader="main" location="data/OfbizDemoDemoData.xml"/>
```

4. `./gradlew loadAll` or https://localhost:8443/webtools/control/EntityImport


5. To see the result: https://localhost:8443/webtools/control/entitymaint

## Form and Services
### Create a Service
[Service Engine Guide | OFBiz](https://cwiki.apache.org/confluence/display/OFBIZ/Service+Engine+Guide)

1. Edit `$OFBIZ_HOME/plugins/ofbizDemo/servicedef/services.xml`: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<services xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="http://ofbiz.apache.org/dtds/services.xsd">
  
    <description>OfbizDemo Services</description>
    <vendor></vendor>
    <version>1.0</version>
  
    <service name="createOfbizDemo" default-entity-name="OfbizDemo" engine="entity-auto" invoke="create" auth="true">
        <description>Create an Ofbiz Demo record</description>
        <auto-attributes include="pk" mode="OUT" optional="false"/>
        <auto-attributes include="nonpk" mode="IN" optional="false"/>
        <override name="comments" optional="true"/>
    </service>
  
</services>
```

2. Edit `$OFBIZ_HOME/plugins/ofbizDemo/ofbiz-component.xml`: 

```xml
<!-- service resources: model(s), eca(s) and group definitions -->
<service-resource type="model" loader="main" location="servicedef/services.xml"/>
```

3. `./gradlew ofbiz`

### Use of UI Labels (Introduction)
Internationalization is made easy.

Example **OfbizDemoUiLabels.xml**: 
```xml
<?xml version="1.0" encoding="UTF-8"?>
<resource xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://ofbiz.apache.org/dtds/ofbiz-properties.xsd">
    <property key="OfbizDemoApplication">
        <value xml:lang="en">OfbizDemo Application</value>
        <value xml:lang="zh">OfbizDemo应用程�?</value>
        <value xml:lang="zh-TW">OfbizDemo應用程�?</value>
    </property>
    <property key="OfbizDemoCompanyName">
        <value xml:lang="en">OFBiz: OfbizDemo</value>
        <value xml:lang="zh-TW">OFBiz: OfbizDemo</value>
    </property>
    <property key="OfbizDemoCompanySubtitle">
        <value xml:lang="en">Part of the Apache OFBiz Family of Open Source Software</value>
        <value xml:lang="it">Un modulo della famiglia di software open source Apache OFBiz</value>
        <value xml:lang="zh">开�?软件OFBiz的组�?部分</value>
        <value xml:lang="zh-TW">開�?軟體OFBiz的組�?部分</value>
    </property>
    <property key="OfbizDemoViewPermissionError">
        <value xml:lang="en">You are not allowed to view this page.</value>
        <value xml:lang="zh">�?�?许你�?览这个页�?�。</value>
        <value xml:lang="zh-TW">�?�?許您檢視這個�?�?�.</value>
    </property>
</resource>
```

### Create the add Form
1. `$OFBIZ_HOME/plugins/ofbizDemo/widget/OfbizDemoForms.xml`: 

**OfbizDemoForms.xml**: 
```xml
<?xml version="1.0" encoding="UTF-8"?>
<forms xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns="http://ofbiz.apache.org/Widget-Form" xsi:schemaLocation="http://ofbiz.apache.org/Widget-Form http://ofbiz.apache.org/dtds/widget-form.xsd">
  
    <form name="AddOfbizDemo" type="single" target="createOfbizDemo">
        <!-- We have this utility in OFBiz to render form based on service definition.
             Service attributes will automatically lookedup and will be shown on form
        -->
        <auto-fields-service service-name="createOfbizDemo"/>
        <field name="ofbizDemoTypeId" title="${uiLabelMap.CommonType}">
            <drop-down allow-empty="false" current-description="">
                <!---We have made this drop down options dynamic(Values from db) using this -->
                <entity-options description="${description}" key-field-name="ofbizDemoTypeId" entity-name="OfbizDemoType">
                    <entity-order-by field-name="description"/>
                </entity-options>
            </drop-down>
        </field>
        <field name="submitButton" title="${uiLabelMap.CommonAdd}"><submit button-type="button"/></field>
    </form>
</forms>
```

2. Adding Form Location to the Main Screen.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<screens xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://ofbiz.apache.org/Widget-Screen" xsi:schemaLocation="http://ofbiz.apache.org/Widget-Screen http://ofbiz.apache.org/dtds/widget-screen.xsd">
  
    <screen name="main">
        <section>
            <actions>
                <set field="headerItem" value="main"/> <!-- this highlights the selected menu-item with name "main" -->
            </actions>
            <widgets>
                <decorator-screen name="main-decorator" location="${parameters.mainDecoratorLocation}">
                    <decorator-section name="body">
                        <screenlet title="Add Ofbiz Demo">
                            <include-form name="AddOfbizDemo" location="component://ofbizDemo/widget/OfbizDemoForms.xml"/>
                        </screenlet>
                    </decorator-section>
                </decorator-screen>
            </widgets>
        </section>
    </screen>
</screens>
```

3. Edit `widget/OfbizDemoScreens.xml`: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<screens xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://ofbiz.apache.org/Widget-Screen" xsi:schemaLocation="http://ofbiz.apache.org/Widget-Screen http://ofbiz.apache.org/dtds/widget-screen.xsd">
  
    <screen name="main">
        <section>
            <actions>
                <set field="headerItem" value="main"/> <!-- this highlights the selected menu-item with name "main" -->
            </actions>
            <widgets>
                <decorator-screen name="main-decorator" location="${parameters.mainDecoratorLocation}">
                    <decorator-section name="body">
                        <screenlet title="Add Ofbiz Demo">
                            <include-form name="AddOfbizDemo" location="component://ofbizDemo/widget/OfbizDemoForms.xml"/>
                        </screenlet>
                    </decorator-section>
                </decorator-screen>
            </widgets>
        </section>
    </screen>
</screens>
```

### Controller Entry for Form

> IMPORTANT! You will need this for the form to call the right service.

1. Edit `$OFBIZ_HOME/plugins/ofbizDemo/webapp/ofbizDemo/WEB-INF/controller.xml`: 

```xml
<request-map uri="createOfbizDemo">
    <security https="true" auth="true"/>
    <event type="service" invoke="createOfbizDemo"/>
    <response name="success" type="view" value="main"/>
</request-map>
```

2. Go to https://localhost:8443/ofbizDemo/

### Create a Find Form
Find form so that you can search the data from this plugin.

1. Edit `widget/OfbizDemoForms.xml`: 

```xml
<form name="FindOfbizDemo" type="single" target="FindOfbizDemo" default-entity-name="OfbizDemo">
    <field name="noConditionFind"><hidden value="Y"/> <!-- if this isn't there then with all fields empty no query will be done --></field>
    <field name="ofbizDemoId" title="${uiLabelMap.OfbizDemoId}"><text-find/></field>
    <field name="firstName" title="${uiLabelMap.OfbizDemoFirstName}"><text-find/></field>
    <field name="lastName" title="${uiLabelMap.OfbizDemoLastName}"><text-find/></field>
    <field name="ofbizDemoTypeId" title="${uiLabelMap.OfbizDemoType}">
        <drop-down allow-empty="true" current-description="">
            <entity-options description="${description}" key-field-name="ofbizDemoTypeId" entity-name="OfbizDemoType">
                <entity-order-by field-name="description"/>
            </entity-options>
        </drop-down>
    </field>
    <field name="searchButton" title="${uiLabelMap.CommonFind}" widget-style="smallSubmit"><submit button-type="button" image-location="/images/icons/magnifier.png"/></field>
</form>
  
<form name="ListOfbizDemo" type="list" list-name="listIt" paginate-target="FindOfbizDemo" default-entity-name="OfbizDemo" separate-columns="true"
    odd-row-style="alternate-row" header-row-style="header-row-2" default-table-style="basic-table hover-bar">
    <actions>
       <!-- Preparing search results for user query by using OFBiz stock service to perform find operations on a single entity or view entity -->
       <service service-name="performFind" result-map="result" result-map-list="listIt">
           <field-map field-name="inputFields" from-field="ofbizDemoCtx"/>
           <field-map field-name="entityName" value="OfbizDemo"/>
           <field-map field-name="orderBy" from-field="parameters.sortField"/>
           <field-map field-name="viewIndex" from-field="viewIndex"/>
           <field-map field-name="viewSize" from-field="viewSize"/>
        </service>
    </actions>
    <field name="ofbizDemoId" title="${uiLabelMap.OfbizDemoId}"><display/></field>
    <field name="ofbizDemoTypeId" title="${uiLabelMap.OfbizDemoType}"><display-entity entity-name="OfbizDemoType"/></field>
    <field name="firstName" title="${uiLabelMap.OfbizDemoFirstName}" sort-field="true"><display/></field>
    <field name="lastName" title="${uiLabelMap.OfbizDemoLastName}" sort-field="true"><display/></field>
    <field name="comments" title="${uiLabelMap.OfbizDemoComment}"><display/></field>
</form>
```

> @TODO - More to add.

## Services using other engines
This is for business logic.

### Service in Java
1. Edit `$OFBIZ_HOME/plugins/ofbizDemo/servicedef/services.xml`: 

```xml
<service name="createOfbizDemoByJavaService" default-entity-name="OfbizDemo" engine="java"
        location="com.companyname.ofbizdemo.services.OfbizDemoServices" invoke="createOfbizDemo" auth="true">
    <description>Create an Ofbiz Demo record using a service in Java</description>
    <auto-attributes include="pk" mode="OUT" optional="false"/>
    <auto-attributes include="nonpk" mode="IN" optional="false"/>
    <override name="comments" optional="true"/>
</service>
```

2. Create package "com.companyname.ofbizdemo.services"

> `src/main/java/com/companyname/ofbizdemo/services`

3. Create file `OfbizDemoServices.java`: 

```java
package com.companyname.ofbizdemo.services;
import java.util.Map;

import org.apache.ofbiz.base.util.Debug;
import org.apache.ofbiz.entity.Delegator;
import org.apache.ofbiz.entity.GenericEntityException;
import org.apache.ofbiz.entity.GenericValue;
import org.apache.ofbiz.service.DispatchContext;
import org.apache.ofbiz.service.ServiceUtil;

public class OfbizDemoServices {

    public static final String module = OfbizDemoServices.class.getName();

    public static Map<String, Object> createOfbizDemo(DispatchContext dctx, Map<String, ? extends Object> context) {
        Map<String, Object> result = ServiceUtil.returnSuccess();
        Delegator delegator = dctx.getDelegator();
        try {
            GenericValue ofbizDemo = delegator.makeValue("OfbizDemo");
            // Auto generating next sequence of ofbizDemoId primary key
            ofbizDemo.setNextSeqId();
            // Setting up all non primary key field values from context map
            ofbizDemo.setNonPKFields(context);
            // Creating record in database for OfbizDemo entity for prepared value
            ofbizDemo = delegator.create(ofbizDemo);
            result.put("ofbizDemoId", ofbizDemo.getString("ofbizDemoId"));
            Debug.log("==========This is my first Java Service implementation in Apache OFBiz. OfbizDemo record created successfully with ofbizDemoId: "+ofbizDemo.getString("ofbizDemoId"));
        } catch (GenericEntityException e) {
            Debug.logError(e, module);
            return ServiceUtil.returnError("Error in creating record in OfbizDemo entity ........" +module);
        }
        return result;
    }
}
```

4. `./gradlew ofbiz`: 

5. https://localhost:8443/webtools/control/runService or update the controller `$OFBIZ_HOME/plugins/ofbizDemo/webapp/ofbizDemo/WEB-INF/controller.xml`: 

```xml
<request-map uri="createOfbizDemoByJavaService">
    <security https="true" auth="true"/>
    <event type="service" invoke="createOfbizDemoByJavaService"/>
    <response name="success" type="view" value="main"/>
</request-map>
```
