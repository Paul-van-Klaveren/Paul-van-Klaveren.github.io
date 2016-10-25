---
title:  "Matching a range in a switch case"
description: Swift pattern matching allows us to see .
date: 2015-11-20
---

**Use Case**: You want to build a switch case that matches both an enum case without a parameter as well as a case for which its associated value should be within a certain range. …but you get an error: "" "case labels with multiple patterns cannot declare variables"


**Approach**: Assuming you always integrate the latest version of an available library, by knowing when the library was last changed you can derive what version it must be.

***

Immediately thinking of a where here (guarding the scope).

case .ServerLocationUnknown, .HTTP(let value) where (1...3).contains(value)

Error: 'case' labels with multiple patterns cannot declare variables

…ok, makes sense: it is kind of hard to reason about the logic in the case body without knowing if a `let` has been set. And checking for it is ugly.

This doesn't work either:
case .ServerLocationUnknown: fallthrough
case .HTTP(let value) where (1...3).contains(value)

Error: 'fallthrough' cannot transfer control to a case label that declares variables


But this does:

case .ServerLocationUnknown, .HTTP(300...399):

…and on top of it, it looks much cleaner as well! Great!
