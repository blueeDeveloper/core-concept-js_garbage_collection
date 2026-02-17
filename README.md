Memory management in JavaScript is mostly automated, but understanding the Mark-and-Sweep algorithm is crucial for writing memory-efficient code and avoiding leaks.

🗑️ Garbage Collection: Mark-and-Sweep
As of 2026, Mark-and-Sweep remains the standard garbage collection (GC) strategy used by modern engines like V8 (Chrome/Node.js). It moves away from the limitations of "reference counting" by focusing on reachability.

1. The Core Concept: Reachability
An object is considered "live" if it is reachable. The algorithm starts from a set of roots (usually the global object, like window or global, and local variables on the current stack) and identifies every object that can be accessed from them.

2. The Three Phases
The algorithm typically operates in distinct stages:

Marking: The GC traverses the "object tree." It starts at the roots and follows every internal reference (pointer) to other objects. Every object it encounters is "marked" as active.

Sweeping: The engine scans the heap memory. Any object that was not marked during the previous phase is considered unreachable and its memory is reclaimed.

Compacting (Optional): Many engines include a third step where they move the remaining "live" objects together to prevent memory fragmentation.

🧱 Why it’s better than Reference Counting
Older algorithms simply counted how many references pointed to an object. This failed miserably with circular references:


