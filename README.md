# A pipeline for Robot Deliberation from the CONVINCE toolbox

This repository contains materials for the ROSCon Fr/De 2025 workshop W5. You can find the [slides here]().

__The material is perfectly usable as a guided tutorial to learn all of the presented technologies at your own pace.__

## Introduction

Robots are increasingly being deployed outside strictly controlled environments. However, when confronted with unexpected situations, they often struggle to take appropriate action and require human intervention. Robot deliberation technologies employ models of the robot and its environment to facilitate high-level decision-making, thereby enhancing flexibility and adaptability in the execution of capabilities such as navigation and manipulation.

The CONVINCE Project(*) develops an open-source toolbox(**) to enable robust robot deliberation. This workshop is a hands-on session where participants will setup and run our pipeline of components from the CONVINCE toolbox, including semantic anchoring, planning, verification and run-time monitoring of system properties. Semantic anchoring produces a symbolic representation of current observations of operational environment for a task planner, which computes an action plan for a given goal. Verification allows to check system performance. Run-time monitors detect violations of properties to enable dynamic replanning, that adapts the system to unexpected situations.

## Setup

### System Requirements

We highly recommend a host PC running Ubuntu 22.04 or 24.04.

If you are using macOS or Windows, you should install virtualization software such as [VirtualBox](https://www.virtualbox.org/) or [VMWare](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion).
Then, set up an Ubuntu 22.04 or 24.04 virtual machine.

You also need to have Docker and Docker Compose installed on your system.
If you do not have these tools set up:

* Install Docker Engine using [these instructions](https://docs.docker.com/engine/install/ubuntu/).
  * __IMPORTANT:__ Make sure you also go through the [Linux post-installation steps](https://docs.docker.com/engine/install/linux-postinstall/).
* Install Docker Compose using [these instructions](https://docs.docker.com/compose/install/).

Once you are able to run `docker` and `docker compose` commands without `sudo`, you can move on to the installation steps below.

```bash
docker run hello-world
docker compose --help
```

### Installation

Open a terminal window and give the following commands:

#### Design-time Verification (AS2FM)

```sh
git clone git@github.com:convince-project/AS2FM.git
cd AS2FM
docker compose pull
```

#### Run-time Monitoring (MOON)

```sh
git clone git@github.com:convince-project/MOON.git
cd MOON
docker compose pull
```

#### Semantic Anchoring (SIT-AW-ANCHORING):

```sh
docker pull mmorelli1/sitaw-env-rosconfr25:0.1.0
```

#### Planning (ACTIVE-/SIMULATE-PLAN):

```sh
docker pull x9th/anomaly-sim:workshop
```

#### Additional Resources (this repository)

In the terminal window, give the following commands:

```sh
git clone https://github.com/convince-project/rosconfrde25-workshop.git
```

The following subsections are specific for each technology (if needed).

##### Semantic Anchoring (SIT-AW-ANCHORING):

Start container with mounted volumes:

```sh
cd rosconfrde25-workshop/sit-aw-anchoring-resources/
make start-docker
```

Build the resources (in container):
```sh
colcon build --symlink-install
```

##### Planning (ACTIVE-/SIMULATE-PLAN):

_In Progress_.

## Next steps

If you are done with your setup and verified that everything is working, you can continue to learn about the tutorials.

## Tutorials

### Design-time Verification (AS2FM)

_In Progress_.

### Run-time Monitoring (MOON)

_In Progress_.

### Semantic Anchoring (SIT-AW-ANCHORING):

Refer to the pdf file `rosconfrde25-workshop/sit-aw-anchoring-resources/sit-aw-anchoring-handson-35mins.pdf`

### Planning (ACTIVE-/SIMULATE-PLAN):

_In Progress_.
