# Batch Connect - OSC Jupyter Notebook

![GitHub Release](https://img.shields.io/github/release/osc/bc_osc_jupyter.svg)
[![GitHub License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)

An interactive app designed for OSC OnDemand that launches a Jupyter Notebook
server within an Owens batch job.

## Prerequisites

This Batch Connect app requires the following software be installed on the
**compute nodes** that the batch job is intended to run on (**NOT** the
OnDemand node):

- [Lmod] 6.0.1+ or any other `module purge` and `module load <modules>` based
  CLI used to load appropriate environments within the batch job before
  launching the Jupyter Notebook server.
- [Jupyter Notebook] 4.2.3+ (earlier versions are untested but may work for
  you)
- [OpenSSL] 1.0.1+ (used to hash the Jupyter Notebook server password)

[Jupyter Notebook]: https://jupyter.org/
[OpenSSL]: https://www.openssl.org/
[Lmod]: https://www.tacc.utexas.edu/research-development/tacc-projects/lmod

## Install

Use Git to clone this app and checkout the desired branch/version you want to
use:

```sh
scl enable git19 -- git clone <repo>
cd <dir>
scl enable git19 -- git checkout <tag/branch>
```

You will not need to do anything beyond this as all necessary assets are
installed. You will also not need to restart this app as it isn't a Passenger
app.

To update the app you would:

```sh
cd <dir>
scl enable git19 -- git fetch
scl enable git19 -- git checkout <tag/branch>
```

Again, you do not need to restart the app as it isn't a Passenger app.

## Contributing

1. Fork it ( https://github.com/OSC/bc_osc_jupyter/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## CHPC specifics

This app is using the local dynamic partition list as described in https://osc.github.io/ood-documentation/master/app-development/tutorials-interactive-apps/add-custom-queue/local-dynamic-list.html

Since our available partitions, apart from the partitions named the same as the cluster, also include partitions owned by PI, which are named the same as their group name (most of the time), we get the available partition list by grepping the sinfo output for the required keywords (in this case "kingspeak" and all the Linux groups the user is in). Thus the more compilcated "cmd" command in form.yml.erb.

