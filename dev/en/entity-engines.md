# Entity Engine | EN | Dev | OFBiz
## Important Paths
- `ofbiz-framework/framework/entity`
    - `ofbiz-framework/framework/entity/config`
        - `ofbiz-framework/framework/entity/config/entityengine.xml`
    - `ofbiz-framework/framework/entity/dtd` - XSD files for the entity XML configuration files.
    - `ofbiz-framework/framework/entity/entitydef` - 
    - `ofbiz-framework/framework/entity/fieldtype` - Each databse type (e.g.: Apache Derby, PostgreSQL, Oracle, MySQL, etc) has one, it defines the what data types can used in the field element `type` attribute: `<field name="changedDate" type="date-time"></field>` (also maps it to Java data types: `<field-type-def type="date-time" sql-type="TIMESTAMP" java-type="java.sql.Timestamp"/>`).
    - `ofbiz-framework/framework/entity/minilang` - 
    - `ofbiz-framework/framework/entity/src` - OFBiz code for the **Entity Engine**. There is also a `src/asciidoc` that contains `.adoc` documentation on the engine.
    - `ofbiz-framework/framework/entity/testdef` - 
    - `ofbiz-framework/framework/entity/ofbiz-component.xml` - 
