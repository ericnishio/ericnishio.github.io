---
layout: post
title: The Cost of Adding Libraries
permalink: /blog/cost-of-adding-libraries/
---

Libraries are an important part of software development since they allow programmers to reuse code that has already been written to solve specific problems instead of rewriting solutions from scratch. So it would make sense to always use libraries when applicable to reduce the time it takes to roll out a product.

But every library you install comes with a technical cost, which may not be apparent outright. As your program grows, the libraries often become more tightly integrated into the core of the application, making them an indispensable part of the system as a whole. Loose coupling and separation of concerns are noble strategies but they can rarely be implemented in their ideal forms, all of the time.

As time passes, libraries demand that you address any breaking changes introduced by newer versions. Often, especially in niche ecosystems like the React universe, libraries also depend on each other, further increasing the number of potential cross-compatibility issues.

And as the number of libraries increases, so does the project's complexity. When mixed with the complexity of your own application code, you can imagine how challenging it can be to keep your codebase maintainable and efficient to work with.

We know that unmaintainable projects often result in expensive and often unnecessary rewrites. It is a vicious cycle that keeps repeating itself unless the underlying issues are resolved.

As a general rule, weigh your options with an economical mindset. Consider whether your codebase would truly benefit from a library, and think how it might affect maintainability months from now. Favor libraries that make your codebase simpler and smaller. Adopt mature and battle-tested libraries (also inspect their GitHub issues and stars). Switch libraries early as you find better replacements.

Admire your short list of dependencies.
