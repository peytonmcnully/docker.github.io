---
description: Learn about the system requirements for installing Docker Universal Control
  Plane.
keywords:
- docker, ucp, architecture, requirements
menu:
  main:
    identifier: ucp_system_requirements
    parent: mn_ucp_installation
    weight: 0
title: System requirements
---

# UCP system requirements

Docker Universal Control Plane can be installed on-premises or on the cloud.
Before installing, be sure your infrastructure has these requirements.

## Hardware and software requirements

You can install UCP on-premises or on a cloud provider. To install UCP,
all nodes must have:

* Linux kernel version 3.10 or higher
* CS Docker Engine version 1.12.0 or higher. Learn about the
[operating systems supported by CS Docker Engine](https://docs.docker.com/cs-engine/install/).
* 2.00 GB of RAM
* 3.00 GB of available disk space
* A static IP address

For highly-available installations, you also need a way to transfer files
between hosts.

## Ports used

When installing UCP on a host, make sure the following ports are open:

| Hosts              | Direction | Port                    | Purpose                                                                    |
|:-------------------|:---------:|:------------------------|:---------------------------------------------------------------------------|
| controllers, nodes |    in     | TCP 443  (configurable) | Web app and CLI client access to UCP.                                      |
| controllers        |    in     | TCP 2376 (configurable) | Swarm manager API endpoint, used by the UCP controller.                    |
| controllers, nodes |    in     | TCP 2377 (configurable) | Docker Engine port for communicating with other swarm nodes.               |
| controllers, nodes |  in, out  | UDP 4789                | Overlay networking.                                                        |
| controllers, nodes |  in, out  | TCP & UDP 7946          | Overlay networking.                                                        |
| controllers, nodes |    in     | TCP 12376               | Proxy for TLS, provides access to UCP, Docker Engine, and Docker Swarm.    |
| controllers        |    in     | TCP 12379               | Internal node configuration, cluster configuration, and HA.                |
| controllers        |    in     | TCP 12380               | Internal node configuration, cluster configuration, and HA.                |
| controllers        |    in     | TCP 12381               | Proxy for TLS, provides access to UCP.                                     |
| controllers        |    in     | TCP 12382               | Manages TLS and requests from the swarm manager.                           |
| controllers        |    in     | TCP 12383               | Used by the authentication storage backend.                                |
| controllers        |    in     | TCP 12384               | Used by authentication storage backend for replication across controllers. |
| controllers        |    in     | TCP 12385               | The port where the authentication service is exposed.                      |
| controllers        |    in     | TCP 12386               | Used by the authentication worker.                                         |

## Compatibility and maintenance lifecycle

Docker Datacenter is a software subscription that includes 3 products:

* CS Docker Engine,
* Docker Trusted Registry,
* Docker Universal Control Plane.

[Learn more about the maintenance lifecycle for these products](http://success.docker.com/Get_Help/Compatibility_Matrix_and_Maintenance_Lifecycle).

## Where to go next

* [UCP architecture](../architecture.md)
* [Plan a production installation](plan-production-install.md)
