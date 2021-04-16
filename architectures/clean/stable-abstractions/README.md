# Stable Abstractions Rule

* __Don't refer to volatile concrete classes, refer to abstract interfaces instead__.
* Don't derive from volatile concrete classes.
* Don't override concrete functions (you inherit its dependencies).
* Never mention the name of anything concrete and volatile.

Changes to concrete implementation do not always, or even usually, require changes to the interfaces they implement. Therefore __interfaces are less volatile than implementations__.

> Indeed, good software designers and architects work hard to reduce the volatility of interfaces, and find ways to add functionality to implementations without making changes to the interfaces.
