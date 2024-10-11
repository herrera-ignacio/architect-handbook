# Churn Rule

> From [Google Software Engineering](https://www.oreilly.com/library/view/software-engineering-at/9781492082781/ch01.html#:~:text=Forcing%20users%20to%20respond%20to,Expertise%20scales%20better.)

## Law

> "Teams must do the work to move their internal users to new versions themselves or do the update in place, in backward-compatible fashion."

## The Problem

Consider a _traditional approach to deprecation_. A new Widget has been developed.

> The decision is made that everyone should use the new one and stop using the old one.

To motivate this, project leads say "We'll delete the old Widget on August 15th; make sure you've converted to the new Widget.".

> This type of approach might work in a small software setting but quickly fails as both the depth and breadth of dependency graph increases.

Team depend on an ever-increasing number of Widgets, and a single build break can affect a growing percentage of the company. Solving these problems in a scalable way means changing the way we do deprecation.

## The Proposal

_Churn rule_ refers to the way we do deprecation: instead of pushing migration work to customers, teams can internalize it themselves, with all the economies of scale that provide.

Dependent projects should no longer be spending progressively greater effort just to keep up.

### Google case study

> "Expertise scales better."

Having a dedicated group of experts execute the change scales better than asking for more maintenance effort from every user: experts spend some time learning the whole problem in depth and then apply that expertise to every subproblem.

Forcing users to respond to churn means that every affected team does a worse job ramping up, solves their immediate problem, and then throws away that now-useless knowledge.
