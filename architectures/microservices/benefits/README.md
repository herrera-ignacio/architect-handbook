# Benefits and alternatives

- [Benefits and alternatives](#benefits-and-alternatives)
  - [Improve Team Autonomy](#improve-team-autonomy)
    - [How else could you do this?](#how-else-could-you-do-this)
  - [Reduce Time to Market](#reduce-time-to-market)
    - [How else could you do this?](#how-else-could-you-do-this-1)
  - [Scale Cost-Effectively for Load](#scale-cost-effectively-for-load)
    - [How else could you do this?](#how-else-could-you-do-this-2)
  - [Improve Robustness](#improve-robustness)
    - [How else could you do this?](#how-else-could-you-do-this-3)
  - [Scale the Number of Developers](#scale-the-number-of-developers)
    - [How else could yo do this](#how-else-could-yo-do-this)
  - [Embrace New Technology](#embrace-new-technology)
    - [How else could you do this?](#how-else-could-you-do-this-4)
  - [Reuse?](#reuse)

## Improve Team Autonomy

Many organizations have shown the benefits of creating autonomous teams. Keeping organizational groups small, allowing them to build close bounds and work effectively together without bringing in too much bureaucracy, has helped many organizations grow and scale more effectively than some of its peers.

If done right, team autonomy can *empower* people, help them step up and grow, and get the job done faster.

When teams own microservices, and have full control over those services, they increase the amount of autonomy they can have within a large-organization.

### How else could you do this?

* Giving ownership to parts of the codebase to different teams could be one answer (e.g., a *modular monolith*).

* Identifying people empoewered to make decisions for parts of the codebase on functional grounds (e.g., one person knows the most about tuning our query performance, so run anything in that area past that person first).

* Simply not having to wait for other people to do things for you, so adopting *self-service* approaches to provisioning machines or environment can be a huge enabler, avoiding the need for central operations teams to have to field tickets for day-to-day activies.

## Reduce Time to Market

By being able to deploy changes to individual services without having to wait for coordinated releases, we have the potential to release functionality to our customers more quickly.

### How else could you do this?

There are many variables. One suggestion is to carry out some sort of *path-to-production modeling* exercise, as it may help show that the biggest blocker isn't what you think.

Map out all the stages involved in delivering software, looking at the process from the moment a product owner comes up with an idea to the point where that idea actually got into production.

## Scale Cost-Effectively for Load

We need to scale up only those parts of our processing that are currently constraining us. It also follows that we can then scale down those microservices that are under less load, perhaps even turning them off when not required.

> This is why so many companies that build SaaS products adopt microservice architecture, it gives them more control over operational costs.

### How else could you do this?

* For a quick short-term improvement, you can try *vertical scaling*.

* Traditional *horizontal scaling* of the existing monolith behind a load balancer or a queue, although this may not help if the bottleneck is in the database.

## Improve Robustness

By decomposing functionality, the impact on one area of functionality need not bring down the whole system.

We also get to focus our time and energy on those parts of the application that most require robustness, ensuring critical parts of the system remain operational.

Microservices do not necessarily give you robustness for free. Rather, they open up opportunities to design a system in such a way that it can better tolerate network partitions, service outages, and the like.

### How else could you do this?

By running multiple copies of your monolith, perhaps behind a load balancer or another load distribution mechanism like a queue, we add redundancy to our system.

## Scale the Number of Developers

Adding more people will only continue to improve how quickly you can deliver, if the work itself can be partitioned into separate pieces of work with limited interactions between them.

To successfully scale the number of developers you bring to bear on a problem requires a good degree of *autonomy* between the teams themselves.

Just having microservices isn't going to be good enough. You'll have to think about how the teams align to the service ownership, and what coordination between teams is required. You'll also need to break up work in such a way that changes don't need to be coordinated across to many services.

### How else could yo do this

An alternative could be a *modular monolith*: different teams own each module, and as long as the interface with other modules remains stable, they could continue to make changes in isolation.

This approach is somewhat limited, though. We still have some form of contention between the different teams, as the software is still all packaged together, so the act of deployment still requires coordination between the appropriate parties.

## Embrace New Technology

By isolating the technology change in one service boundary, we can understand the benefits of the new technology in isolation, and limit the impact if the technology turns out to have issues.

The flexibility in being able to try new technology in a safe way can give them competitive advantage, both in terms of delivering better results for customers and in helping keep their developers happy as they get to master new skills.

### How else could you do this?

* If we still continue to ship our software as a single process, we do have limits on which technologies we can bring in. Of course, nothing stops you from incrementally replacing your existing monolith with a new one.

* New types of databases are problematic as this implies some sort of decomposition of a previously monolithic data model to allow for an incremental migration, unless you're going for a complete, immediate switchover to a new database technology, which is compliated and risky.

* If the current technology stack is considered a *burning platform* (end-of-life), you may have no choice other than to repliace it with a newer, better-supported technology stack.

## Reuse?

Fundamentally, reuse is *not* a direct outcome people want. Reuse is something people hope will lead to other benefits. We hope that through reuse, we may be able to ship features more quickly, or perhaps reduce costs, but if those things are your goals, track those things instead, or you may end up optimizing the wrong things.

Following the "goal of reuse", our team may be directed to use a functionality that is currently managed by a different team, in a different part of the organization. So now we have to coordinate with another part of the organization to make changes. We work out that we could actually just write our own implementation much faster and ship the feature to the customer more quickly that if we spend the time to adapt the existing goal.

If your acual goal is faster time to market, then writing your own implementation may be the right choice. But if you optimize for reuse hoping you get faster time to market, you may end up doing things that slow you down.

> Spend your time focusing on the actual object instead, and recognise that reuse may not always be the right answer.
