# json-kotlin-annotations

Annotations for Kotlin JSON serialization and deserialization.

These classes provide a means of customizing the operation of the
[`json-kotlin`](https://github.com/pwall567/json-kotlin) library.
They were formerly part of `json-kotlin`, but have been split out into a separate project to allow them to be used
independently of the original project.

## Annotations

### `@JSONAllowExtra`

This annotation is applied to classes to indicate that extra properties in an object are allowed (and ignored) on
deserialization.

### `@JSONIgnore`

This annotation is applied to properties and data class constructor parameters, and it indicates that the relevant
property is to be ignored during serialization and deserialization.
Note that a constructor parameter annotated with `@JSONIgnore` will need to have a default value supplied if it is to be
deserialized.

### `@JSONIncludeAllProperties`

This annotation is applied to classes to indicate that all properties in the class are to be included in
auto-serialization even if `null`.

### `@JSONIncludeIfNull`

This annotation is applied to individual properties and data class constructor parameters to indicate that the relevant
property is to be included in auto-serialization even if `null`.

### `@JSONName`

This annotation is applied to properties and data class parameters, and it supplies the name to be used in place of the
property name for auto-serialization and deserialization.

It takes a single parameter `name` - the name to be used.

## Alternative Annotations

In many cases, existing code will have annotations for the purposes above already in the code.
The `json-kotlin` library can be configured to use these annotations from other libraries - see the `JSONConfig` class.

## Dependency Specification

The latest version of the library is 1.0.1, and it may be obtained from the Maven Central repository.

### Maven
```xml
    <dependency>
      <groupId>net.pwall.json</groupId>
      <artifactId>json-kotlin-annotations</artifactId>
      <version>1.0.1</version>
    </dependency>
```
### Gradle
```groovy
    implementation 'net.pwall.json:json-kotlin-annotations:1.0.1'
```
### Gradle (kts)
```kotlin
    implementation("net.pwall.json:json-kotlin-annotations:1.0.1")
```

Peter Wall

2020-04-18
