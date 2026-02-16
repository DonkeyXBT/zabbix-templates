# Zabbix SNMP Templates

A collection of custom Zabbix templates for monitoring infrastructure hardware via SNMP.
All templates are in **Zabbix 6.4 YAML** export format and can be imported directly through the Zabbix web UI.

---

## Templates

### HPE StoreEver MSL6480 Tape Library

**File:** `HPE_StoreEver_MSL6480_Template.yaml`
**MIB:** HP-httpManageable-MIB (`1.3.6.1.4.1.11.2.36.1`)

Comprehensive monitoring for the HPE StoreEver MSL6480 tape library and its internal components (drives, robotics, I/O blades, etc.).

**What it monitors:**

| Category | Details |
|---|---|
| **ICMP Availability** | Ping, packet loss, response time |
| **MIB-II System** | sysDescr, sysUpTime, sysName, sysContact, sysLocation, sysObjectID |
| **Device Health** | Per-component health status (OK / Warning / Critical / Non-Recoverable) via SNMP discovery |
| **Device Inventory** | Manufacturer, product name, serial number, firmware version, hardware version, ROM version, asset number |
| **Device Location** | Contact person/phone/email/pager, location, rack ID, rack position |
| **Entity Relationships** | Sub-components, attached entities, cluster nodes with IP addresses and management URLs |
| **Licensing (CVTL)** | License status, key, duration (permanent/temporary), expiration date, quantity |
| **SNMP Traps** | Health state changes (Unknown/OK/Warning/Critical/Non-Recoverable), agent shutdown, device added/removed |

**Triggers included:**
- Device unreachable (ICMP)
- SNMP agent unavailable
- Device restarted (uptime < 10 min)
- Per-component health degradation (Warning / Critical / Non-Recoverable / Unknown)
- Health status change detection
- Serial number or firmware version change (hardware replacement / update detection)
- License not active
- All 9 SNMP trap types with appropriate severities (INFO through DISASTER)

---

### Kemp LoadMaster Load Balancer

**File:** `kemp_loadmaster_template.yaml`
**MIB:** ONE4NET-MIB, IPVS-MIB, B100-MIB, CERTS-MIB (`1.3.6.1.4.1.12196`)

Full monitoring for Kemp LoadMaster load balancers including traffic, HA, virtual services, and SSL certificates.

**What it monitors:**

| Category | Details |
|---|---|
| **System Info** | Version, firmware, uptime |
| **HA Cluster** | Cluster status monitoring |
| **Global Traffic** | Connections, packets, bytes in/out |
| **TPS Metrics** | Total and SSL transactions per second |
| **Virtual Services** | Auto-discovery with full metrics per VS |
| **Real Servers** | Auto-discovery with health status per RS |
| **SSL Certificates** | Auto-discovery with expiry monitoring |
| **Performance** | Request/response times, RTT |

---

### APC ATS AP7721 (Automatic Transfer Switch)

**File:** `Template_APC_ATS_AP7721_Generic_SNMP.yaml`
**MIB:** SNMPv2-MIB, IF-MIB

Generic SNMP template for APC Automatic Transfer Switches. Works with both SNMPv2c and SNMPv3.

**What it monitors:**

| Category | Details |
|---|---|
| **System Info** | sysName, sysDescr, sysUpTime, sysContact, sysLocation |
| **Network Interfaces** | Auto-discovery with HC counters (traffic, errors, utilization) |

---

## Installation

1. Download the `.yaml` template file(s) you need
2. In Zabbix, navigate to **Data collection > Templates**
3. Click **Import** (top right)
4. Select the YAML file and click **Import**
5. Create or edit a host, add an **SNMP interface** with the correct IP/community/credentials
6. Link the imported template to the host

## Requirements

- **Zabbix Server** 6.4 or newer
- **SNMP** access (v2c or v3) to the target device
- For SNMP trap items: Zabbix SNMP trap receiver must be configured (`snmptrapd` + trap handler)

## License

These templates are provided as-is for community use. Feel free to modify and redistribute.
