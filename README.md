## Node Breakdown

### Load Balancer Nodes
| Node            | IP Address      | Description                          |
|----------------|----------------|--------------------------------------|
| Load Balancer 1 | 192.168.1.10   | First load balancer for HA setup    |
| Virtual IP (VIP) | 192.168.1.100 | Floating IP for load balancer pair  |

### Control Plane Nodes
| Node            | IP Address      | Description                                  |
|----------------|----------------|----------------------------------------------|
| Control Plane 1 | 192.168.1.50   | First control plane node                    |
| Control Plane 2 | 192.168.1.51   | Second control plane node                   |

### Worker Nodes
| Node            | IP Address      | Description                                  |
|----------------|----------------|----------------------------------------------|
| Worker Node 1  | 192.168.1.60   | First worker node for application workloads |
| Worker Node 2  | 192.168.1.61   | Second worker node for application workloads |


