---
layout: components
---

The VISP Ecosystem consists of two major components: the VISP Marketplace and the VISP Runtime. The VISP Marketplace aims at creating an ecosystem for IoT-based topologies by minimizing the required effort for the user to design a topology. The VISP Runtime complements the VISP Marketplace, by providing a platform to execute the previously designed topologies.

# Architecture

TBD


# Runtime

TBD

## Web GUI

TBD

## Resource Provider

TBD

## Reasoner

TBD

## Topology Parser

The VISP topology parser is used to make sense of input files in the **VISP topology description language** format. Such files are either created manually by the user (or by the Topology Builder in the VISP Marketplace) or they can be generated automatically by the VISP Runtime in the process of executing topology updates at runtime.

The parser is based on Antlr4 and uses a fairly simple grammar. An exemplary input file for a topology with a source, two processing nodes and a sink may look like the following:

```
$source = Source() {
  concreteLocation = 192.168.0.1/openstackpool,
  type             = source,
  outputFormat     = "temperature data from sensor XYZ",
  #meaningless for sources and should be ignored by parser:
  expectedDuration = 15
}

$step1 = Operator($source) {
  allowedLocations = 192.168.0.1/openstackpool 192.168.0.1/openstackpool 192.168.0.3/openstackpool 192.168.0.4/openstackpool 192.168.0.5/openstackpool,
  concreteLocation = 192.168.0.1/openstackpool,
  inputFormat      = step1,
  type             = step1,
  outputFormat     = step2,
  size             = small,
  stateful = false
}

$step2 = Operator($step1) {
  allowedLocations = 192.168.0.1/openstackpool,
  inputFormat      = step1,
  type             = "step2",
  outputFormat     = "step3",
  size             = small,
  stateful         = true,
  expectedDuration = 15,
  scalingCPUThreshold = 20,
  scalingMemoryThreshold = 55,
  queueThreshold = 11
}
$log = Sink($step5) {
 concreteLocation = 192.168.0.1/openstackpool,
 inputFormat      = "transformed data from step 5",
 type             = "logger for temperature data",
}
```

Each node in the topology is represented by an entry starting with `$<name> =` defining the node's identifier.
This is followed by a **type** - either Source, Operator or Sink. One or more sources are then defined in brackets where each source refers to a node that must also be defined in the same topology file (but not necessarily in a line before they are used as sources).

In curly braces, the following options can be specified:

* `concreteLocation`<br />
Location (rabbitmq host, resource pool) where the operator should be deployed<br /><br />
* `allowedLocations`<br />
List of locations where the operator can be deployed (a concrete location is picked from this list if none is explicitly provided)<br /><br />
* `type`<br />
<br /><br />
* `inputFormat`<br />
Which kinds of input format are expected<br /><br />
* `outputFormat`<br />
Which output formats are produced<br /><br />
* `size`<br />
How much disk space does the operator use (either *small*, *medium* or *large*)<br /><br />
* `stateful`<br />
Whether or not the operator shows a stateful behavior<br /><br />
* `expectedDuration`<br />
How long is the expected duration to process one item (in seconds)
<br /><br />
* `scalingCPUThreshold`<br />
CPU threshold
<br /><br />
* `scalingMemoryThreshold`<br />
Memory threshold
<br /><br />
* `queueThreshold`<br />
Queue threshold

### Locations

Each node is deployed in one or more locations. A location is uniquely specified by an infrastructure host and a resource pool. The first is responsible for routing the data stream inputs while the second is the identifier of the (cloud) resource pool where the operator is actually executed.


# Processing Nodes

TBD

# Data Provider

TBD
