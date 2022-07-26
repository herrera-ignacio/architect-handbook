# Churn Rule

> "Infrastructure teams must do the work to move their internal users to new versions themselves or do the update in place, in backward-compatible fashion."

*Churn rule* refers to the way we do deprectation: instead of pushing migration work to customers, teams can internalize it themselves, with all the economies of scale that provide.

This policy scales better: dependent projects are no longer spending progressively greater effort just to keep up.

## Google experience

Having a dedicated group of experts execute the change scales better than asking for more maintenance effort from every user: experts spend some time learning the whole problem in depth and then apply that expertise to every subproblem.

Forcing users to respond to churn means that every affected team does a worse job ramping up, solves their immediate problem, and then throws away that now-useless knowledge. **Expertise scales better**.
