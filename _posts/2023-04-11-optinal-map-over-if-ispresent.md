---
layout: post
title: Optional.map over if and isPresent
--- 

Using Optinal API in Java consider using Optional.map over a combination of if-Statement and Optional.isPresent.

```java
var someOptional = Optional.ofNullable("Something");
if (someOptional.isPresent()) { // same structure as without Optinal API, actually only a bit more verbose
    System.out.println(someOptional.get().toUpperCase());
} else {
    System.out.println("");
}
````

```java
var text = Optional.ofNullable("Something") //
.map(String::toUpperCase) // this line is only executed if the optional value is present
.orElse("");
System.out.println(text);
````
