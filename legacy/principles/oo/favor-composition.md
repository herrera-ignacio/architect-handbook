# Favor object composition over class inheritance

Ideally, __you shouldn't have to create new components to achieve reuse. You should be able to get all functionality you need just by assembling existing components through object composition__.

This is rarely the case, because the set of available components is never quite rich enough in practice. Reuse by inheritance makes it easier to make new components that can be composed with the old ones. Inheritance and object composition thus work together.

Nevertheless, designs are often made more reusable (and simple) by depending more on object composition.
