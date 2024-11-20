# Advanced Proxmox VE Homelab

This repository showcases my advanced Proxmox VE homelab setup, featuring multiple virtual machines for various purposes including networking, containerization, home automation, media serving, and system monitoring.
## Components

### Proxmox VE Host

- The main hypervisor running all virtual machines
- Provides resource allocation and management for VMs


### VM1: pfSense

- Acts as the main router and firewall for the entire network
- Manages VLANs for network segmentation
- Provides VPN access for remote management and access


### VM2: Kubernetes

- Runs a Kubernetes cluster for container orchestration
- Hosts various web applications and databases
- Allows for easy deployment and scaling of services


### VM3: Home Assistant

- Central hub for home automation
- Integrates with various smart home devices
- Allows for complex automation scenarios and routines


### VM4: Blackbox & Adobe Storage

- Runs Blackbox Media Server for serving and gathering media files
- Acts as a centralized storage solution for Adobe Creative Suite applications
- Manages both media files and Adobe project files
- Serves media to connected devices on the network


### VM5: Monitoring

- Runs a comprehensive monitoring stack:

- Prometheus for metrics collection
- Grafana for visualization and dashboards
- ELK Stack (Elasticsearch, Logstash, Kibana) for log management



- Monitors all other VMs and the Proxmox host itself


## Setup and Configuration Notes

1. Proxmox VE is installed on bare metal hardware
2. Each VM is allocated resources based on its specific needs
3. Network is segmented using VLANs managed by pfSense
4. Kubernetes cluster is set up using k3s for lightweight orchestration
5. Home Assistant is configured with Z-Wave and Zigbee controllers for device communication
6. Blackbox Media Server is configured to scan and index media files regularly
7. Adobe Creative Suite files are stored on a dedicated, high-performance storage volume
8. Monitoring system is set up with alerting for critical events


## Future Expansion Ideas

1. Implement a backup solution using Veeam or similar software
2. Add a GitLab instance on the Kubernetes cluster for CI/CD pipelines
3. Expand the storage capabilities with a dedicated NAS
4. Implement machine learning projects using GPU passthrough
5. Set up a mail server for a self-hosted email solution

## Homelab Architecture

```mermaid
graph TD
    A[Proxmox VE Host]
    B[VM1: pfSense]
    C[VM2: Kubernetes]
    D[VM3: Home Assistant]
    E[VM4: Blackbox & Adobe Storage]
    F[VM5: Monitoring]

    A -->|Hosts| B & C & D & E & F
    B -->|Routes| C & D & E & F
    F -->|Monitors| A & B & C & D & E

    B -->|Firewall, VPN, VLANs| Internet((Internet))
    C -->|Runs| WebApps[Web Apps] & DB[(Databases)]
    D -->|Controls| SmartDevices{Smart Devices}
    E -->|Serves Media| Clients([Connected Devices])
    E -->|Stores Files| AdobeApps[Adobe Creative Suite]
    F -->|Includes| Prometheus & Grafana & ELK[ELK Stack]

    subgraph VM4Content [VM4: Blackbox & Adobe Storage]
        Blackbox[Blackbox Media Server]
        Storage[Network Storage]
        Blackbox -->|Manages| Storage
        Storage -->|Stores| MediaFiles[Media Files]
        Storage -->|Stores| AdobeFiles[Adobe Project Files]
    end

    E --- VM4Content

    classDef vm fill:#f9f,stroke:#333,stroke-width:2px;
    class B,C,D,E,F vm;
