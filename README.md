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

All of these pipelines use [beaker_acceptance.yml](https://github.com/OpenVoxProject/shared-actions/blob/main/.github/workflows/beaker_acceptance.yml) under the hood. The pipeline, at the moment, is just a convenience for running them all in one spot and referencing all the results together for one identified collection of packages.

## TODO

* Add support for building packages prior to running acceptance tests.
* Add openvoxdb
* Add openfact
* Upgrade testing
* ???
