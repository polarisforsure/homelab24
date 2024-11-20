# Advanced Proxmox VE Homelab

This repository showcases my advanced Proxmox VE homelab setup, featuring multiple virtual machines for various purposes including networking, containerization, home automation, media serving, and system monitoring.

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
