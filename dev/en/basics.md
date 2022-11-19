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


