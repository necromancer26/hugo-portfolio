+++
title = "Cloud Computing Pillars"
description = ""
date = "2023-07-29T13:34:51+01:00"
tags = ["", ""]
categories = ["", ""]
draft = true
+++
# The Pillars of Cloud
There are at least as many different opinions of what ‘cloud’ means as there are software developers. However, we can all agree that cloud does mean something. Cloud computing promotes more efficient utilization of resources by reducing the [transaction costs](https://en.wikipedia.org/wiki/Transaction_cost) involved in provisioning and deprovisioning infrastructure to near zero, and it is able to do so because it differs in qualitative ways from previous models of computing (including virtualization). We identify two in particular.

These concepts are not always applicable to all aspects of the system, but we expect all services in OpenStack to conform to them wherever they are applicable, either directly or by working in conjunction with other services.
**Elasticity**
+ L'élasticité dans le cloud computing est la capacité de ce cloud à s'adapter aux besoins
applicatifs le plus rapidement possible.
**Grid Computing**
+ It provides a platform in which computing resources are organized into one or more logical pools to reach a common goal to solve a single task.
+ Grid computing systems can involve computing resources that are heterogeneous and geographically dispersed.
+ Grid computing is a form of distributed computing that involves coordinating and sharing computing, application, data and storage or network resources across dynamic and geographically dispersed organization
# Cloud Computing
+ Cloud computing is a model for enabling convenient, on-demand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction.
## Key technologies
+ Virtualization : an environment able to render all the services, being supported by a hardware
+ Outsourcing : farming out of services to a third party
+ Ressource sharing : device or piece of information on a computer that can be remotely accessed from another computer, transparently as if it were a resource in the local machine.
## Cloud Characteristics
+ Elasticity: Capacities can be elastically provisoned and released in some cases automatically and rapidly using the concept of scaling (horizental and vertical)
+ On demand self service: A consumer can unilaterally provision computing capabilities, such as server time and network storage, as needed automatically without requiring human interaction
+ Ressource pooling: The provider’s computing resources are pooled to serve multiple consumers using a ==multi-tenant model==, with different physical and virtual resources dynamically assigned and reassigned according to consumer demand.
+ Measured service: Cloud systems automatically control and optimize resource use by leveraging a metering capability at some level of abstraction appropriate to the type of service
+ Broad network access: Capabilities are available over the network and accessed through standard mechanisms that promote use by heterogeneous thin or thick client platforms
# Cloud deployments
A cloud deployment model specifies how a cloud infrastructure is built, managed, and accessed.
NIST specifies four primary cloud deployment models: 
+ Public
+ Private (On-premise, Off-premise)  
+ Community (On-premise, Off-premise)
+ Hybrid
## Public Cloud
+ Available to the general public
+ Available with little restriction
+ Access through internet
+ Owned by an organization (amazon, microsoft)
+ Data might be comingled on common storage devices
## Private Cloud
+ Exist on-premises or off-premises
+ Operated solely by an organization for the organization
+ Data is not comingled
+ Uses organizations data center and IT ressources and with virtualization
+ More strict access than public cloud
## Community Cloud
+ Can be premise or off premise
+ Can be used by different organization that share the same concers
+ Can be managed by the organization or third party
+ Shared non public cloud
## Hybrid Cloud
+ Offer flexibily
+ Can be a mix of 2 or more cloud deploymend models (private+public)
+ Higher complexity: management of security and risk
# Cloud virtualization
Virtualization is a technique that is used in cloud computing to simulate the functioning of a software of device on top of a hardware layer
## Means of virtualization
+ Multiplexing: Create a virtual object from one instance of physical object
+ Aggregation: Create a virtual object from multiple physicla objects like raid for multiple disks
+ Emulation: Creates a virtual object and its functioning from a different type of physical object
+ Multiplexing & Emulation: combines multiplexing and emulation
## Advantages of virtualization
+ less servers
+ cost reduction
+ better security
+ power and space reduction
+ better use of resources
Virtualization technology enables different virtual servers to share one physical server.
This process is called ==server consolidation==  which is commonly used to increase hardware utilization, load balancing and optimization of IT ressources.
