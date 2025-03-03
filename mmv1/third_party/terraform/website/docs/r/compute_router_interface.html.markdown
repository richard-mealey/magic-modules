---
subcategory: "Compute Engine"
page_title: "Google: google_compute_router_interface"
description: |-
  Manages a Cloud Router interface.
---

# google\_compute\_router_interface

Manages a Cloud Router interface. For more information see
[the official documentation](https://cloud.google.com/compute/docs/cloudrouter)
and
[API](https://cloud.google.com/compute/docs/reference/latest/routers).

## Example Usage

```hcl
resource "google_compute_router_interface" "foobar" {
  name       = "interface-1"
  router     = "router-1"
  region     = "us-central1"
  ip_range   = "169.254.1.1/30"
  vpn_tunnel = "tunnel-1"
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) A unique name for the interface, required by GCE. Changing
    this forces a new interface to be created.

* `router` - (Required) The name of the router this interface will be attached to.
    Changing this forces a new interface to be created.

In addition to the above required fields, a router interface must have specified
either `ip_range` or exactly one of `vpn_tunnel` or `interconnect_attachment`,
or both.

- - -

* `ip_range` - (Optional) IP address and range of the interface. The IP range must be
    in the RFC3927 link-local IP space. Changing this forces a new interface to be created.

* `vpn_tunnel` - (Optional) The name or resource link to the VPN tunnel this
    interface will be linked to. Changing this forces a new interface to be created. Only
    one of `vpn_tunnel` and `interconnect_attachment` can be specified.

* `interconnect_attachment` - (Optional) The name or resource link to the
  VLAN interconnect for this interface. Changing this forces a new interface to
  be created. Only one of `vpn_tunnel` and `interconnect_attachment` can be
  specified.

* `redundant_interface` - (Optional) The name of the interface that is redundant to
  this interface. Changing this forces a new interface to
  be created.

* `project` - (Optional) The ID of the project in which this interface's router belongs. If it
    is not provided, the provider project is used. Changing this forces a new interface to be created.

* `region` - (Optional) The region this interface's router sits in. If not specified,
    the project region will be used. Changing this forces a new interface to be
    created.

## Attributes Reference

In addition to the arguments listed above, the following computed attributes are exported:

* `id` - an identifier for the resource with format `{{region}}/{{router}}/{{name}}`

## Timeouts

This resource provides the following
[Timeouts](/docs/configuration/resources.html#timeouts) configuration options:

- `create` - Default is 4 minutes.
- `delete` - Default is 4 minutes.

## Import

Router interfaces can be imported using the `region`, `router`, and `name`, e.g.

```
$ terraform import google_compute_router_interface.foobar us-central1/router-1/interface-1
```
