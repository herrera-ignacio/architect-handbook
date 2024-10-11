# README

> Don't call us, we'll call you.

The Hollywood Principle gives us a way to prevent *dependency rot*. When rot sets in, no one can easily understand the way a system is designed.

> Dependency rot happens when you have high-level components depending on low-level components depending on high-level components depending on sideways components depending on low-level components, and so on.

With the Hollywood Principle, we allow low-level components to *hook* themselves int oa system, but the high-level components determine when they are needed, and how.

The high-level components give the low-level components a "don't call us, we'll call you" treatment. A **low-level component never calls a high-level component directly**.
