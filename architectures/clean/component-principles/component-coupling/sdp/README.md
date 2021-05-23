# Stable Dependencies Principle

> Depend in the direction of stability.

Some components are designed to be volatile. We *expect* them to cange.

Any component that we expect to be volatile should not be depended on by a component that is difficult to change. Otherwise, the volatile component will also be difficult to change.

> A module that you have designed to be easy to change can be made difficult to change by someone else who simply hangs a dependency on it.

## Not All Components Should Be Stable

> If all the components in a system were maximally stable, the system would be unchangeable.

We want to design our component structure so that some components are unstable and some are stable. The changeable components are on top and depend on the stable components at the botton. Putting the unstable components at the top of the diagram is a useful convention because any arrows that points *up* is volating the *SDP*.
