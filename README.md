# Acceptance Pipelines

This repo contains standalone acceptance test pipelines for OpenVox projects.

It leverages [shared-actions](https://github.com/OpenVoxProject/shared-actions) for underlying work.

## Actions

### openvox_acceptance_pipeline

The [openvox_acceptance_pipeline.yml](.github/workflows/openvox_acceptance_pipeline.yml) pipeline runs the acceptance suites for openvox, openvox-agent and openvox-server at given git refs against a set of pre-built packages as referenced by versions/collections from the apt/yum.voxpupuli.org or artifacts.voxpupuli.org servers.

It does not build packages yet.

This pipeline isn't doing anything different than the individual project pipelines:

* [openvox-server acceptance](https://github.com/OpenVoxProject/openvox-server/actions/workflows/acceptance.yml)
* [openvox acceptance](https://github.com/OpenVoxProject/openvox/actions/workflows/acceptance.yml)
* [openvox-agent acceptance](https://github.com/OpenVoxProject/openvox-agent/actions/workflows/acceptance.yml)
* [openvoxdb acceptance](https://github.com/OpenVoxProject/openvoxdb/actions/workflows/acceptance.yml)

All of these pipelines use [beaker_acceptance.yml](https://github.com/OpenVoxProject/shared-actions/blob/main/.github/workflows/beaker_acceptance.yml) under the hood. The pipeline, at the moment, is just a convenience for running them all in one spot and referencing all the results together for one identified collection of packages.

#### Arm64 Support

You can run the acceptance pipeline on arm64 guests in gha by
setting `guest_arch` to `arm64`. Currently though this has serious
limitations due to the lack of kvm support on the gha arm64 runners.
(https://github.com/actions/runner-images/issues/14062) Consequently,
the kvm_automation_tooling module runs the arm64 guests in qemu
instead, and they are *very* slow.

The openvox suite can be run successfully on a subset of platforms by
sharding the test suite into four tag groups that allow it to complete
within the 6 hour gha job limit (they actually end up taking about 4
hours this way). Right now, `beaker_acceptance` uses Alma9 and
debian13, which just happen to be two of the faster arm64 platforms
running under qemu...for reasons?

The openvox-agent suite generally completes as is.

For openvox-server, alma9/rocky9 successfully complete. The other
platforms tend to have a few consistent ssh connection failures.

Openvoxdb I have not tried to get working. Given the difficulty with
the openvox-server suite, I don't think it's worth the effort at the
moment.

In general, you may be better off just running the
openvoxproject/openvox acceptance pipeline directly (which is both
openvox and openvox-agent), since these are really the only two suites
that will complete.

## TODO

* Add support for building packages prior to running acceptance tests.
* Add openfact
* Upgrade testing
* ???
