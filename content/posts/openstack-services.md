+++
title = "Openstack Services"
description = ""
date = "2023-07-29T13:34:01+01:00"
tags = ["", ""]
categories = ["", ""]
draft = true
+++
# Openstack
An OpenStack deployment contains a number of components providing APIs to access infrastructure resources. This page lists the various services that can be deployed to provide such resources to cloud end users.
# Compute
## NOVA(Compute service)
Nova is the OpenStack project that provides a way to provision compute instances (aka virtual servers). Nova supports creating virtual machines, baremetal servers (through the use of ironic), and has limited support for system containers. Nova runs as a set of daemons on top of existing Linux servers to provide that service.
### Dependencies
+ Keyston: This provides identity and authentication for all OpenStack services.
+ Glance: This provides the compute image repository. All compute instances launch from glance images.
+ Neutron: This is responsible for provisioning the virtual or physical networks that compute instances connect to on boot.
+ Placement: This is responsible for tracking inventory of resources available in a cloud and assisting in choosing which provider of those resources will be used when creating a virtual machine.
*It can also integrate with other services to include: persistent block storage, encrypted disks, and baremetal compute instances.*
### Tools for using Nova
+ [[#Horizon]]: The official web UI for the OpenStack Project.
+ [Openstack client](https://docs.openstack.org/python-openstackclient/latest/) : The official CLI for OpenStack Projects. You should use this as your CLI for most things, it includes not just nova commands but also commands for most of the projects in OpenStack.
+ [Nova client](https://docs.openstack.org/python-novaclient/latest/user/shell.html) :For some very advanced features (or administrative commands) of nova you may need to use nova client. It is still supported, but the `openstack` cli is recommended.

## ZUN(Containers Service)
Zun is an OpenStack Container service. It aims to provide an API service for running application containers without the need to manage servers or clusters.
### Dependencies
-   [[#KEYSTONE (Identity service)]]
-   [[#NEUTRON]]
-   [Kuryr-libnetwork](https://docs.openstack.org/kuryr-libnetwork/latest/readme.html#kuryr-libnetwork): Kuryr-libnetwork is [Kuryr’s](https://github.com/openstack/kuryr) Docker libnetwork driver that uses Neutron to provide networking services. It provides containerised images for the common Neutron plugins.
other optional services:
+ Cinder: Cinder is the OpenStack Block Storage service for providing volumes to Nova virtual machines, Ironic bare metal hosts, containers and more.
+ Heat: Heat is a service to orchestrate composite cloud applications using a declarative template format through an OpenStack-native REST API.
+ Glance
# Hardware Lifecycle
## IRONIC (Bare metal provisioning)
Ironic is an OpenStack project which provisions bare metal (as opposed to virtual) machines. It may be used independently or as part of an OpenStack Cloud, and integrates with the OpenStack Identity (keystone), Compute (nova), Network (neutron), Image (glance), and Object (swift) services.
It provides the cloud operator with a unified interface to a heterogeneous fleet of servers while also providing the Compute service with an interface that allows physical servers to be managed as though they were virtual machines.
# Storage
## SWIFT (Object store)
Swift is a highly available, distributed, eventually consistent object/blob store.
Swift is ideal for storing unstructured data that can grow without bound.
## CINDER (Block Storage)
Cinder is the OpenStack Block Storage service for providing volumes to Nova virtual machines, Ironic bare metal hosts, containers and more.
Cinder goals:
-   **Component based architecture**: Quickly add new behaviors
-   **Highly available**: Scale to very serious workloads
-   **Fault-Tolerant**: Isolated processes avoid cascading failures
-   **Recoverable**: Failures should be easy to diagnose, debug, and rectify
-   **Open Standards**: Be a reference implementation for a community-driven api
### Dependencies
+ keystone
### Tools for using cinder
+ Horizon
+ Openstack client
- [Cinder Client](https://docs.openstack.org/python-cinderclient/latest/user/shell.html): The **openstack** CLI is recommended, but there are some advanced features and administrative commands that are not yet available there. For CLI access to these commands, the **cinder** CLI can be used instead.
# Networking
## NEUTRON
Neutron is an OpenStack project to provide “network connectivity as a service” between interface devices, managed by other OpenStack services (e.g., nova). It implements the [OpenStack Networking API](https://docs.openstack.org/api-ref/network/).
### Dependencies
+ [[#KEYSTONE (Identity service)]]
# Orchestration
## HEAT
Heat is a service to orchestrate composite cloud applications using a declarative template format through an OpenStack-native REST API.
Heat provides a template based orchestration for describing a cloud application.
A Heat template describes the infrastructure for a cloud application in text files which are readable and writable by humans, and can be managed by version control tools.
# Web frontends
## Horizon
a web based user interface to OpenStack services including Nova, Swift, Keystone, etc.
Horizon ships with three central dashboards:
+ User Dashboard
+ System Dashboard
+ Settings” dashboard. 
Between these three they cover the core OpenStack applications and deliver on Core Support.
The Horizon application also ships with a set of API abstractions for the core OpenStack projects in order to provide a consistent, stable set of reusable methods for developers. Using these abstractions, developers working on Horizon don’t need to be intimately familiar with the APIs of each OpenStack project.
# Shared Services
## Glance (Image services)
The Image service (glance) project provides a service where users can upload and discover data assets that are meant to be used with other services. This currently includes _images_ and _metadata definitions_.
### Images
discovering, registering, and retrieving virtual machine (VM) images. Glance has a RESTful API that allows querying of VM image metadata as well as retrieval of the actual image.
### Metadata Definitions
Glance hosts a _metadefs_ catalog. This provides the OpenStack community with a way to programmatically determine various metadata key names and valid values that can be applied to OpenStack resources.
Note that what we’re talking about here is simply a _catalog_; the keys and values don’t actually do anything unless they are applied to individual OpenStack resources using the APIs or client tools provided by the services responsible for those resources.
## KEYSTONE (Identity service)
Keystone is an OpenStack service that provides API client authentication, service discovery, and distributed multi-tenant authorization by implementing OpenStack’s Identity API.
### Tools for using keystone
keystone can be managed through cli management utilities:
+  keystone-manage: the command line tool which interacts with the Keystone service to initialize and update data within Keystone. Generally, `keystone-manage` is only used for operations that cannot be accomplished with the HTTP API, such data import/export and database migrations.
+ keystone-status: command line tool that helps operators upgrade their deployment.
### Advanced features
keystone provides other more advanced features like:
+ Unified Limits: limits can be used by services to enforce quota on resources across OpenStack.
+ Resource Options: options are used to control specific features or behaviors within keystone.
+ Credential Encryption:  keystone encrypts all credentials stored in the default `sql` backend. Credentials are encrypted with the same mechanism used to encrypt Fernet tokens, `fernet`. Keystone provides only one type of credential encryption but the encryption provider is pluggable in the event you wish to supply a custom implementation.
# Webography
[OpenStack Services](https://www.openstack.org/software/project-navigator/openstack-components#openstack-services)
[Kuryr-libnetwork](https://docs.openstack.org/kuryr-libnetwork/latest/readme.html#kuryr-libnetwork)
[Ironic](https://docs.openstack.org/ironic/latest/)
[Swift](https://docs.openstack.org/swift/latest/)
[Cinder](https://docs.openstack.org/cinder/latest/)
[Neutron](https://docs.openstack.org/neutron/latest/)
[Heat](https://docs.openstack.org/heat/latest/)
[Horizon](https://docs.openstack.org/horizon/latest/)
[Horizon Basics](https://docs.openstack.org/horizon/latest/contributor/intro.html#contributor-intro)
[Keystone](https://docs.openstack.org/keystone/latest/)
[Unified limits](https://docs.openstack.org/keystone/latest/admin/unified-limits.html)
[Resource options](https://docs.openstack.org/keystone/latest/admin/resource-options.html)
[Credential encryptiuon](https://docs.openstack.org/keystone/latest/admin/credential-encryption.html)
[Glance](https://docs.openstack.org/glance/latest/)