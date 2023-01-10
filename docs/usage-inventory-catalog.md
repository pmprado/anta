# Inventory & Catalog definition

This page describes how to create an inventory and a tests catalog.

## Create an inventory file

`check-devices` needs an inventory file to list all devices to tests. This inventory is a YAML file with the folowing keys:

```yaml
anta_inventory:
  hosts:
    - host: 1.1.1.1
  networks:
    - network: '1.1.2.0/24'
  ranges:
    - start: 1.1.3.10
      end: 1.1.3.21
```

In this configuration file, you can use different device definitions:

- __hosts__: is a list of single Arista EOS host to check.
- __networks__: is a list of networks where check-devices.py will search for active EOS devices.
- __ranges__: is a range of IP addresses where check-devices.py will search for active EOS devices.

Your inventory file can be based on any of these 3 keys and shall start with `anta_inventory` key.

Besides this standard definition, you can also define some tags to target a subset of devices during your tests exeution. it can be useful to only run test about VXLAN on leaf only and skip underlay devices.

```yaml
anta_inventory:
  hosts:
    - host: 1.1.1.1
      tags: ['leaf', 'border']
  networks:
    - network: '1.1.2.0/24'
      tags: ['leaf']
  ranges:
    - start: 1.1.3.10
      end: 1.1.3.21
      tags: ['spines']
```

Tag definition is a list of string you defined according your own setup. If not defined, a default tag (`default`) is generated during script execution.

## Test Catalog

In addition to your inventory file, you also have to define a catalog of tests to execute against all your devices. This catalogue list all your tests and their parameters.

Its format is a YAML file and keys are tests functions inherited from the python path. Let's take an example below:

### Default tests catalog

All tests are located under `anta.tests` module and are categorised per family (one submodule). So to run test for software version, you can do:

```yaml
anta.tests.software:
  - verify_eos_version:
```

!!! information
    With this approach, it means you can load your own tests collection as described in the next section.

It will load the test `verify_eos_version` located in `anta.tests.software`. But since this function has parameters, we will create a catalog with the following structure:

```yaml
anta.tests.software:
  - verify_eos_version:
      # List of allowed EOS versions.
      versions:
        - 4.25.4M
        - 4.26.1F
```

To get a list of all available tests and their respective parameters, you can read the [tests section](./api/tests.md) of this website.

The following example gives a very minimal tests catalog you can use in almost any situation

```yaml
---
# Load anta.tests.software
anta.tests.software:
  # Verifies the device is running one of the allowed EOS version.
  - verify_eos_version:
      # List of allowed EOS versions.
      versions:
        - 4.25.4M
        - 4.26.1F

# Load anta.tests.system
anta.tests.system:
  # Verifies the device uptime is higher than a value.
  - verify_uptime:
      minimum: 1

# Load anta.tests.configuration
anta.tests.configuration:
  # Verifies ZeroTouch is disabled.
  - verify_zerotouch:
  - verify_running_config_diffs:
```

### Custom tests catalog

In case you want to leverage your own tests collection, you can use the following syntax:

```yaml
<your package name>:
  - <your test in your package name>:
```

So for instance, it could be:

```yaml
titom73.tests.system:
  - verify_platform:
    type: ['cEOS-LAB']
```

!!! note "How to create custom tests"
    To create your custom tests, you should refer to this [following documentation](usage-as-python-lib.md#test-structure)