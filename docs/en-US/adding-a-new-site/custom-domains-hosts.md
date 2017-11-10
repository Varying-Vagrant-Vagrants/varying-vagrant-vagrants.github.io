---
category: 3. Adding a New Site
order: 2
title: Custom Domains and Hosts
description: Define custom domains in the sites section of vvv-custom.yml. vvv-init.sh can be used for edge circumstances.
permalink: /docs/en-US/adding-a-new-site/custom-domains-hosts/
---

There are 3 ways to define hosts

 - The main `vvv-custom.yml` config file
 - A `vvv-hosts` file
 - The `vvv-init.sh` file

The recommended way is to use the `vvv-custom.yml` file. `vvv-hosts` is supported for backwards compatibility, and `vvv-init.sh` can be used for edge circumstances.

When changing hosts, the Nginx config will need updating so that Nginx knows to listen for requests on those domains. If this isn't done, the VVV dashboard will appear instead of the desired site.

<div class="note">
	<h5>Don't forget to Reprovision on Changes</h5>
	If you modify <code>vvv-custom.yml</code>, you must reprovision for the changes to take effect. Run <code>vagrant reload</code> after making changes.
</div>

## vvv-custom.yml

When adding a site in `vvv-custom.yml`, add a hosts section listing the domains of that site. For example:

```yaml
example:
  hosts:
    - example.com
```

This will map example.com to the example site, and update the HOST file on your machine.

## vvv-hosts

VVV 1 added hosts using a file named `vvv-hosts`, and VVV 2 continues support for this for backwards compatibility reasons. Place this as a text file with no file extension in a `provision` subfolder, or in the root of the site.

Here's an example that adds 2 domains:

```
example.com
example.net
```
