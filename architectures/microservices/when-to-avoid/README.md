# When to Avoid?

- [When to Avoid?](#when-to-avoid)
  - [Unclear Domain](#unclear-domain)
  - [Startups](#startups)
  - [Customer-Installed and Managed Software](#customer-installed-and-managed-software)
  - [Not Having a Good Reason!](#not-having-a-good-reason)

## Unclear Domain

Getting service boundaries wrong can be expensive. It can lead to a larger number of cross-service changes, overly coupled components, and in general could be worse than just havng a single monolithic service.

Prematurely decomposing a system into microservices can be costly, especially if you are new to the domain. In many ways, having an exsting codebase you want to decompose into microservices is much easier than trying to go to microservices from the beginning.

> If you feel that you don't yet have a full grasp of your domain, resolving that before commiting to a system decomposition may be a good idea.

## Startups

Many of the organizations famous for their use of microservices are considered startups, but in reality many of these companies including Netflix, Airbnb, and te like *moved oward* mocriservice archtecture only *later* in their evolution.

Microservices can be a great option for "scale-ups"; startup companies that have established at least the fundamentals of their product/market first and are now scaling to increase or achieve profitability.

Startups are often experimenting with various ideas. This can lead to huge shifts in the original vision for the production. It is likely a small organization with limited funding, which needs to focus all its attention on finding the right fit for its product. Microservices primarily solve the sorts of problems startups have once they've found that fit with their customer base.

Microservices are a great way of solving the sorts of problems you'll get once you have initial success as a startup.

> *"If your initial idea is bad, it doesn't matter whether you built it with microservices or not."* - Sam Newman

One alternative is to *only* split around boundaries that are clear at the beginning, and keep the rest on the more monolithic side. This will also give you time to assess how mature you are from an operational point of view.

## Customer-Installed and Managed Software

If you create software that is packaged and shipped to customers who then operate it themselves, microservices may well be a bad choice. When you migrate to a microservice architecture, you push a lot of complexity into the operational domain. Previous techniques you used to monitor and troubleshoot your monolithic deployment may well not work with your new distributed system.

You cannot expect your customers to have the skills or platforms available to manage microservice architectures. Even if they do, they may not have the same skills or platform that you require.

## Not Having a Good Reason!

This is the biggest reason not to adopt microservices, and that is if you don't have a clear idea of what exactly is that you're trying to achieve.

The outcome you are looking from your adoption of microservices will define *where* you start the migration and *how* you decompose the system.
