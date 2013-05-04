1 Introduction
============

Programming languages, like all languages, evolve over time in response to the changing needs and demands of the people using them.  In the realm of computer programming, potential language changes often begin with some form of a change proposal. Each language has its own particular version of a change proposal, but the underlying idea tends to be basically the same.  In essence, a change proposal provides documentation that allows the community of user to discuss and evaluate proposed alterations before ultimately deciding whether or not they merit inclusion in future versions of the language.  In the Scala programming language, formal changes are proposed via documentation of the Scala Improvement Processes, or SIPs.  SIP 18: Modularizing Language Features was initially proposed on March 17, 2012 and later accepted for inclusion in the release of Scala 2.10.0.  Consideration of SIP 18's impact on the Scala language and its use will provide the focus of this investigation.

First released in 2003, Scala is still a relatively new language. Thus, its evolution has not progressed to the same degree as more established languages like Python, C or Java.  Currently, increasing adoption as a mainstream programming language is one of the primary forces driving Scala's evolution.  The recent influx of Scala developers requires that the language be adapted to accommodate not only the burgeoning community of novice users, but also the new, complex ways that Scala will inevitably be used as its user base grows.  SIP-18  is one of the ways that Scala is being adapted to meet these needs.


1.1 Motivation for Improvement
------------------------------
In order to understand how SIP 18 will impact the Scala language, it is important to first understand the reason for proposing the change.  The major motivation underlying this proposal is the desire to improve the process of constructing high-level libraries and domain specific languages (DSLs).  With the increasing number of new Scala developers there is a trend of rising demand for better guidance particularly with the powerful abstractions that enable the construction of high-level libraries and domain specific languages (DSLs).

Developers continue to find new ways to use the powerful abstractions offered by Scala to construct modify and improve tools- in the form of high level libraries and DSLs- to handle a variety of solution techniques.  As these solutions grow in complexity the risk of errors due to improper use of more difficult language features becomes a near-constant concern.  Most mainstream languages are packaged with a variety of standardized Domain-Specific (DS) libraries- like symbolic math and arbitrary-precision computation libraries for example- to provide developers with powerful and consistent tools for solving a variety of problems.  Scala lacks this standardization of language features, and as a result, all of the language features that exist are available in the scope of any coding solution.  Other languages that are more fully established in the mainstream usually require that users explicitly import the features that they intend to use.

In C this looks like:

```#include  <path-spec>```

In Java this looks like:

```import package.Class```

SIP 18 addresses the implementation of this kind of modular method for importing member classes, objects and packages that are currently loaded by default.

Modularization has as much to do with the organization of packages as the usefulness of the language. Not every program/programer uses all of Scala’s many specialized and DS libraries. Limiting the scope of classes included in the default scope forces programmers to be aware of and control which are used.

1. Modualr organization shifts how developers explore the language. As they come across new uses for scala, they will be introduced to a DS library with a variety of related functionality.

2. Segmenting libraries aids in organizing documentation and support. If a question is raised on stack overflow (or another question/answer website), the community can point people in the direction of a DS Scala class.

3. Through a modular approach, one creates boundaries between sets of interconnected algorithms, which can then be separately maintained and improved. 


2 Proposed Improvement
====================
This SIP seeks to modularize abstractions for high-level libraries and DSL creation.  Modularity will promote a development process in which only the tools that a user needs are available in a given scope. 
2.1 Description
----------------
These are the libraries to be modularized:

1. 
2. 
3. 
4. 
5. 

These libraries provide high-level complex functionality and in some situations could be concidered dangerous when not implimented correctly. When imported, the postFixOps library eliminates the need for a statement operator (".") between a value and an associated method call. In other words, it allows the use of operator syntax in a postfix position. For example:

```List(1,2,3) tail```  rather than ```List(1,2,3).tail```  

This example is harmless in and of itself, but in more complicated expressions it can lead to abiguity about where statements end and where method calls are expected. This code does not compile due to some assumptions about how the compiler looks for method calls:

    val appender:List[Int] => List[Int] = List(1,2,3) ::: //add ; here
    List(3,4,5).foreach {println}

Seperately, the first and second statements (on each line) are correct. The problem arises when the compiler treates them as a single statment. The compiler is unsure where values end and method calls begin. A simple semi-collin tells the comiler to separate the statements.
2.2 Specification:
------------------
Language features will be controlled via inclusion of two new language objects in the Scala package. The first, named "languageFeature" is defined as follows:
    
    object languageFeature {  
    trait dynamics  
    trait postfixOps  
    trait reflectiveCalls  
    trait implicitConversions  
    trait higherKinds  
    trait existentials  
    object experimental {  
    trait macros  
    }  
    }
Second is an object named "language" that contains implicit feature values.  The name of each implicit value in this object matches the name of its feature type.  

    object language {  
    import languageFeature._  
    implicit val macros: macros = _  
    implicit val dynamics: dynamics = _  
    implicit val postfixOps: postfixOps = _  
    implicit val reflectiveCalls: reflectiveCalls = _  
    implicit val implicitConversions: implicitConversions = _  
    implicit val higherKinds: higherKinds = _  
    implicit val existentials: existentials = _  
    object experimental {  
    implicit val macros: macros = _  
    }  
    }
The types in the `languageFeature` object, called "feature flags" each control a set of features included in the Scala language.  For a feature to be enabled, an implicit value of that type must be available.  The primary way to do this is with a named import from the language object.  These look like:  

    imoort language.dynamics  
    import language.experimentals.macros  
    import language.{existentials, postfixOps}  
It is also possible to import all of the feaure flags using:  

    import language. _  
When a feature flag is imported, the features that it controls are enabled in the whole scope where the import statement is in effect.  This is important as it allows users to enable language features in parts of their code while leaving them disabled in other parts.
    
3 Impacts On the Language
=========================
(Include evidence and examples)

4 Conclusions
===========
>>>>>>> update
