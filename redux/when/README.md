# When and when not to reach out for Redux

> These are my notes from [this blog post](https://www.changelog.com/posts/when-and-when-not-to-reach-for-redux).

## Redux origins

Redux was invented as an implementation of the _Flux architecture_), which was in turn created to deal with limitations people had found in event-trigger-based state management, like Backbone specifically.

So I set `user.firstName`, it triggers a "change firstName" event, some other code is listening to that, it triggers another event...

Next thing you know, you're 15 events down one big synchronous call stack, and you have no idea why this happened in the first place. That's what Flux

## Ask yourself

* Do other parts of the application care about that list?

* Do you need to be able to derive data from that list?

* Is the same data being used to derive multiple components/features?

* Is there value to you, to being able to restore the state to a given point in time?

* Do you want to cache the data, i.e: reload it from state if it's already there instead of requesting it again?
