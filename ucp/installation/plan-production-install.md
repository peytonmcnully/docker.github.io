---
aliases:
- /ucp/plan-production-install/
description: Learn about the Docker Universal Control Plane architecture, and the
  requirements to install it on production.
keywords:
- docker, ucp, install, checklist
menu:
  main:
    identifier: ucp_plan_production_install
    parent: mn_ucp_installation
    weight: 10
title: Plan a production installation
---

# Plan a production installation

Docker Universal Control Plane can be installed on-premises, or
on a virtual private cloud. If you've never used Docker UCP before,
you should start by [installing it on a sandbox](../install-sandbox.md).

This article explains what you need to consider before deploying
Docker Universal Control Plane.

## System requirements

Before installing UCP, you should make sure all nodes of your cluster
comply with the [system requirements](system-requirements.md).


## Hostname strategy

Docker UCP requires CS Docker Engine to run. Before installing the commercially
supported Docker Engine on your cluster nodes, you should plan for a common
hostname strategy.

Decide if you want to use short hostnames like `engine01` or Fully Qualified
Domain Names (FQDN) likes `engine01.docker.vm`. Independently of your choice,
ensure your naming strategy is consistent across the cluster, since Docker
Engine and UCP use hostnames.

As an example, if your cluster has 4 hosts you can name them:

```bash
engine01.docker.vm
engine02.docker.vm
engine03.docker.vm
engine04.docker.vm
```

## Static IP addresses

Docker UCP requires each node on the cluster to have a static IP address.
Before installing UCP, ensure your network and nodes are configured to support
this.

## Load balancing strategy

Docker UCP does not include a load balancer. You can configure your own
load balancer to balance user requests across all controller nodes.

If you plan on using a load balancer, you need to decide whether you are going
to add the nodes to the load balancer using their IP address, or their FQDN.
Independently of what you choose, it should be consistent across nodes.

After that, you should take note of all IPs or FQDNs before starting the
installation.

## Load balancing UCP and DTR

By default, both UCP and DTR use port 443. If you plan on deploying UCP and DTR,
your load balancer needs to distinguish traffic between the two by IP address
or port number.

* If you want to configure your load balancer to listen on port 443:
    * Use one load balancer for UCP, and another for DTR,
    * Use the same load balancer with multiple virtual IPs.
* Configure your load balancer to expose UCP or DTR on a port other than 443.


## Using external CAs

You can customize UCP to use certificates signed by an external Certificate
Authority. When using your own certificates, take in consideration that you
need to have a certificate bundle that has:

* A ca.pem file with the root CA public certificate,
* A cert.pem file with the server certificate and any intermediate CA public
certificates. This certificate should also have SANs for all addresses used to
reach the UCP controller,
* A key.pem file with server private key.

You can have a certificate for each controller, with a common SAN. As an
example, on a three node cluster you can have:

* engine01.docker.vm with SAN ducp.docker.vm
* engine02.docker.vm with SAN ducp.docker.vm
* engine03.docker.vm with SAN ducp.docker.vm


Alternatively, you can also install UCP with a single externally-signed
certificate for all controllers rather than one for each controller node.
In that case, the certificate files will automatically be copied to any new
controller nodes joining the cluster or being promoted into controllers.

## Where to go next

* [UCP system requirements](system-requirements.md)
* [Install UCP for production](install-production.md)
