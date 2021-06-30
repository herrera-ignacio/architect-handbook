# Beyoncé Rule

> "If a product experiences outages or other problems as a result of infrastructure changes, but the issue wasn't surfaced by tests in our *Continuous Integration* (CI) system, it is not the fault of the infrastructure change." More colloquially, this is phrased as *"If you liked it, you should have put a CI test on it".*

This is a great enabler of infrastructure teams, protecting their ability to make infrastructure changes safely.

The *Beyoncé Rule* implies that complicated, one-off bespoke tests that aren't triggered by our common CY system do not count. Without this, an engineer on an infrastructure team could conceivably need to track down every team with any affected code and ask them how to run their tests.
