# Overview

This repo contains HOT orchestartion templates used to build the UKCloud integration test servers.

The templates use Ansible to build a CentOS7 server with tempest and refstack installed and configured.

We provide this template to our customers to understand how we test end user scenarios. The aim is:

  * To be transparent about our tests
  * To allow customers to build a server capapable of running the integration tests so they can develop and contribute their own

**Note:** The HOT templates also checkout the custom UKCloud scenarios

## Tempest
Tempest is an OpenStack project dedicated to testing. It provides coverage in the following forms:

  * API - tests that the API functions as expected, both during success and failure
  * Scenario - Allows complex user based scenarios to be setup to allow full workflows to be tested
  * Stress - Allows for complex stress testing workloads to be executed

## RefStack
RefStack is a wrapper for tempest that allows for OpenStack compatibilty testing to make sure UKClouds OpenStack services are consistent between other OpenStack cloud providers.

# Setup

Amend the environment file so it is represntive of the connection details

Run:

```
openstack stack create -f yaml -t tempest-infrastructure.yaml -e environment.yml tempest --wait
```

# Running tests

Once the server is deployed access it via ssh

```
ssh centos@{public IP}
```

## Tempest

Individual UKCloud tests can be run with:

```
cd /home/centos/tempest
testr run tempest.scenario.test_minimum_basic.TestMinimumBasicScenario --concurrency=1
```

The entire tempest suite can be run with:

```
cd /home/centos/tempest
./run_tempest.sh
```
