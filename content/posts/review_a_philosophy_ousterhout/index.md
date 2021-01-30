---
title: "Review: A philosophy of software development by John Ousterhout"
date: 2021-01-30T07:00:00+01:00
author: Diego
Tags:
    - Review
    - Books
    - Software engineering
    - Software Design
---

## TL:DR?

This book focuses on complexity as the main cause of problems in designing, developing and maintaining software systems.
Together with explaining how complexity happens it provides a coherent framework that allows developers and designers to think about complexity and how to keep it under control.

**Vote**: 10/10

**Who should read this**: everyone but especially junior developers.

## Review

### Summary
Reading this book was both validating and extremely frustrating.
Prof. Ousterhout is a compelling writer and he was able to put in a coherent form ideas and concepts about software development that I had floating around in my head for years.
This was the validating part, the frustrating part is that I wanted to write a book like this in ten years and now I know that is not necessary.


The central theme of the book is that the greatest limitation in software development is the ability of designers and programmers to deal with the complexity of the systems that they are creating.
Complexity is defined in the book as *anything related to the structure of a software system that makes it hard to understand and modify the system.*
Complexity seems to always increase and it ends up blocking everything, changes become impossible, people become frustrated and leave, and companies go broke.
The book tries to present a coherent framework to keep complexity to a manageable level by taking small actions that in the aggregate can have amazing effects.

### Main ideas

1. **Strategic vs tactical programming.**
    In the introduction Prof. Ousterhout highlights how complexity is incremental. 
    It is a death by a thousand cuts that happens because of decisions after decisions that pile up.
    Prof. Ousterhout claims, in my eyes correctly, that the main source of these cuts is what he calls tactical programming. 
    Tactical programming is the mindset of *having working code is the most important thing*.
    While working code is indeed important, in itself it is not enough to produce good system design and will (almost) always cause pain down the road.
    Strategic programming is the the opposite, it is the acknowledgement that working code is *not* enough. 
    Ideally once a new piece of code is added, the system should have been refactor in such a way that it looks like the new code was always intended to be there.
2. **Deep vs shallow modules.**
    The core concept of modular design is the idea of abstraction. An abstraction is defined in the book as: *a simplified view of an entity, which omits unimportant details*.
    The advantage of an abstraction is that its users need to only understand the abstraction's interface in order to use all the functionalities that it provides.
    Prof. Ousterhout argues then that the ideal design is for abstractions to have a small interface and offer lots of functionalities.
    Which is what he calls a *deep module*.
    Meanwhile most programmer end up producing what he calls *shallow modules*, i.e. modules with a large interface and a small number of functionalities.
3. **Design it twice.**
    Most developers especially the one that came up doing a traditional computer science education tend to fell in love with the first design they come up with. 
    This works really well most of the time while one is in university and/or working on small projects where the complexity is limited, the requirements are (somewhat) clear and changes are not that common. 
    In the real world this approach often fails spectacularly. 
    Prof. Ousterhout suggestion is to always try to design everything twice with completely different approaches. 
    This can be a waste of time in the short run but most of the time it will highlight limitations in the first approach and might show a better way to approach a problem.
4. **Comments as first class citizen.**
    Most developer resist comments and documentation.
    Prof. Ousterhout analyzes the usual myths around comments and he shows how these myths are quite dangerous and most of the time completely off the mark. 
    The book analyses what makes a comment good and what does not and it proposes to structure development around a comments first approach. 
    When you write a new module you should start from the documentation by sketching out its interfaces and structure with comments the main parts.
    The coding becomes the simply a matter of filling in the gaps and all the comments are up to date.
    While I am not one hundred percent sure that this is the best way to do it the whole discussion about comments in the book was really great and worth its time reading.

### What I find missing 

No book is perfect and clearly no book can cover everything. 
Actually one of the strengths of this book is that it does not try to do that.
It aims to discuss one aspect of software designing, i.e. complexity, and it does it really well.
That said, I think it is important to highlight there I think this book felt short or did not cover the topic all together.
In no particular order

* Agile and project management in general. 
  While this is not a book about project management almost all programmers work within an agile framework these days. 
  The book leave us with the important observation that iteration should happen over abstractions and not over feature.
  As almost everybody iterates over features I fell like there was a missed opportunity here to expand more on the subject.
* Working in teams.
  Almost all the software is designed by teams and there is very limited discussion in the book about how to deal with that.
* Refactoring. 
  There is a whole chapter in the book about refactoring but it does not really go too much into details. 
  As most of the code is actually legacy code it would have been nice to have a more detailed discussion on the topic.
* Testing.
  Similar to refactoring the topic is covered, even if only in a section, but it is not expanded as I think it should be.
  More and more project are adopting testing and this is really good but at the same time testing has a significant diminishing returns effect.
  I would have appreciated a longer discussion about pro and cons of testing and how to integrate testing with strategic development.
* Requirements.
  While it is not strictly speaking software design the ability of collecting requirements and understanding them is something fundamental for each software developer.
  If you code the wrong thing nothing else matter, it is still wrong. 
  The book hints at it here and there when it talks about design but it does not delve into it as much as it could.


### Conclusion

This is an amazing book that any junior software developer should read, and probably quite a few senior too. 
It is short and to the point and full of great examples about why this or that is a good/bad idea and can be use as a quick reference when needed.
If you want to improve your understanding of how to make good software this is a must read.