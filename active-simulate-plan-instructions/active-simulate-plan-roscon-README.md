# ROSCON Workshop - Unknown Anomaly Handling

## Prerequisites
- Docker installed: https://docs.docker.com/get-docker/
- Linux/Ubuntu system with GUI support
- X11 display server running

## Setup

### 1. Pull the Docker Image
```bash
docker pull x9th/anomaly-sim:workshop
```
*Note: The image is approximately 6.5GB*

### 2. Enable GUI Access
```bash
xhost +local:root
```

### 3. Fix Docker Permissions (if needed)
If you encounter permission errors, run:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

## Running the Demos

### Step 1: Launch CoppeliaSim Simulator
Open a terminal and run:
```bash
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/0_launch_sim.sh
```
**Keep this terminal open** - CoppeliaSim must remain running for all demos

### Step 2: Run Examples (in a new terminal)

First, enable X11 access again in the new terminal:
```bash
xhost +local:root
```

#### Show Nominal Behavior
```bash
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/1_nominal.sh
```

#### Show Failure Scenarios
```bash
# Misalignment failure (C on B collapses)
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/2_failure_misalignment.sh

# Occlusion failure (B on A hits obstacle)
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/3_failure_occlusion.sh
```

#### Identify Anomalies Using MCTS
```bash
# Scenario 1 - Misalignment (15 iterations)
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/4_identify_anomaly1.sh

# Scenario 2 - Occlusion (15 iterations)
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/5_identify_anomaly2.sh

# Scenario 3 - Mixed scenario (25 iterations)
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/6_identify_anomaly3.sh
```

#### Recovery Planning with PDDL
```bash
# Recover from anomaly 1
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/7_recover_anomaly1.sh

# Recover from anomaly 2
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/8_recover_anomaly2.sh

# Recover from anomaly 3
docker run -it --rm \
    --network=host \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    x9th/anomaly-sim:workshop \
    demos/9_recover_anomaly3.sh
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| **Permission denied** | Run `newgrp docker` or prefix commands with `sudo` |
| **Display errors** | Ensure `xhost +local:root` was executed |
| **"Cannot connect to X server"** | Check DISPLAY variable: `echo $DISPLAY` |
| **CoppeliaSim not responding** | Check simulator is still running in first terminal |
| **Qt platform plugin error** | Restart Docker daemon: `sudo systemctl restart docker` |

## Workshop Overview

This system demonstrates automated anomaly detection and recovery in robotic manipulation tasks:

### Scenarios
1. **Anomaly 1**: Misalignment - Block C incorrectly positioned on B
2. **Anomaly 2**: Occlusion - Block B placement blocked by obstacle
3. **Anomaly 3**: Mixed - Combination of multiple anomalies

## System Requirements
- **OS**: Ubuntu 20.04/22.04 or compatible Linux distribution
- **RAM**: Minimum 8GB recommended
- **Storage**: 10GB free space
- **Graphics**: OpenGL 3.3+ support

## Contact
For issues or questions during the workshop, please ask the presenters.

---
*ROSCON Workshop - CONVINCE Project*
