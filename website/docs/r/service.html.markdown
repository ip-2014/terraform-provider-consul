---
layout: "consul"
page_title: "Consul: consul_service"
sidebar_current: "docs-consul-resource-service"
description: |-
  A high-level resource for creating a Service in Consul. Since Consul requires clients to register services with either the catalog or an agent, `consul_service` may register with either the catalog or an agent, depending on the configuration of `consul_service`. For now, `consul_service` always registers services with the agent running at the address defined in the `consul` resource. Health checks are not currently supported.
---

# consul_service

A high-level resource for creating a Service in Consul. Currently,
defining health checks for a service is not supported.

**Most users should not use this resource**. When using Consul with
compute instances, it's better to install
[the Consul Agent](https://www.consul.io/docs/agent/basics.html)
on these machines and register services via the agent. This ensures
that services get assigned to the appropriate Consul "nodes" and
allows service health to integrate with general node health as
reported by the agent.

To register a non-compute resource, such as a hosted database,
as a service, as described in
[Consul's _External Services_ guide](https://www.consul.io/docs/guides/external.html),
use [`consul_catalog_entry`](catalog_entry.html) instead, which
can create an arbitrary service record in the Consul catalog.

## Example Usage

```hcl
resource "consul_service" "google" {
  address = "www.google.com"
  name    = "google"
  port    = 80
  tags    = ["tag0", "tag1"]
}
```

## Argument Reference

The following arguments are supported:

* `service_id` - (Optional, string) The ID of the service, defaults to the value of `name`
  if not supplied.

* `address` - (Optional, string) The address of the service. Defaults to the
  address of the agent.

* `name` - (Required, string) The name of the service.

* `port` - (Optional, int) The port of the service.

* `tags` - (Optional, set of strings) A list of values that are opaque to Consul,
  but can be used to distinguish between services or nodes.


## Attributes Reference

The following attributes are exported:

* `service_id` - The id of the service, defaults to the value of `name`.
* `address` - The address of the service.
* `name` - The name of the service.
* `port` - The port of the service.
* `tags` - The tags of the service.
