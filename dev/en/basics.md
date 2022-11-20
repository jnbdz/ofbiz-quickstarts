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



