# Hyrum's Law: The Law of Implicit Dependencies

> "With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody."

This is one of the most important lesson about *"it works"* versus *"it is maintainable"*. This axiom is a dominant factor in any discussion of changing software over time.

It is conceptually akin to entropy in thermodynamics. Just because Hyrum's Law will apply when maintaining software doesn't mean we can't plan for it or try to better understand it. We can **mitigate it**, but we know that **it can never be eradicated**.

*Hyrum's Law* represents the practical knowledge that **we can never assume perfect adherence to published contracts or best practices**.

As an API owner, you will gain *some* flexibility and freedom by being clear about interface promises, but in practice, the complexity and difficulty of a given change also depends on how useful a user finds some observable behavior of your API. If users cannot depend on such things, your API will be easy to change. **Given enough time and enough users, even the most innocuous change *will* break something**; your analysis of the value of that change must incorporate the difficulty in investigating, identifying, and resolving those breakages.

> This is thinking over the differences between code written with a *"works now"* and a *"works indefinitely"* mentality.

Code that depends on brittle and unpublished features of its dependencies is likely to be described as "hacky" or "clever", whereas code that follows best practices and has planned for the future is more likely to be described as "clean" and "maintainable". Both have their purposes, and which one you select depends crucially on the expected life span of the code in question.

> We've taken to saying, *"It's programming if 'clever' is a compliment, but it's software engineering if 'clever' is an accusation."*.
