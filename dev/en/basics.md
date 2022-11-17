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
1. Defining entity

