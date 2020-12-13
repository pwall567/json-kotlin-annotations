# json-kotlin-annotations

[![Build Status](https://travis-ci.org/pwall567/json-kotlin-annotations.svg?branch=master)](https://travis-ci.org/pwall567/json-kotlin-annotations)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Kotlin](https://img.shields.io/static/v1?label=Kotlin&message=v1.4.0&color=blue&logo=kotlin)](https://github.com/JetBrains/kotlin/releases/tag/v1.4.0)
[![Maven Central](https://img.shields.io/maven-central/v/net.pwall.json/json-kotlin-annotations?label=Maven%20Central)](https://search.maven.org/search?q=g:%22net.pwall.json%22%20AND%20a:%22json-kotlin-annotations%22)

Annotations for Kotlin JSON serialization and deserialization.

These classes provide a means of customizing the operation of the
[`json-kotlin`](https://github.com/pwall567/json-kotlin) library.
They were formerly part of `json-kotlin`, but have been split out into a separate project to allow them to be used
independently of the original project.

## Annotations

### `@JSONAllowExtra`

This annotation is applied to classes to indicate that extra properties in an object are allowed (and are to be ignored)
on deserialization.
It has no effect on serialization.

Example:
```kotlin
@JSONAllowExtra
data class Person(val name: String, val age: Int)
```
Deserializing the JSON string `{"name":"Fred Jones","age":25,"role":"manager"}` into this class will silently ignore the
`role` property.

### `@JSONIgnore`

This annotation is applied to properties (including `val` or `var` constructor parameters), and it indicates that the
relevant property is to be ignored during serialization and deserialization.
Note that a constructor parameter annotated with `@JSONIgnore` will need to have a default defined if the constructor is
to be used in the deserialization of an object with the property missing.

Example:
```kotlin
class Player(val name: String, @JSONIgnore val note: String? = null) {
    @JSONIgnore
    var score: Int = 0
}
```
Both the `note` and `score` properties will be ignored on serialization, and neither will be required (and will be
ignored if present) on deserialization.

### `@JSONIncludeAllProperties`

This annotation is applied to classes to indicate that all properties in the class are to be included in
auto-serialization even if `null`.
It has no effect on deserialization.

Example:
```kotlin
@JSONIncludeAllProperties
data class Project(val name: String, val description: String?)
```
The `description` property will be serialized as `"description":null` if the property is `null` instead of being
omitted.

### `@JSONIncludeIfNull`

This annotation is applied to individual properties (including `val` or `var` constructor parameters) to indicate that
the relevant property is to be included in auto-serialization even if `null`.

Example:
```kotlin
data class Project(val name: String, @JSONIncludeIfNull val description: String?)
```
The `description` property will be serialized as `"description":null` if the property is `null` instead of being
omitted.
This is similar to the example above but in this case the annotation applies only to the property `description`.

### `@JSONName`

This annotation is applied to properties and constructor parameters, and it supplies the name to be used in place of the
property or parameter name for auto-serialization and deserialization.

It takes a single parameter `name` - the name to be used.

Example:
```kotlin
data class Person(@JSONName("surname") val lastName: String, val firstName: String)
```
The property `lastName` will be serialized and deserialized using the property name `surname`.

## Alternative Annotations

In many cases, existing code will have annotations for the purposes above already in the code.
The `json-kotlin` library can be configured to use these annotations from other libraries - see the `JSONConfig` class.

## Dependency Specification

The latest version of the library is 1.1.1, and it may be obtained from the Maven Central repository.

### Maven
```xml
    <dependency>
      <groupId>net.pwall.json</groupId>
      <artifactId>json-kotlin-annotations</artifactId>
      <version>1.1.1</version>
    </dependency>
```
### Gradle
```groovy
    implementation 'net.pwall.json:json-kotlin-annotations:1.1.1'
```
### Gradle (kts)
```kotlin
    implementation("net.pwall.json:json-kotlin-annotations:1.1.1")
```

Peter Wall

2020-12-13
