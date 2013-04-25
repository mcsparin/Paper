1 Introduction
============

Programming languages, like all languages, evolve over time in response to the changing needs and demands of the people using them.  In the realm of computer programming, potential language changes often begin with some form of a change proposal. Each language has its own particular version of a change proposal, but the underlying idea tends to be basically the same.  In essence, a change proposal provides documentation that allows the community of user to discuss and evaluate proposed alterations before ultimately deciding whether or not they merit inclusion in future versions of the language.  In the Scala programming language, formal changes are proposed via Scala Improvement Processes, or SIPs.  SIP 18: Modularizing Language Features was initially proposed on March 17, 2012 and later accepted for inclusion in the release of Scala 2.10.0.  Consideration of SIP 18's impact on the Scala language and its use will provide the focus of this invesigation.

<<<<<<< HEAD
Being that Scala is still in its infancy, its domain of usefulness has not been decided by the CS community. Developers continue to modify and improve its features, tailoring syntax and functionality to handle a variety of solution techniques in an effort to solidify Scala as a general-purpose programming language. Most general-purpose languages are packaged with a variety of Domain-Specific (DS) libraries like those for symbolic math and arbitrary-precision computation, but, unlike Scala, you must explicitly import them into the environment. 

In C this looks like:

```#include  <path-spec>```

In Java this looks like:

```import package.Class```

SIP 18 addresses the implementation of this kind of modular method for importing member classes, objects and packages that are currently loaded by default.

1.1 Motivation for Improvement
------------------------------
In order to understand how SIP 18 will impact the Scala language, it is important to first understand the reason for proposing the change.  The major motivation underlying this proposal is the desire to improve the process of constructing high-level libraries and domain specific languages (DSLs).  Or more specifically, to satisfy the growing demand for better guidance in using the "range of powerful abstractions that enable the construction of high-level libraries and DSLs" that Scala defines.

Modularization has as much to do with the organization of packages as the usefulness of the language. Not every program/programer uses all of Scala’s many specialized and DS libraries. Limiting the scope of classes included in the default scope forces programmers to be aware of and control which are used.

1. Modualr organization shifts how developers explore the language. As they come across new uses for scala, they will be introduced to a DS library with a variety of related functionality.

2. Segmenting libraries aids in organizing documentation and support. If a question is raised on stack overflow (or another question/answer website), the community can point people in the direction of a DS Scala class.

3. Through a modular approach, one creates boundaries between sets of interconnected algorithms, which can then be separately maintained and improved. 


2 Proposed Improvement
====================
2.1 Description
----------------
2.2 Implementation
------------------

3 Impacts On the Language
=========================
(Include evidence and examples)

4 Conclusions
===========
>>>>>>> update
