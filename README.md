[![Build Status](https://secure.travis-ci.org/mpollmeier/scalameta-serialiser.png?branch=master)](http://travis-ci.org/mpollmeier/scalameta-serialiser)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.michaelpollmeier/scalameta_serialiser_2.11/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.michaelpollmeier/scalameta_serialiser_2.11)

# Setup with sbt
Get the latest version of [scalameta-serialiser](https://maven-badges.herokuapp.com/maven-central/com.michaelpollmeier/scalameta_serialiser_2.11) and the [scalameta compiler plugin](https://maven-badges.herokuapp.com/maven-central/org.scalameta/paradise_2.11.8)

```
libraryDependencies += "com.michaelpollmeier" %% "scalameta_serialiser" % "0.0.3"
addCompilerPlugin("org.scalameta" % "paradise" % "3.0.0-M5" cross CrossVersion.full)
```

# Usage

## @mappable

```scala
import scala.meta.serialiser.mappable
@mappable case class MyCaseClass(i: Int)
```

Annotating any case class with `mappable` will generate a companion object for your case class with two functions: 
* `def toMap(myCaseClass: MyCaseClass): Map[String, Any]` 
* `def fromMap(map: [String, Any]): Option[MyCaseClass]`

For details check out [MappableTest.scala](examples/src/test/scala/scala/meta/serialiser/MappableTest.scala)

## current limitations (a.k.a. TODOs)
* no support for default values -> information is available inside Term.Param (Trees.scala in scalameta repo)
* will fail if there is an existing companion object
  * can we match the companion object so we can track ? it's not in `defn`
  * any way to generate another object with a different name?
    * definition in macro paradise?
      git grep 'eponymous companions'

# sbt command to compile and test this project
~;clean;examples/clean;examples/test
