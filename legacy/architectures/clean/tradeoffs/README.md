# Clean Architecture Tradeoffs

The added flexibility of the Clean Architectures comes at the cost of __more complexity__.

Many applications and especially CRUD webapps do not benefit from that. It makes sense to isolate things that might change, e.g. by using templates to generate HTML. It makes less sense to isolate things that are unlikely o change, e.g. the backing database. What is likely to change depends on the context and business needs.

> Frameworks make assumptions about what is going to change. E.g. React tends to assume that design and behaviour of a component change together, so it doesn't make sense to separate them. Few frameworks assume that you might want to change the framework. As such, frameworks do present an amount of lock-in. E.g. Ruby on Rail's reliance on the _Active Record_ pattern make it difficult to impossible to change your adata access strategy to the Repository pattern.
