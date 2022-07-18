# Basics | OFBiz | Quickstarts
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
