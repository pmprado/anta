**Table of Contents**

- [examples directory](#examples-directory)
  - [devices.txt file](#devicestxt-file)
  - [eos-commands.yaml file](#eos-commandsyaml-file)
  - [tests.yaml file](#testsyaml-file)
  - [demo directory](#demo-directory)
- [anta directory](#anta-directory)
- [documentation directory](#documentation-directory)
  - [generate-functions-documentation.py file](#generate-functions-documentationpy-file)
  - [overview.md file](#overviewmd-file)
  - [tests.md file](#testsmd-file)
- [scripts directory](#scripts-directory)
  - [check-devices-reachability.py file](#check-devices-reachabilitypy-file)
  - [clear-counters.py file](#clear-counterspy-file)
  - [collect-eos-commands.py file](#collect-eos-commandspy-file)
  - [check-devices.py file](#check-devicespy-file)
  - [evpn-blacklist-recovery.py file](#evpn-blacklist-recoverypy-file)
  - [collect-sheduled-show-tech.py file](#collect-sheduled-show-techpy-file)
- [tests directory](#tests-directory)
  - [unit-test.py file](#unit-testpy-file)
  - [mock-data directory](#mock-data-directory)
- [.github directory](#github-directory)
  - [workflows directory](#workflows-directory)
  
# [examples](examples) directory

## [devices.txt](devices.txt) file

The file [devices.txt](../examples/devices.txt) is the devices inventory.

The devices inventory is a text file with the devices IP address or hostnames (if resolvable with DNS or your hosts file). This file has one device per ligne.

## [eos-commands.yaml](../examples/eos-commands.yaml) file

The file [eos-commands.yaml](../examples/eos-commands.yaml) is a YAML file used to indicated the list of commands output we would like to collect from devices in text or json format.

## [tests.yaml](../examples/tests.yaml) file

The file [tests.yaml](../examples/tests.yaml) is a YAML file used to indicated the tests we would like to run. It is also used to indicated the parameters used by the tests.
Each test has an identifier which is then used in the tests report.
The tests are defined in the directory [anta](../anta/).

## [demo](demo) directory

The [demo](demo) directory shows a demo of this repository with an ATD (Arista Test Drive) instance.

# [anta](../anta/) directory

The directory [anta](../anta/) is a python package.

The python functions to test EOS devices are defined the python module [tests.py](../anta/tests.py) in the python package [anta](../anta/).

# [documentation](documentation) directory

## [generate-functions-documentation.py](../documentation/generate-functions-documentation.py) file

The script [generate-functions-documentation.py](generate-functions-documentation.py) is used to generate the functions documentation in markdown format.
It requires the installation of the package `lazydocs` that is indicated in the file [requirements-dev.txt](../requirements-dev.txt)

The functions to test EOS devices are coded in the python module [tests.py](../anta/tests.py) in the python package [anta](../anta).
These functions have docstrings.
The docstrings are used by the script [generate-functions-documentation.py](generate-functions-documentation.py) to generate the functions documentation in markdown format in the directory [documentation](documentation).

## [overview.md](overview.md) file

The [anta](../anta) python package documentation in markdown format.  
Generated by the script [generate-functions-documentation.py](generate-functions-documentation.py) and the docstrings.

## [tests.md](tests.md) file

The [anta](../anta) python package documentation in markdown format.  
Generated by the script [generate-functions-documentation.py](generate-functions-documentation.py) and the docstrings.

# [scripts](scripts) directory

## [check-devices-reachability.py](check-devices-reachability.py) file

The python script [check-devices-reachability.py](check-devices-reachability.py) is used to test devices reachability with eAPI.

The python script [check-devices-reachability.py](check-devices-reachability.py) takes as input a text file with the devices IP address or hostnames (when resolvable), and tests devices reachability with eAPI and prints the unreachable devices on the console.

## [clear-counters.py](clear-counters.py) file

The python script [clear-counters.py](clear-counters.py) is used to clear counters on EOS devices.

It takes as input a text file with the devices IP address or hostnames (when resolvable) and clears counters on these devices.

## [collect-eos-commands.py](collect-eos-commands.py) file

The python script [collect-eos-commands.py](collect-eos-commands.py) is used to collect commands output from EOS devices.

The python script [collect-eos-commands.py](collect-eos-commands.py):

- Takes as input:
  - A text file with the devices IP address or hostnames (when resolvable).
  - A YAML file with the list of EOS commands we would like to collect in text or JSON format.
- Collects the EOS commands from the devices, and saves the result in files.

## [check-devices.py](check-devices.py) file

The python script [check-devices.py](check-devices.py) is used to run tests on devices.

The python script [check-devices.py](check-devices.py):

- Imports the python functions defined in the directory [anta](anta).
  - These functions defined the tests.
- Takes as input:
  - A text file with the devices IP address or hostnames (when resolvable).
  - A YAML file with the list of the tests we would like to use and their parameters.
- Runs the tests, and prints the result on the console and saves the result in a file.

## [evpn-blacklist-recovery.py](evpn-blacklist-recovery.py) file

The python script [evpn-blacklist-recovery.py](evpn-blacklist-recovery.py) is used to clear on EOS devices the list of MAC addresses which are blacklisted in EVPN.

The python script [evpn-blacklist-recovery.py](evpn-blacklist-recovery.py) takes as input a text file with the devices IP address or hostnames (when resolvable) and run the command `clear bgp evpn host-flap` on the EOS devices.

## [collect-sheduled-show-tech.py](collect-sheduled-show-tech.py) file

The python script [collect-sheduled-show-tech.py](collect-sheduled-show-tech.py) is used to collect the scheduled show tech-support files from EOS devices.

It takes as input a text file with the devices IP address or hostname and collects the show tech-support files from these devices and save the files locally.
# [tests](tests) directory

## [unit-test.py](unit-test.py) file

The python script [unit-test.py](unit-test.py) is used to test the functions defined in the directory [test-eos](test-eos) without using actual EOS devices.
It requires the installation of the package `pytest` that is indicated in the file [requirements-dev.txt](requirements-dev.txt)

## [mock-data](mock-data) directory

The [mock-data](mock-data) directory has data used by the python script [unit-test.py](unit-test.py) to test the functions defined in the directory [test-eos](test-eos) without using actual EOS devices.

# [.github](.github) directory

## [workflows](workflows) directory

Configuration folder containing yaml files for GitHub Actions