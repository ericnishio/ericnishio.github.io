---
layout: post
title: The Cost of Adding Libraries
permalink: /blog/cost-of-libraries/
---

Libraries are an important part of software development since they allow programmers to reuse code that has already been written to solve a particular problem instead of rewriting solutions from scratch (reinventing the wheel). So it would make sense to always reuse libraries when applicable to reduce the time it takes to roll out a product.

But every library that you install comes with a technical cost, which may not be apparent outright. As your program grows, the libraries often become more tightly integrated into the core of the application, making them an indispensable part of the system as a whole. Loose coupling and separation of concerns are noble strategies but they can rarely be implemented in their ideal forms, all of the time.

As time passes, libraries demand that you address any breaking changes introduced by newer versions. Sometimes, especially in niche ecosystems like the React universe, libraries also depend on each other, further increasing the number of potential cross-compatibility issues.

As more libraries are added to the project, the level of complexity increases exponentially. And when mixed with the complexity of actual application code, you can imagine how challenging it can become to keep your codebase maintainable and efficient to work with.

We already know that unmaintainable projects often result in expensive rewrites, which is a vicious cycle that keeps repeating itself if the underlying issues are left unresolved.
