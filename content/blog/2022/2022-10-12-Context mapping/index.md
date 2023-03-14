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

One example of how context mapping could be utilized in the aerospace industry is in the development of complex projects such as the F-22 Raptor. The F-22 was designed and produced by various companies, each with their own areas of expertise and knowledge domains related to the development of the aircraft. To ensure efficient cooperation and development of the F-22, these companies could have potentially used context mapping techniques to identify the different bounded contexts involved in the project, such as avionics, engines, aerodynamics, and weapons systems. They could have then mapped out the relationships and dependencies between these contexts, allowing each company to focus on their own areas of expertise while still collaborating effectively.

By utilizing context mapping, the companies involved in the F-22's development would have been able to determine what each context or team expected to receive from the other teams, and what they needed to contribute in order to build a complete, functional aircraft. This approach could have helped to ensure that the F-22 Raptor was developed efficiently and effectively, with each company contributing their specialized knowledge and expertise to the project.

## Introduction to context map relations 

Context Maps are a way to visualize the contact between different contexts and teams. They can help you see how patterns are shared between different teams, and how the different teams interact with each other.. This allows you to see the relationships between different contexts of the system. Context Maps can be used to help understand the structure and functionality of existing systems or applications, as well as to help plan the design of new ones. There are many different context map patterns, depending of publications, this article will focus on the most common ones.

Context maps help identify management issues between applications and teams, revealing how teams communicate and their influence on one each other. Using context mapping, it is possible to gain a clear understanding of where and how bad models are propagated in system.

Context map patterns are categorized in three ways:

- Upstream patterns: Open Host Service and Event Publisher

- Midway patterns: Shared Kernel, Published Language, Separate Ways, Partnership

- Downstream patterns: Customer/Supplier, Conformist, Anti-Corruption Layer

### Open / Host Service
Exposing an API defined by a (bounded) context that allows other systems integrate with it. This downstream relation comes in handy when we have many integrators as allow each team to maintainance their own intergrations. In the ideal scenario api is only expanding, except when a single team has speciall needs and api has to be expanded breaking the downsteream hierarchy, but the previous api should be always preserved for already integrated systems.


### Publish language

> “The translation between the models of two bounded contexts requires a common language. Use a well-documented shared language that can express the necessary domain information as a common medium of communication, translating as necessary into and out of that language. Published Language is often combined with Open Host Service.” [Evans 2003]

It is basicily a relation that is based on some shared, well-defined common language, which could be e.g. xml, protobuf, GTFS, vcard.


### Partnership
Relationship between two contexts that cooperate to align the two teams with dependent goals

### Shared Kernel
Relationship when common parts of several contexts are extracted to another context/module to reduce code duplication

### Customer-supplier
Connection between two contexts, where one context (upstream) produces data, and the other (downstream) consume it. In this relationship, both sides are interested in establishing the best possible communication

### Conformist
If the downstream team can accept the upstream team's model, the relationship between the bounded contexts is called conformist.

### Anticorruption layer
The anticorruption layer pattern addresses scenarios in which it is not desirable or worth the effort to conform to the supplier's model, such as: When the downstream bounded context contains a core subdomain.

This type of relationship is often used to adapt a legacy system to a new architecture, and gradually migrate from the legacy codebase. The Anticorruption layer acts as an adapter that translates data from the upstream and protects it from unwanted changes.

### Event publisher

A domain event is a term used to describe something that happened in the past and is relevant to domain experts. Upstream contexts publish all their domain events through a messaging system, and downstream contexts can subscribe to the events that are relevant for them and conform or transform those events in their models.

Links:  
[DDD-strategic-patterns](https://pubs.opengroup.org/architecture/o-aa-standard/DDD-strategic-patterns.html)
[Domain-Driven Design: Tackling Complexity in the Heart of Software, by Eric Evans, Addison-Wesley 2004](http://ddd.fed.wiki.org/)
[DDD bounded contexts](https://www.baeldung.com/java-modules-ddd-bounded-contexts)
[Domains subdomainp roblem](https://medium.com/nick-tune-tech-strategy-blog/domains-subdomain-problem-solution-space-in-ddd-clearly-defined-e0b49c7b586c)