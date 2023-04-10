+++
title = "Context mapping"
description = "Briefly introduce to Context mapping"
draft = false

[taxonomies]
tags = ["ddd", "strategic ddd"]

[extra]
feature_image = './john-torcasio-DXa_QaVmM2A-unsplash.jpg'
feature = true
link = ""
+++

![Streams](john-torcasio-DXa_QaVmM2A-unsplash.jpg)

Context mapping is a technique used in Domain-Driven Design (DDD) to facilitate the management of relationships and interactions between different bounded contexts within a larger domain. This technique has been successfully applied in several fields, including software development, engineering, and aerospace.

One example of how context mapping could be applied in the aerospace industry is in the development of complex projects like the F-22 Raptor. The F-22 was a product of various companies, each with their own specialized knowledge domains related to the aircraft's development. To ensure efficient collaboration and development of the F-22, context mapping techniques could have been utilized to identify the different bounded contexts involved in the project, such as avionics, engines, aerodynamics, and weapons systems. The relationships and dependencies between these contexts could have been mapped out, allowing each company to focus on their own areas of expertise while still working together effectively.

By utilizing context mapping, the companies involved in the F-22's development would have been able to determine what each context or team expected to receive from the other teams, and what they needed to contribute in order to build a complete, functional aircraft. This approach could have helped to ensure that the F-22 Raptor was developed efficiently and effectively, with each company contributing their specialized knowledge and expertise to the project.

## Introduction to context map relations 
Context maps are powerful tools for visualizing the relationships between different contexts and teams in a system. They enable you to identify patterns and interactions between teams and see how they affect each other. This is essential for understanding the structure and functionality of existing systems or applications, as well as planning the design of new ones. In this article, we will explore the most common context map patterns and their applications.
Context maps are particularly helpful in identifying management issues between applications and teams. They can reveal how teams communicate and their influence on each other. Using context mapping, it is possible to gain a clear understanding of where and how bad models are propagated in the system.

Context map patterns are categorized in three types:

- Upstream patterns: Open Host Service and Event Publisher

- Midway patterns: Shared Kernel, Published Language, Separate Ways, Partnership

- Downstream patterns: Customer/Supplier, Conformist, Anti-Corruption Layer

### Open / Host Service
The Open Host Service pattern involves exposing an API defined by a bounded context that allows other systems to integrate with it. This relationship is particularly useful when there are multiple integrators, allowing each team to maintain their own integrations. The ideal scenario is where the API is only expanding, except when a single team has special needs and the API has to be expanded, breaking the downstream hierarchy. However, the previous API should always be preserved for already integrated systems.

### Shared Kernel
The Shared Kernel is a pattern in context mapping where multiple teams collaborate to extract common parts of several contexts into a shared module or context, reducing code duplication and ensuring consistency in the system. The process involves defining a common subset of the domain model, which requires teams to agree on a common set of terms and concepts. Once defined, the common subset can be implemented in a shared module or context, enabling each team to align their work with the rest of the system. This approach is valuable when there is a high degree of collaboration and need for consistency across multiple bounded contexts. By implementing the Shared Kernel pattern, teams can improve consistency and reduce code duplication, leading to a more efficient and effective system.

**The Shared Kernel approach is often a natural choice for libraries, as it allows for code reuse and reduces duplication. However, in the context of domain modeling, the approach can sometimes create additional coupling between different contexts, making the system more fragile and less resilient to changes. This is particularly true when the contexts have significantly different needs and objectives, or when a high degree of autonomy is required for each context.**

While the Shared Kernel approach can be useful in some situations, it is important to carefully consider the needs of each context before implementing it. In cases where the contexts have different needs or objectives, or where a high degree of autonomy is required, other approaches, such as the Anti-Corruption Layer or Separate Ways patterns, may be more appropriate. By choosing the right approach for each context, developers can create a more resilient and effective system.

### Separated ways
The Separate Ways pattern in context mapping is a powerful technique that can help developers minimize dependencies between different contexts. By allowing each context to have its own domain model and business logic, this approach can reduce coupling and make the system more resilient to changes.

The Separate Ways pattern can be very beneficial when working with multiple contexts that have unique needs and objectives. By isolating each context, developers can prevent changes in one area from affecting others. This helps to create a more modular and manageable system, ultimately leading to a more efficient and effective product.

For example, imagine a system with several contexts that all share some common concepts but have separate implementations for those concepts. Using the Separate Ways pattern, each context can have its own domain model and business logic, allowing developers to make changes to one context without affecting the others. This makes it easier to maintain the system and can help to reduce the risk of unintended consequences from changes made in one context.

To implement the Separate Ways pattern, developers need to carefully define the boundaries of each context and ensure that they are properly isolated from each other. This may involve setting up clear communication channels between contexts and using well-defined interfaces to exchange data between them. By taking these steps, developers can effectively implement the Separate Ways pattern and create a more resilient and efficient system.

### Anticorruption layer
The anticorruption layer pattern addresses scenarios in which it is not desirable or worth the effort to conform to the supplier's model, such as: When the downstream bounded context contains a core subdomain.

This type of relationship is often used to adapt a legacy system to a new architecture, and gradually migrate from the legacy codebase. The Anticorruption layer acts as an adapter that translates data from the upstream and protects it from unwanted changes.

### Publish language

> “The translation between the models of two bounded contexts requires a common language. Use a well-documented shared language that can express the necessary domain information as a common medium of communication, translating as necessary into and out of that language. Published Language is often combined with Open Host Service.” [Evans 2003]

It is basically a relation that is based on some shared, well-defined common language, which could be e.g. xml, protobuf, GTFS, vcard.


### Partnership
The Partnership pattern is a context map pattern that involves a cooperative relationship between two contexts that have dependent goals. In this pattern, two teams work together to align their goals and collaborate to achieve their objectives.

The Partnership strategy is beneficial when two or more teams are dependent on each other's work to achieve their goals. For example, one team may be responsible for developing the backend of an application, while another team is responsible for the frontend. Both teams need to work together to ensure that the frontend and backend are integrated seamlessly and that the application functions as expected.

In a Partnership relationship, both teams are responsible for ensuring that their work aligns with the goals of the other team. They communicate regularly to ensure that they are on the same page and to identify any potential issues that may arise.

This pattern is particularly useful in situations where there is a high degree of interdependence between teams, and where communication and collaboration are critical to the success of the project. By working together in a Partnership relationship, teams can ensure that their work is aligned, and that the project is completed on time and within budget.

### Customer-supplier
The Customer-supplier pattern describes the relationship between two contexts where one provides data or services (upstream) and the other consumes them (downstream). Both contexts must establish clear communication channels and agree on the format and quality of the data or services being provided to ensure effective collaboration. This pattern is useful when there is a clear connection between the two contexts and the downstream context relies on the data or services provided by the upstream context to function effectively.

### Conformist
The Conformist pattern is a valuable approach in context mapping that facilitates collaboration between two bounded contexts. It occurs when the downstream context is able to embrace and implement the upstream context's model without needing to make any changes or modifications. his pattern is applicable when there is a high degree of consistency and alignment between the two contexts, allowing for seamless integration of the upstream context's model into the downstream context's system.

By adopting the Conformist pattern, the downstream context is able to align itself with the upstream context's model, which promotes consistency and reduces the risk of errors or inefficiencies in the system. It can also lead to more efficient communication and collaboration between the two contexts, ultimately resulting in a more effective and streamlined system.

### Event publisher

A domain event is a term used to describe something that happened in the past and is relevant to domain experts. Upstream contexts publish all their domain events through a messaging system, and downstream contexts can subscribe to the events that are relevant for them and conform or transform those events in their models.

Links:  
[DDD-strategic-patterns](https://pubs.opengroup.org/architecture/o-aa-standard/DDD-strategic-patterns.html)
[Domain-Driven Design: Tackling Complexity in the Heart of Software, by Eric Evans, Addison-Wesley 2004](http://ddd.fed.wiki.org/)
[DDD bounded contexts](https://www.baeldung.com/java-modules-ddd-bounded-contexts)
[Domains subdomain roblem](https://medium.com/nick-tune-tech-strategy-blog/domains-subdomain-problem-solution-space-in-ddd-clearly-defined-e0b49c7b586c)