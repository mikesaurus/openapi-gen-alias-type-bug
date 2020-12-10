# openapi-generator Alias Type Bug

## Summary
This is an example project to demonstrate a openapi-generator bug that causes a compilation error when 
setting the `generateAliasAsModel` option to `true`.

### Expected Behavior
When generating client code with openapi-generator and the `generateAliasAsModel` option set to `true`, model properties 
of alias model types are initialized to null or to a new instance of the alias object type and the code compiles.

Expected code:
```java
public class StandardModelClass {
  private MapAliasModelClass mapAliasModel = null;
}
```
or
```java
public class StandardModelClass {
  private MapAliasModelClass mapAliasModel = new MapAliasModelClass();
}
```

### Actual Behavior
When generating client code with openapi-generator and the `generateAliasAsModel` option set to `true`, model properties 
of alias types are initialized to a new instance of the base object type, not the alias object type, and compilation fails.

Actual code:
```java
public class StandardModelClass {
  private MapAliasModelClass mapAliasModel = new HashMap<String, String>();
}
```

## Building
Configured for Maven 3 and Java 11.  Change the <java.version> POM property if using a different Java version (and the 
local jenv version if using jenv).

To build, run `mvn install` from the project root. This will result in the following compilation error:

```
org/example/service/v1/model/Person.java:[76,43] incompatible types: java.util.HashMap<java.lang.String,java.util.List<java.lang.String>> cannot be converted to org.example.service.v1.model.Relationships
```
