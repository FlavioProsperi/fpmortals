{frontmatter}

> "Love is wise; hatred is foolish. In this world, which is getting more
> and more closely interconnected, we have to learn to tolerate each
> other, we have to learn to put up with the fact that some people say
> things that we don't like. We can only live together in that way. But
> if we are to live together, and not die together, we must learn a kind
> of charity and a kind of tolerance, which is absolutely vital to the
> continuation of human life on this planet."
> 
> ― Bertrand Russell


# About This Book

This book is for Scala developers with a Java background who wish to
learn the **Functional Programming** (FP) paradigm. We do not accept
that the merits of FP are obvious. Therefore, this book justifies
every concept with practical examples, in Scala.

There are many ways to do Functional Programming in Scala. This book
focuses on using [scalaz](https://github.com/scalaz/scalaz), but you can instead use [cats](http://typelevel.org/cats/) or roll your own
framework.

This book is designed to be read from cover to cover, in the order
presented, with a rest between chapters. To ensure that the book is
concise, important concepts are not always repeated. Re-read sections
that are confusing, they will be important later.

A computer is not necessary to follow along, although we hope that you
will gain the confidence to independently study the scalaz source
code. Some of the more complex code snippets are available with [the
book's source code](https://github.com/fommil/fpmortals/tree/master/src/main/scala/) and those who want to play along with exercises are
encouraged to (re-)implement scalaz (and the example application)
using the partial descriptions presented in this book.

We also recommend [The Red Book](https://www.manning.com/books/functional-programming-in-scala) as further reading. It teaches how to
write an FP library in Scala from first principles. Try to attend a
Fantasyland Institute of Learning training course if you can, or at
least read the associated material: [Advanced Functional Programming
with Scala](https://gist.github.com/jdegoes/97459c0045f373f4eaf126998d8f65dc).


# Copyleft Notice

This book is **Libre** and follows the philosophy of [Free Software](https://www.gnu.org/philosophy/free-sw.en.html): you
can use this book as you like, the [source is available](https://github.com/fommil/fp-scala-mortals), you can
redistribute this book and you can distribute your own version. That
means you can print it, photocopy it, e-mail it, upload it to
websites, change it, translate it, remix it, delete bits, and draw all
over it.

You can even sell this book or your own version (although, morally,
you should offer a royalty share to the author). If you received this
book without paying for it, I would appreciate it if you donated what
you feel it is worth at <https://leanpub.com/fpmortals>.

This book is **Copyleft**: if you change the book and distribute your
own version, you must also pass these freedoms to its recipients.

This book uses the [Creative Commons Attribution ShareAlike 4.0
International](https://creativecommons.org/licenses/by-sa/4.0/legalcode) (CC BY-SA 4.0) license.

All original code snippets in this book are separately [CC0](https://wiki.creativecommons.org/wiki/CC0) licensed,
you may use them without restriction. Excerpts from `scalaz` and
related libraries maintain their license, reproduced in full in the
appendix.

The example application `drone-dynamic-agents` is distributed under
the terms of the [GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html): only the snippets in this book are available
without restriction.


# Thanks

Diego Esteban Alonso Blas, Raúl Raja Martínez and Peter Neyens of 47
degrees, Rúnar Bjarnason, Tony Morris, John de Goes and Edward Kmett
for their help explaining the principles of FP. Kenji Yoshida and
Jason Zaugg for being the main authors of scalaz, and Paul Chuisano /
Miles Sabin for fixing a critical bug in the scala compiler ([SI-2712](https://issues.scala-lang.org/browse/SI-2712)).

The readers who gave feedback on early drafts of this text.

Juan Manuel Serrano for [All Roads Lead to Lambda](https://skillsmatter.com/skillscasts/9904-london-scala-march-meetup#video), Pere Villega for [On
Free Monads](http://perevillega.com/understanding-free-monads), Dick Wall and Josh Suereth for [For: What is it Good For?](https://www.youtube.com/watch?v=WDaw2yXAa50),
Erik Bakker for [Options in Futures, how to unsuck them](https://www.youtube.com/watch?v=hGMndafDcc8), Noel Markham
for [ADTs for the Win!](https://www.47deg.com/presentations/2017/06/01/ADT-for-the-win/), Yi Lin Wei and Zainab Ali for their tutorials
at Hack The Tower meetups.

The helpul souls who patiently explained some concepts to me: Merlin
Göttlinger, Edmund Noble, Fabio Labella, Vincent Marquez, Adelbert
Chang, Kai(luo) Wang, Michael Pilquist, Adam Chlupacek, Pavel
Chlupacek, Paul Snively, Daniel Spiewak, Stephen Compall, Brian
McKenna, Ryan Delucchi, Pedro Rodriguez, Emily Pillmore.


# Practicalities

If you'd like to set up a project that uses the libraries presented in
this book, you will need to use a recent version of Scala with
FP-specific features enabled (e.g. in `build.sbt`):

{lang="text"}
~~~~~~~~
  scalaVersion in ThisBuild := "2.12.4"
  scalacOptions in ThisBuild ++= Seq(
    "-language:_",
    "-Ypartial-unification",
    "-Xfatal-warnings"
  )
  
  libraryDependencies ++= Seq(
    "com.github.mpilquist" %% "simulacrum"  % "0.11.0",
    "com.chuusai"          %% "shapeless"   % "2.3.2" ,
    "com.fommil"           %% "stalactite"  % "0.0.5" ,
    "org.scalaz"           %% "scalaz-core" % "7.2.15"
  )
  
  addCompilerPlugin("org.spire-math" %% "kind-projector" % "0.9.4")
  addCompilerPlugin(
    "org.scalamacros" % "paradise" % "2.1.1" cross CrossVersion.full
  )
~~~~~~~~

In order to keep our snippets short, we will omit the `import`
section. Unless told otherwise, assume that all snippets have the
following imports:

{lang="text"}
~~~~~~~~
  import scalaz._, Scalaz._
  import simulacrum._
  import stalactite._
~~~~~~~~


# Giving Feedback

You are reading an Early Access version of this book. You will have
access to the final version of the book, expected in 2018, at no
additional cost.

Please help raise awareness of this book by telling your friends,
especially the most sceptical.

If you would like to give feedback on this book, thank you! I ask of
you:

1.  if you are an FP beginner and something confused you, please point
    out the exact part of the text that confused you at
    [fommil/fpmortals](https://github.com/fommil/fp-scala-mortals/issues)
2.  if you are an expert in FP, please help by answering my questions
    at [fommil/drone-dynamic-agents](https://gitlab.com/fommil/drone-dynamic-agents/issues) and pointing out factual errors in
    this text.
3.  if you understood a concept, but feel that it could be explained in
    a different way, let's park that thought for now.
4.  grammatical errors and typos will (eventually) be corrected by an
    editor, they do not need to be reported.


