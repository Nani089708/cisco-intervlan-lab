<div align="center">

# 🛡️ Enterprise Edge Security Lab: FortiGate + Cisco Core

![Cisco](https://img.shields.io/badge/Cisco-L2%2FL3%20Switch-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Fortinet](https://img.shields.io/badge/Fortinet-FortiGate%20VM-EE3124?style=for-the-badge&logo=fortinet&logoColor=white)
![Topology](https://img.shields.io/badge/Architecture-Router--on--a--Stick-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Lab%20Status-Verified%20%26%20Tested-success?style=for-the-badge)

<p align="center">
  <b>Production-grade network topology integrating a FortiGate Next-Generation Firewall with Cisco Layer 2/3 Switching for secure Inter-VLAN routing, perimeter security, and NAT/PAT inspection.</b>
</p>

</div>

---

## 📐 Network Architecture Diagram

```mermaid
flowchart TD
    subgraph WAN [External Network]
        Internet((Internet / ISP))
    end

    subgraph Perimeter [Perimeter Security]
        FGT[FortiGate Firewall\nport1: WAN (DHCP)\nport2: Trunk to LAN]
    end

    subgraph Core [Internal Distribution]
        SW[Cisco Catalyst 2960\nGi0/1: 802.1Q Trunk]
    end

    subgraph LAN [Segmented Subnets]
        HR[HR Dept\nVLAN 10\n192.168.10.0/24]
        IT[IT Dept\nVLAN 20\n192.168.20.0/24]
        DMZ[Servers / DMZ\nVLAN 30\n192.168.30.0/24]
    end

    Internet <-->|Static Default Route / NAT| FGT
    FGT <-->|VLAN Sub-interfaces 10, 20, 30| SW
    SW --- HR
    SW --- IT
    SW --- DMZ

    classDef fgtStyle fill:#ee3124,stroke:#333,stroke-width:2px,color:#fff;
    classDef ciscoStyle fill:#005073,stroke:#333,stroke-width:2px,color:#fff;
    classDef lanStyle fill:#71c7ec,stroke:#333,stroke-width:1px;
    classDef wanStyle fill:#fdb813,stroke:#333,stroke-width:1px;

    class FGT fgtStyle;
    class SW ciscoStyle;
    class HR,IT,DMZ lanStyle;
    class Internet wanStyle;
