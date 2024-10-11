# Architects live in the first derivative

- [Architects live in the first derivative](#architects-live-in-the-first-derivative)
  - [Rate of change defines architecture](#rate-of-change-defines-architecture)
    - [Short-term vs Long-term](#short-term-vs-long-term)
  - [A balancing act](#a-balancing-act)
  - [Aspects that impede change](#aspects-that-impede-change)
    - [Dependencies](#dependencies)
    - [Friction](#friction)
    - [Poor quality](#poor-quality)
    - [Fear](#fear)
  - [Multispeed Architectures](#multispeed-architectures)
  - [Rate of change for architects](#rate-of-change-for-architects)

## Rate of change defines architecture

> The only system that wouldn't benefit from architecture is one that doesn't change at all. Just getting it working somehow seems good enough.

Good architects deal with change. They live in the system's _first derivative_: the mathematical expression for __how quickly a function's value changes__.

### Short-term vs Long-term

If either a large software project or housing project is undertaken without a conscious decision about its architecture, the "default" architecture converges toward the _Big Ball of Mud_.

Optimizing for local or short-term change can inhibit global or long-term change.

## A balancing act

Defining a system's architecture is a balancing act between many, often conflicting goals: flexible systems can be complex; high-performancing systems can be difficult to understand; easy-to-maintain systems can take more effort to construct initially.

Traditional IT organizations tend to have a somewhat uneasy relationship with change. This mindset is often reveladed by the popular engine room slogan: "_never touch a running system_".

Thus, many organizational systems are designed to control and prevent change: budgeting processes limit spending on change; quality gates limit changes going to production; project planning and requirements documents limit scope changes. Transforming a software delivery organization such that it embraces constant change requires adjusting these processes to support rather than prevent change without ignoring the generally useful motivation for setting them up in the first place.

## Aspects that impede change

### Dependencies

Too many interdependencies between a system's components will result in small changes needing adjustments in many places, increasing both effort and risk.

### Friction

Both cost and risk of change increase with friction, generated, for example, by long lead times for infrastructure provisioning or numerous manual deployment steps.

### Poor quality

There's a common misbelief that good quality requires extra time and effort. The inverse is actually true: __poor quality slows down software delivery__.

Changes to a poorly tested or poorly built system take more time and are more likely to break things.

### Fear

Poor quality and low levels of automation make change a risky proposition. Developers will thus be afraid of making changes. This leads to code rot, which in turn increases the risk of change - a nasty spiral.

## Multispeed Architectures

It suggests to separate components by rate of change. Moreover, traditional companies looking to become competitive in a digital world should initially increase the rate of change in the _interaction layer_ so that rapid changes can supposedly be applied to the customer-facing systems, whereas the legacy or record-keeping systems are kept stable and reliable.

This particular approach has significant shortcomings. It's based on the flawed assumption that one can _move faster by compromising quality_. Otherwise, we wouldn't need to keep a low rate of change in legacy systems to maintain their reliability. Second, a company will be hard pressed to localize change into the interaction layer. Furthermore, doing a change on the interaction layer typically also requires a change to the system of record, coupling the two systems' rates of change.

It turns out that the separation between systems of engagement and systems of record is _artificial_ and doesn't line up well with the overall rate of change from a business or end-user perspective.

Separating rate of change along a different dimension might well be beneficial, though. For example, a company's accounting or payroll system will likely have a lower rate of change and can utilize a different architecture from the core business systems, which form a competitive differentiator for the organization, and hence should support a higher rate of change.

## Rate of change for architects

Architects have an enormous challenge of staying up to date with new technologies but no one can stay current on everything. Instead, architects should be part of a __trusted but diverse network of experts__, which can provide unbiased information.

However, __neutraility is an architect's major asset__, so they're expected to cut through the buzzword fog to discern what's really new and what's just clever repackaging of old concepts.
