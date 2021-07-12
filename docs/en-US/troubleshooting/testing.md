---
category: 5. Troubleshooting
order: 3
title: Testing
description: How To Test VVV
permalink: /docs/en-US/troubleshooting/testing/
---

## Main VVV Repo

To test changes to the main repo, we need to check that it doesn't break an existing VM, and that it doesn't stop new VVV installs from working.

### Checking An Existing VM

Take an existing VVV install, and switch to the branch that has the changes, then reprovision. GitHub will have CLI instructions for how to checkout the branch with the new changes near the merge button.

Once the folder has the changes, run `vagrant halt && vagrant up --provision`.

## Utilities

You can test a new utility by adding it to `config/config.yml` ([example file](https://github.com/Varying-Vagrant-Vagrants/VVV/blob/develop/config/default-config.yml)) and reprovisioning.

To test changes to the core provisioner, delete the `provision/utilities/core` folder, then change the `config/config.yml` file to match the repo and branch you'd like to test:

```yaml
utility-sources:
  core:
    repo: URL of repo to test
    branch: name of branch to test
```

Then, halt the VM and reprovision: `vagrant halt && vagrant up --provision`

## Dashboard

```yaml
```

## Custom Site Template

```yaml
  wordpress-two:
    skip_provisioning: false
    description: "A standard WP install, useful for building plugins, testing things, etc"
    repo: https://github.com/Varying-Vagrant-Vagrants/custom-site-template.git
    custom:
      # locale: it_IT
      delete_default_plugins: true
      install_plugins:
        - query-monitor
    hosts:
      - two.wordpress.test
```

If the pull request adds new parameters, check that they work as expected, and check that things still work if the parameter is missing/blank.

## Custom Site Template Develop

```yaml
  wordpress-trunk:
    skip_provisioning: true # provisioning this one takes longer, so it's disabled by default
    description: "An svn based WP Core trunk dev setup, useful for contributor days, Trac tickets, patches"
    repo: https://github.com/Varying-Vagrant-Vagrants/custom-site-template-develop.git
    hosts:
      - trunk.wordpress.test
```

This template generate a log of different logs to simplify the debugging and the output in console, for a better testing is better to check the log in `VVV/log/provisioners/<datetime>/provisioner-site-wordpress-trunk.log` and the other files generated.
