# Secure Edge-to-Cloud IoT Architecture — AWS (Tasmania Farmhouse)

A group project designing and deploying a **cloud-based smart logistics network** for grain storage and transport across three physical sites in Tasmania. Built as part of the Professional Practice module at Middlesex University London.

The system connects Raspberry Pi edge devices at a farm, storage facility, and transport hub to AWS cloud infrastructure — enabling real-time GPS tracking, automated inventory alerts, and secure data pipelines.

---

## 🌾 Problem Statement

Farmers in Tasmania face grain surpluses during harvest seasons with limited local storage. There was no real-time visibility into grain movement, no automated communication between farmers, transporters, and storage facilities, and no scalable way to manage logistics.

---

## 🏗️ System Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   FARM SITE     │    │  TRANSPORT HUB   │    │ STORAGE FACILITY│
│  Raspberry Pi   │    │  Raspberry Pi    │    │  Raspberry Pi   │
│  GPS Tracker    │    │  GPS Tracker     │    │  Inventory IoT  │
│  5G Router      │    │  5G Router       │    │  5G Router      │
└────────┬────────┘    └────────┬─────────┘    └────────┬────────┘
         │                     │                        │
         └──────── MQTT (mTLS) ────────────────────────┘
                               │
                     ┌─────────▼──────────┐
                     │   AWS IoT Core      │
                     └─────────┬──────────┘
                               │
              ┌────────────────┼─────────────────┐
              │                │                 │
     ┌────────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐
     │  AWS Lambda   │  │  DynamoDB   │  │     S3      │
     │ (automation)  │  │  (storage)  │  │  (archive)  │
     └───────────────┘  └─────────────┘  └─────────────┘
              │
     ┌────────▼──────────────────────────┐
     │  CloudWatch · GuardDuty · IAM     │
     │  CloudTrail · EKS (containers)    │
     └───────────────────────────────────┘
```

---

## 🛠️ Tech Stack

**Edge Devices**
- `Raspberry Pi` — sensor data collection and MQTT publishing
- `GPS Trackers` — real-time location of grain shipments
- `5G Routers` — site connectivity

**AWS Cloud**
- `AWS IoT Core` — device management and message broker
- `AWS Lambda` — event-driven automation (inventory updates, alerts)
- `DynamoDB` — real-time data storage
- `S3` — long-term data archiving
- `EKS` — containerised service deployment
- `CloudWatch` — monitoring and logging
- `GuardDuty` — threat detection
- `CloudTrail` — audit trail
- `IAM` — identity and access management

**Security**
- `MQTT with mutual TLS (mTLS)` — encrypted device-to-cloud communication
- `OpenVPN on EC2` — site-to-cloud VPN for secure tunnelling

**Simulation & Documentation**
- `Cisco Packet Tracer` — network topology simulation
- `Docker` — containerised deployments

---

## 🔐 Security Architecture

- All MQTT connections require client certificates (mutual TLS) — no anonymous publishing
- OpenVPN tunnels between each site and AWS VPC
- IAM roles with least-privilege policies per service
- GuardDuty continuously monitors for anomalous API calls and network traffic
- CloudTrail logs every AWS API action for audit

---

## ✅ Testing & Results

| Test | Outcome |
|---|---|
| GPS tracking simulation | Validated in Packet Tracer |
| AWS Lambda automation | Triggered correctly on IoT Core messages |
| MQTT mTLS connection | Devices authenticated and published successfully |
| DynamoDB writes | Event data stored with correct schema |
| CloudWatch alerts | Threshold alarms fired as expected |

---

## 📈 Key Outcomes

- Real-time visibility into grain location and inventory status across all 3 sites
- Automated stakeholder notifications via Lambda triggers
- Scalable, secure architecture ready for real-world deployment
- Full security monitoring stack (GuardDuty, CloudTrail, CloudWatch)

---

## 👥 Team

- Figo Figo
- Harnil Makwana
- Deep Patel
- Serge Kapo
- Karunya Votarka

**Module**: Professional Practice — Middlesex University London

---

## 👤 Author Contact

**Figo Figo** — BSc Networking & Security, Middlesex University London  
🌐 [figo.me.uk](https://figo.me.uk) · 💼 [LinkedIn](https://www.linkedin.com/in/figo-figo-1204642b2)
