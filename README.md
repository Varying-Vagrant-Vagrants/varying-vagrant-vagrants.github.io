# varyingvagrantvagrants.org [![Build Status](https://travis-ci.org/Varying-Vagrant-Vagrants/varyingvagrantvagrants.org.svg?branch=master)](https://travis-ci.org/Varying-Vagrant-Vagrants/varyingvagrantvagrants.org)

This repository provides the code and content for [varyingvagrantvagrants.org](https://varyingvagrantvagrants.org), [VVV](https://github.com/Varying-Vagrant-Vagrants/vvv)'s official website.

The `master` branch of this repository deploys to production under [varyingvagrantvagrants.org](https://varyingvagrantvagrants.org). It also pulls the [CONTRIBUTING.md](https://github.com/Varying-Vagrant-Vagrants/VVV/blob/develop/.github/CONTRIBUTING.md) and [CHANGELOG.md](https://github.com/Varying-Vagrant-Vagrants/VVV/blob/develop/CHANGELOG.md) files from the `develop` branch of [VVV](https://github.com/Varying-Vagrant-Vagrants/VVV).

Pull requests can be opened against this repository for the following:

* Issues with deployment configuration through Travis CI.
* Issues with Jekyll configuration.
* Updates to the varyingvagrantvagrants.org home page.
* Updates to varyingvagrantvagrants.org blog posts.
* Updates to VVV documentation.

Once a pull request is merged to `master`, Travis CI is used to deploy the built site files to an AWS S3 bucket. Nginx is used to direct traffic to the correct branch directory in the bucket.

Issues to discuss changes to the code and documentation should be opened at the main [VVV repository](https://github.com/Varying-Vagrant-Vagrants/vvv).
