---
title: "Data Mesh — just yet another rabbit hole?"
linkTitle: "Data Mesh — just yet another rabbit hole?"
tags: [datamesh, saas]
categories: ["blog"]
weight: 100
description: >-
     Data Mesh is the latest addition to enterprise architectures, promising to solve all the problems that have plagued corporate technology landscapes for decades. But can it really deliver or will it be just another fad?
---

Data Mesh is the latest addition to enterprise architectures, promising to solve all the problems that have plagued corporate technology landscapes for decades. But can it really deliver or will it be just another fad?

The idiom “the whole is greater than the sum of its parts” is a popular one when it comes to building software. And yet, somehow, we’ve managed to get caught up in the “sum of its parts” approach — and it’s not working.

Let’s take a trip down memory lane.

The past 20 years have been a whirlwind of change for corporate IT departments.

What started with data warehouses has snowballed into off-the-shelf Software as a Service solutions, data lakes, and cloud computing.

And while they do offer a great deal of value and are facilitating data and digital transformation, I’ve noticed that most of our partners and customers at Ferris Labs typically encounter these three problems when using them:

1. Lack of quality data.
2. Scaling bottlenecks.
3. Lack of ownership of company-wide data.

Fast-forwarding to today, what promises to be the holy grail of architecture is coming to the rescue: **data mesh**.

![architecture benefits](/images/blog1-pic1.png)
*Pic 1: Abstract Data Mesh conceptual view*

Data mesh is a solution that could be the key to unlocking the value trapped in legacy systems as well as new SaaS offerings, and it could help you scale your data platforms in both technical and organizational ways.

But is this new design pattern — which combines equal parts of methodology and technology with a healthy dose of common sense — just another passing fad or is it here to stay?

This article intends to explore this question by taking a closer look at what data mesh is all about, what it means for your business, and how we can embrace data’s distributed and ubiquitous nature with this new design pattern.

Let’s dive in.

---

## Wait, why are we at an impasse with other traditional design patterns?
Traditional data architecture patterns have been built on deeply-entrenched assumptions about how data is created, stored, accessed, and processed.

These assumptions have become so ingrained in our minds that they don’t even register as assumptions anymore; they just seem like “the way things are” or “the way things have always been done”.

To unpack the underlying limitations that all generations of data architectures carry, let’s start by breaking down the paradigm that is currently in place:


## Most companies live with a very heterogeneous, historically grown mix of systems
This is not just a matter of having different types of software but also of different architectures and languages

For example, some parts of the system might be written in Java, others in Ruby or Python. Some parts might use REST services while others are connected by TCP/IP sockets.

In addition, there are legacy systems that no longer serve their original purpose or don’t fit the requirements of modern applications.

**The resulting landscape can be confusing, hard to understand and maintain, and expensive to change using traditional design patterns.**


## The various data trends have created facts we need to deal with & new setups to come.
We all know that software development is a dynamic, ever-changing field. But the pace of change has accelerated in recent years as new trends emerge and disrupt the status quo.

Think of old ERP and monolith systems. They were hard to scale, maintain, and upgrade, so we moved forward to SaaS solutions and cloud offerings. These offer greater agility, but they also have their own limitations.

The thing is, **today’s world demands more flexibility from our applications**: they need to be able to handle multiple sources of data, work with different types of users (both internal and external), and be able to scale quickly when necessary.


## The journey to SaaS & cloud is not yet over for most companies
The reasons for this are varied, but one of the biggest challenges is the fact that many companies rely on traditional design patterns in their existing systems.

This is largely because they have a lot of complex, legacy applications that don’t take advantage of what makes the cloud so great — scalability and flexibility — , and can’t be migrated without significant investment in time and money.

## Organizations need to get more nimble and unified
At the same time, every organization needs to get faster in order to meet the needs of clients and the market. It’s important for them to be able to scale up and down quickly, as well as adopt new products or services in a matter of days or weeks instead of months.

They need to do this while still being able to manage their data with all its complexity without sacrificing responsiveness or innovation.

Another problem is that whenever a tech or analytics team isn’t aligned with the rest of the organization, it creates friction because of mutually exclusive objectives and priorities.

Traditionally that is true for many “Centers of Excellence” and centralized departments like data science teams or analytics groups that are not reporting to a specific line of business or client-oriented department.

**This is all too difficult to achieve with traditional design patterns**, and that’s exactly why we need a more accurate and effective approach to develop a model that supports the client and the company and allows for standardization over time.

The data mesh claims to solve this dilemma.

It provides teams with a universal and automated approach to data standardization, product lineage, and quality metrics. Plus, data owners can use their data in more ways, allowing them to experiment and innovate while reducing the amount of work a team has to do to support every consumer.

![data mesh benefits](/images/blog1-pic2.png)
*Pic 2: Benefits of adopting a Data Mesh architecture*


## Can there ever be a “one size fits all” architecture?
Given all stated above, the short answer is “No”. But here’s the thing:

**We don’t have to align and harmonize everything in order to overcome the biggest challenge**: quickly identifying business and client priorities and keeping them aligned over time. And we don’t need to do this at the risk of efficiency and effectiveness.

**One of the cornerstones of this approach is domain-driven design**, where the people who know their data best — the data owners — take responsibility for managing it. **They own their data products.**

This new way of thinking about teams introduces the concept of an “inside view” and an “outside view”:

- The **inside view** has the freedom to decide how best to solve a particular problem or tackle a use case.

- The **outside view** has clear guidance on the common responsibilities every team has to cater to in order to provide value and transparency to the organization.

This “outside view” is non-negotiable and leads to what the data mesh community terms **“polyglot data products”**

## Polyglot data products
**Polyglot data products serve their immediate users and sponsors first and foremost**, and they can decide which tech stack is best suited for them. Also they need to reach beyond the traditional analytical scope in order to stay relevant in toady’s fast paced tech change environment. Which is why the business process and event pane should not be neglected.

![data products](/images/blog1-pic3.png)
*Pic 3: Data Products need to reach beyond just traditional analytics scope*

But to ensure transparency for the rest of the organization, these data products have to guarantee that:

- All data is accessible in a variety of ways (e.g, SQL, Graph, File, Message).

- All functions are available as services (ideally in an OpenAPI standard).

- All processes are usable and extensible via events, preferably in a Cloud Event standardized format.

- Role-based access control is baked into all access paths and technologies.

- All of the above are self-service and self-documenting.

*Why bother with all that trouble?,* you might ask.

It’s simple: because this architecture limits the impact any given change to a data product will have on its respective up and downstream components, making the whole organization more flexible.

*And what about the slow convergence over time?*

While every data product team is very flexible, the mandatory “connectivity” requirements *(the outside view)* create an elastic layer that will increasingly become the enterprise’s data and processing layer: the data mesh.

But **a transformation like this requires a long-term commitment, and organizations need to be aware that it’ll change how teams operate and how departments relate to each other.**

It takes cross-functional expertise to make such a journey successful, and it calls for high levels of autonomy.


## Does that mean all my previous investments are sunk cost?
The data mesh philosophy is based on the idea of integration and reuse, which means any existing systems that are deemed future-proof should be incorporated into the design over time.

The thing is, transforming monolithic and closed systems into data products is not a simple task. We need to make sure we’re also making thoughtful investments in our legacy components so that these systems can become true data products over time.

And whenever a new requirement, service, or call for a dedicated system arises, the domain owners and product sponsors should ensure that they have this new architecture mindset at heart.

The bottom line? If you need to get things done quickly and you’re on a budget, then data mesh is the answer.

Time and money-boxed solutions are ideal for this kind of focused approach. At Ferris Labs, for example, we’ve taken data mesh solutions and products from first thoughts to enterprise deployment in as little as 12 weeks.

---

## Data Mesh Use Cases & Examples
Now, let’s get to the more practical stuff: What are some common use cases for this approach, and who is using them?

Here are just a few examples:

- [Zalando](https://www.databricks.com/session_na20/data-mesh-in-practice-how-europes-leading-online-platform-for-fashion-goes-beyond-the-data-lake) has implemented a data mesh architecture to enable the company’s different engineering teams to work with innovations created by other teams, without the need for a slow, centralized change management process.

- [HSBC](https://www.assetservicingtimes.com/assetservicesnews/dataservicesarticle.php?article_id=10675&navigationaction=dataservicesnews&newssection=Data%20Services) has completely overhauled its securities processing by redesigning their internal data and insight logistics to be more “Amazon-style” and support faster change with fewer breaking points.

- A large [Swiss universal bank](https://www.waterstechnology.com/emerging-technologies/7947976/beyond-the-big-red-blob-ubs-sees-future-in-data-mesh-for-analytics) used this approach to renew and modernize its intraday liquidity processing.

- [Intuit](https://medium.com/intuit-engineering/intuits-data-mesh-strategy-778e3edaa017) uses data meshes to make sure that data engineering, mission-critical apps, and new machine learning algorithms work together in a coordinated way while enjoying some flexibility when required.

There are also other situations where data mesh is an ideal setup.

For example, when analytical and operational requirements come together, this architecture can be helpful because it doesn’t discriminate against either pattern and ensures that both are addressed. This is because data products need to serve and inform the data lake, which in turn, provides analytical or data science patterns with an easy way to access its insights.

Some other common starting points for data mesh architectures include the refactoring of existing legacy systems, cloud migration, and the productizing of data science components.


## So, how do I start implementing a Data Mesh strategy?
When you’re ready to get started with a data mesh architecture, there are a few things you need to keep in mind:

1) The first step is to make sure you are ready to embrace a federated setup of engineering responsibilities and break the traditional technical silos.

2) You’ll then need to align to a business domain with an important and urgent problem that your company can solve.

3) After that, assess how much time and money this would require, based on your existing setup, and then ask your stakeholders to come up with their “standard” design.

4) Once that’s done, you can ask us for a data product design that you can compare and judge against your “usual way of doing things”.

You can also get in touch to work out such a domain-driven design if you’d rather not bother your organization with competitive struggle.


## Final Thoughts
All in all, the data mesh architecture can be an incredibly powerful tool for any organization, and there’s never been a better time to make it your next tech investment.

It’s true that the multi-year journey of transforming your company from an imperative-based system to an event-driven one can be seen as a long process, but it is also rewarding and exciting.

It allows you to connect all of your systems, processes, and people in a way that makes it easier to make decisions and respond to change.

Best of all, there’s no reason to wait or hold back while the overall transformation is happening. Its domain-driven design lets you start without making major changes all at once or putting all your eggs in the same “data mesh basket.”
