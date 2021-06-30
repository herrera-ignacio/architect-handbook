# Codebase Flexibility

We've discovered many factors that affect a flexibility of a codebase:

* **Expertise**: We know how to do this; for some languages, we've now down hundreds of compiler upgrades across many platforms.

* **Stability**: There is less change between releases because we adopt releases more regularly.

* **Conformity**: There is less code that hasn't been through an upgrade already, again because we are upgrading regularly.

* **Familiarity**: Because we do this regularly enough, we can spot redundancies in the process of performing an upgrade and attempt to automate.

* **Policy**: We have processes and policies like the *Beyoncé Rule*. The net effect of these processes is that upgrades remain feasible because infrastructure teams do not need to worry about every unknown usage, only the ones that are visible in our CI systems.

The underlying lesson is not about the frequency or difficulty of an upgrade, but that as soon as we became aware that upgrade tasks were necessary, we found ways to **make sure to perform those tasks with a constant number of engineers**, even as the codebase grew.
