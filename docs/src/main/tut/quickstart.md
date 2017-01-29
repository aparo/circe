## Quick start

circe is published to [Maven Central][maven-central] and cross-built for Scala 2.10, 2.11, and 2.12,
so you can just add the following to your build:

```scala
val circeVersion = "0.6.1"

libraryDependencies ++= Seq(
  "io.circe" %% "circe-core",
  "io.circe" %% "circe-generic",
  "io.circe" %% "circe-parser"
).map(_ % circeVersion)
```

If you're using circe's generic derivation with Scala 2.10, or `@JsonCodec` the macro annotation
(with any Scala version), you'll also need to include the [Macro Paradise][paradise] compiler
plugin in your build:

```scala
addCompilerPlugin(
  "org.scalamacros" % "paradise" % "2.1.0" cross CrossVersion.full
)
```

Then type `sbt console` to start a REPL and then paste the following (this will also work from the
root directory of this repository):

```tut:book
import io.circe._, io.circe.generic.auto._, io.circe.parser._, io.circe.syntax._

sealed trait Foo
case class Bar(xs: List[String]) extends Foo
case class Qux(i: Int, d: Option[Double]) extends Foo

val foo: Foo = Qux(13, Some(14.0))

foo.asJson.noSpaces

decode[Foo](foo.asJson.spaces4)
```

No boilerplate, no runtime reflection.
