---
title: Cloud Computing - Everything Else (leftover slide notes)
tags: [cloud-computing, exam, leftovers, nptel]
course: Cloud Computing (NPTEL, IIT Kharagpur, Prof. Soumya K. Ghosh)
exam-format: MCQ
---

# ☁️ Cloud Computing - Everything Else

> [!abstract] What this file is
> This file holds the **slide content that is not already in** [[Cloud_Computing_-_Tier_1_Notes]], [[Cloud_Computing_-_Tier_2_Notes]] or [[Cloud_Computing_-_Tier_3_Notes]]. I compared every Week 1 to 12 section against those three files.
>
> **Read it last.** These are lower-yield topics, but exam questions can still come from them, especially the lists (advantages, disadvantages, challenges) and the case studies.
>
> **Label guide**: 📘 = from the slides. 📌 = not on the slides (from papers or my own working, and I say so).

> [!note] What is deliberately not here
> - Slides that are **only a picture** (screenshots, architecture diagrams) or only **references/URLs**: I mention what the picture shows, but there's no text to copy.
> - Slides that **repeat** earlier ones (Week 7 MCC-II repeats MCC-I, Week 10 Lecture 50 repeats Lecture 49).

**Contents**
- [ ] [[#1. Week 1 - general cloud topics]]
- [ ] [[#2. Week 2 - network virtualization]]
- [ ] [[#3. Week 4 - Meghamala (IIT Kharagpur private cloud)]]
- [ ] [[#4. Week 5 - economics assignments, worked]]
- [ ] [[#5. Week 6 - security basics, SaaS collaboration, broker marketplace]]
- [ ] [[#6. Week 7 - mobile cloud extras, fog extras, geospatial extras]]
- [ ] [[#7. Week 8 - course summary and research areas]]
- [ ] [[#8. Week 10 - Docker demo]]
- [ ] [[#9. Week 12 - CPS, trajectory cloud, Internet of Health Things case study]]
- [ ] [[#10. One-page cheat sheet]]

---

# 1. Week 1 - general cloud topics

## 1.1 Advantages of cloud computing 📘

| Advantage | Meaning |
|---|---|
| **Lower computer costs** | You don't need a high-powered, high-priced PC. Apps run in the cloud, so the PC can have a smaller disk and less memory |
| **Improved performance** | Fewer big programs hogging memory, so PCs boot and run faster |
| **Reduced software costs** | You get most of what you need for free instead of buying expensive software |
| **Instant software updates** | Web apps update automatically. You always get the latest version without paying for an upgrade |
| **Improved document format compatibility** | No more format mismatches between versions |
| **Unlimited storage capacity** | Your 1 TB drive is small next to the hundreds of petabytes in the cloud |
| **Increased data reliability** | A crashed PC doesn't destroy your data, because it is stored and replicated in the cloud |
| **Universal information access** | Documents stay in the cloud, so you access them anywhere with an internet connection |
| **Latest version availability** | The edited version is the one you see wherever you log in |
| **Easier group collaboration** | Several users work on the same documents and projects |
| **Device independence** | You're not tied to one computer or network, and changes follow you |

## 1.2 Disadvantages of cloud computing 📘

| Disadvantage | Meaning |
|---|---|
| **Requires a constant internet connection** | No connection means no access to even your own documents |
| **Can be slow** | Even on a fast link, web apps can be slower than desktop software |
| **Features might be limited** | For example, you can do much more in desktop PowerPoint than in Google Presentation |
| **Stored data might not be secure** | Can unauthorised users get at confidential data? |
| **Stored data can be lost** | It is replicated, but if it goes missing you have no local backup |
| **Poor fit for HPC** | Not clear that compute-intensive **MPI/OpenMP** applications run well. Scheduling matters because you want the VMs **co-located** to minimise latency |
| **General concerns** | Each cloud uses different **protocols and APIs**, so applications may not move between clouds. Standards are missing |

> [!warning] Exam traps
> - "Cloud computing works offline" → false (it needs a constant connection).
> - "Cloud is ideal for MPI-based HPC applications" → false.
> - "Data in the cloud is always lost if a PC crashes" → false (it is the reverse: cloud improves reliability).

## 1.3 Cloud-sourcing and cloud storage 📘

**Cloud-sourcing** = using other people's cloud infrastructure and services.
- **Why it matters**: high-scale, **low-cost providers**; **any time/place access** through a web browser; **rapid scalability** with incremental cost and load sharing; you no longer need to focus on local IT.
- **Concerns**: **performance, reliability and SLAs**; **control of data and service parameters**; application features and choices; **interaction between cloud providers**; **no standard API** (a mix of **SOAP and REST**); and privacy, security and trust.

**Cloud storage** = several big web companies hire out their spare **data storage capacity**. Data stored remotely can be temporarily cached on desktops, phones or other Internet-linked devices. **Amazon EC2 (Elastic Compute Cloud) and S3 (Simple Storage Service)** are the well-known examples.

## 1.4 Virtual workspaces and VM advantages 📘

**Virtual workspace** = an abstraction of an execution environment that can be made **dynamically available to authorised clients** through well-defined protocols. It has a **resource quota** (CPU, memory share) and a **software configuration** (for example the OS). It is implemented on **virtual machines**.

**Advantages of virtual machines** 📘
- Run operating systems where the **physical hardware isn't available**.
- **Easier to create** new machines and **to back up** machines.
- **Software testing** using **clean installs** of operating systems and software.
- **Emulate more machines** than are physically available.
- **Timeshare lightly loaded** systems on one host.
- **Debug problems** (suspend and resume the problem machine).
- **Easy migration**.

> [!tip] Link
> The performance point is in Tier 1: **para-virtualization (e.g. Xen) is very close to raw physical performance**.

## 1.5 Business drivers and economics of the cloud 📘

**The main reason for interest** = public clouds can **cut IT costs** significantly. The end user gets the **illusion of near-infinite capacity**, can **scale rapidly** and **pays only for what is used**. In a private data centre you must provision for **peak capacity**, so **average utilisation is only 5 to 20%**.

**IaaS economics: in-house server vs cloud server** (from *Enterprise Cloud Computing* by Gautam Shroff)
| | In-house server | Cloud server |
|---|---|---|
| Purchase cost | **$9,600** | none |
| Cost per hour (over 3 years) | **$0.36** | **$0.68** (ratio cloud/in-house 1.88) |
| Efficiency | **40%** | **80%** |
| Cost per **effective** hour | $0.90 | $0.85 |
| Power and cooling | $0.36 | 0 |
| Management cost | $0.10 | $0.01 |
| **Total cost per effective hour** | **$1.36** | **$0.86** (ratio in-house/cloud **1.58**) |

> [!tip] In simple words
> The cloud looks 88% more expensive per hour ($0.68 vs $0.36), but because it is **used twice as efficiently** and has **no power or management overhead**, it ends up **cheaper per useful hour**.

**Benefits of the public cloud for the end user** 📘
- High utilisation and high scalability.
- No separate hardware procurement, power cost or IT administration.
- **User-friendly SLA** with high availability (about **99%**) and compensation if the SLA is missed.
- Rent the cloud to **develop and test prototypes** before big investments.
- **Portability standards** are being developed by the **Cloud Computing Interoperability Forum** and the **Open Cloud Consortium**. For example, **Amazon EC2 and Eucalyptus share the same API**.
- **Startups** benefit by renting computing and storage instead of buying it.
- **Small and medium businesses** (**fewer than 250 employees**) also benefit.

**Benefits of the private cloud** 📘
- **One server** with 12 cores and 12 GB RAM costs far less than **12 servers** with 1 core and 1 GB each.
- **Confidentiality of data** is preserved.
- Virtual machines are **cheaper** and **faster to provision** than physical machines.

**PaaS vs IaaS economics** 📘: a web app must be available 24×7 but its transaction volume is **unpredictable**.
- **IaaS**: you must keep a **minimum number of servers running all the time**.
- **PaaS**: deploying costs **nothing up front**. You pay **according to usage**, and the platform **scales automatically**.

**PaaS benefits** 📘: no need to handle **scaling and load balancing** across VMs; a **web-based IDE** for development and deployment; **easier move** from development to production; developers write apps directly on the cloud and **don't buy separate licences** for tools.

**SaaS benefits** 📘: you **subscribe** instead of buying and licensing software. Google Docs is free instead of buying Word. Enterprises use web-based **CRM** instead of buying servers and installing CRM software and databases.

**Purpose of cloud computing in organisations** 📘: IT platform for **multi-organisation business processes**; **backup**; running **CRM, ERP and supply-chain** applications; **productivity and collaboration** tools; **development and testing**; **storing and archiving large files** (video, audio); **analysing customer or operations data**; **research and development analysis**; **meeting spikes in demand**; running **data-intensive batch jobs** (data conversion, risk modelling, graphics rendering); sharing information with the government or regulators; consumer entertainment.

**Top cloud applications driving adoption** 📘: mail and messaging, archiving, backup, storage, security, virtual servers, **CRM**, collaboration across enterprises, **hosted PBX**, **video conferencing**.

## 1.6 Role of networking in the cloud 📘
- In cloud computing, **network resources can be provisioned dynamically**.
- Core networking concepts: **Virtual Local Area Networks (VLANs)**, **Virtual Private Networks (VPNs)** and the **different protocol layers**.
- Tools used to set up topologies and configurations: **OpenSSH** and **OpenVPN**.

## 1.7 Network Function Virtualization (NFV) 📘

**ETSI definition (paraphrased)**: NFV aims to change how network operators build networks by using **standard IT virtualization** to **consolidate many network equipment types onto industry-standard high-volume servers, switches and storage**, located in data centres, network nodes or at the end user's premises. Network functions are implemented **in software** that runs on standard servers and can be **moved or instantiated in different locations as required, without installing new equipment**.

> [!tip] In simple words
> Instead of buying a separate physical firewall box, router box and load-balancer box, you run them as **software on ordinary servers**, and you can start or move them whenever you want.

## 1.8 Client-server architecture 📘
- Consists of one or more **load-balanced servers** servicing requests from clients.
- Clients and servers exchange messages in **request-response** style.
- The client is often a **thin client** (low computing power). The server can be a **load-balanced cluster or a stand-alone machine**.
- The **three-tier** client-server architecture appears on a picture-only slide (it separates the presentation, application logic and data layers). 📌
- The comparison with the cloud model is in Tier 1.

---

# 2. Week 2 - network virtualization

## 2.1 Basics 📘
- **Network virtualization** = making a **physical network appear as multiple logical ones**.
- **Formal definition**: a networking environment that lets **multiple service providers dynamically compose multiple heterogeneous virtual networks** that **co-exist in isolation** from each other, deploy **customised end-to-end services on the fly**, and manage them for end users by **sharing and using network resources leased from multiple infrastructure providers**.

**Related concepts and why they aren't enough** 📘
| Concept | Meaning | Limitation |
|---|---|---|
| **VPN** | A virtual network connecting distributed sites | **Not customisable enough** |
| **Active and programmable networks** | Customised network functions through programmable interfaces and active code | |
| **Overlay networks** | **Application-layer** virtual networks | **Not flexible enough** |

## 2.2 Network virtualization model 📘
The model has four parts: **business model, architecture, design principles, design goals**.

**Business model: four players**
| Player | Role |
|---|---|
| **Infrastructure Providers (InPs)** | Manage the underlying **physical networks** |
| **Service Providers (SPs)** | **Create and manage virtual networks** and deploy customised end-to-end services |
| **End users** | **Buy and use** services from different service providers |
| **Brokers** | **Mediators / arbiters** |

**Design principles** 📘
- **Concurrence** of multiple heterogeneous virtual networks (introduces diversity).
- **Recursion** of virtual networks (opens the door for network-virtualization economics).
- **Inheritance** of architectural attributes (promotes value addition).
- **Revisitation** of virtual nodes (simplifies network operation and management).

**Design goals** 📘
| Goal | Meaning |
|---|---|
| **Flexibility** | Service providers can choose any topology, routing, forwarding and control/data plane without coordinating with others ("the IPv6 fiasco should never happen again") |
| **Manageability** | Clear **separation of policy from mechanism**, defined accountability, modular management |
| **Scalability** | Maximise the number of co-existing virtual networks, raise utilisation, spread CAPEX and OPEX |
| **Security, privacy and isolation** | **Complete isolation** between virtual networks (logical and resource), isolating faults, bugs and misconfigurations |
| **Programmability** | Programmable network elements (e.g. routers) without being vulnerable to threats |
| **Heterogeneity** | Supports different networking technologies (optical, sensor, wireless) |
| **Experimental and deployment facility** | Test beds like **PlanetLab, GENI, VINI** let you deploy services from testing straight to the real world |
| **Legacy support** | Treat the existing Internet as one of the many virtual Internets |

> [!tip] Memory trick
> **F-M-S-S-P-H** (+ test beds + legacy): **F**lexibility, **M**anageability, **S**calability, **S**ecurity/isolation, **P**rogrammability, **H**eterogeneity.

---

# 3. Week 4 - Meghamala (IIT Kharagpur private cloud)

> [!note] Mostly screenshots
> The Week 4 Meghamala slides are almost all pictures. Here is what they show and what you should know.

**Meghamala** = IIT Kharagpur's **private cloud, built on OpenStack**. The lecture covers three things: **VM creation overview, accessing the VM as a user, and VM termination**. 📘

**What the screenshots show** 📘 (matching the OpenStack components in [[Cloud_Computing_-_Tier_1_Notes]], Section 6)
| Screen | Component | What it shows |
|---|---|---|
| Login and dashboard, graphical **resource usage** | **Horizon** | Web dashboard |
| Details of instances | **Nova** | Instance list (internal IP ranges in the 192.x and 10.4.x ranges) |
| Available images | **Glance** | The images you can launch VMs from |
| Network access rules of a **security group** | **Neutron** | Which traffic is allowed |
| vCPU, RAM and storage of **hypervisors** | **Nova** | Compute node capacity |
| Different **flavors** of VMs | **Nova** | VM sizes (vCPU, RAM, disk) |
| Volumes | **Cinder** | Block storage |

- **Accessing a created VM**: through the **X2Go client** (the example VM is named *cloud-nptel*).
- **Termination**: shown only as screenshots of terminating the instance from the dashboard (no extra text on the slides).

---

# 4. Week 5 - economics assignments, worked

> [!warning] Read this note first
> The slides give the **questions only**, and some of the formulas are garbled in the text. The solutions below are **my own working** (📌). Check them against how your teacher solved them.

**Assignment 2** 📘 (question) **+ my working** 📌
- Peak demand P = 100, baseline unit cost B = 120, cloud unit cost C = 200, period T = 100. Is the cloud cheaper?
- The slide's formula is garbled. I read it as **D(t) = 50(1 + e⁻ᵗ)**, because that gives a **peak of 100 at t = 0**, which matches the question.
- **Average demand**: A = (1/100) ∫₀¹⁰⁰ 50(1 + e⁻ᵗ) dt = 50 × (1 + (1 − e⁻¹⁰⁰)/100) ≈ **50.5**.
- **P/A** = 100 ÷ 50.5 ≈ **1.98**. **U = C/B** = 200 ÷ 120 ≈ **1.67**.
- **U < P/A** → **the cloud is cheaper**. (Total costs: owned = P×B×T = 1,200,000; cloud = A×U×B×T ≈ 1,010,000.)

**Assignment 3** 📘 (question) **+ my working** 📌 (in-house 6,00,000 for 12 cores, cloud 8 cores)
| | In-house | Cloud |
|---|---|---|
| Hourly cost | 6,00,000 ÷ (3 × 365 × 24 = 26,280 h) = **22.83** | **42** |
| ÷ efficiency | 22.83 ÷ 0.4 = **57.08** | 42 ÷ 0.8 = **52.50** |
| + power and cooling / management | + 22 + 6 → **85.08** per hour | + 1 → **53.50** per hour |
| **Per core-hour** | 85.08 ÷ 12 ≈ **7.09** | 53.50 ÷ 8 ≈ **6.69** |

→ The **cloud is cheaper per core-hour**, even though it has fewer cores.

**Assignment 1** (the sine-demand penalty problem) is a pure integral problem, and the method is in [[Cloud_Computing_-_Tier_3_Notes]], Section 5.5: R(t) = D(t) + δ·dD/dt, and penalty = area between D and R, times the unit cost (0.9 on the slide).

---

# 5. Week 6 - security basics, SaaS collaboration, broker marketplace

The main security content (attacks, Gartner's 7 risks, co-residence, SoD, broker) is in [[Cloud_Computing_-_Tier_2_Notes]]. This section adds the rest.

## 5.1 Basics of security 📘

**Basic components**: **Confidentiality** (keeping data and resources hidden), **Integrity** (data integrity, plus **origin integrity = authentication**), **Availability** (enabling access to data and resources).

**Classes of threats** 📘
| Class | Covers |
|---|---|
| **Disclosure** | **Snooping** |
| **Deception** | Modification, **spoofing**, repudiation of origin, denial of receipt |
| **Disruption** | Modification |
| **Usurpation** | Modification, spoofing, **delay**, **denial of service** |

**Policies and mechanisms** 📘
- A **policy** says what is and isn't allowed (it defines "security" for the system). **Mechanisms enforce** policies. If composed policies **conflict**, the gaps can create vulnerabilities.
- **Trust and assumptions** underlie all of security: policies must unambiguously partition states into secure and not secure, and mechanisms are *assumed* to enforce the policy.
- A mechanism can be **secure** (reachable states ⊆ secure states), **precise** (reachable = secure states) or **broad** (reachable states include insecure ones).
- **Assurance** goes through specification → design → implementation.
- **Operational issues**: cost-benefit analysis (is it cheaper to prevent or to recover?), **risk analysis** (should we protect it, and how much?), laws and customs.
- **Human issues**: organisational problems (power, responsibility, financial benefits), **people problems** (outsiders and insiders, **social engineering**).

**Security services** 📘: confidentiality (privacy), **authentication** (who created or sent the data), **integrity** (not altered), **non-repudiation** (the order is final), **access control** (prevent misuse of resources), **availability** (permanence, non-erasure).

**Role of a security infrastructure** 📘: confidentiality, integrity, availability, **authentication** (identify legitimate users), **authorisation** (is this operation allowed for this user), **non-repudiation** (trace what happened and prevent denial), and **safety** (protection against tampering, damage and theft).

**Types of attack** 📘: social engineering/**phishing**, physical break-ins and theft, **password attacks**, **buffer overflows**, **command injection**, denial of service, exploiting faulty application logic, snooping, packet manipulation or fabrication, backdoors.

## 5.2 Cloud security II 📘

- **Economic advantages**: consumers get **no upfront commitment** and can scale with demand (smaller start-up costs, lower **CAPEX**). Providers get **higher data-centre utilisation**.
- **Why isn't everyone on the cloud?** Clouds still face the old **confidentiality, integrity, availability and privacy** issues, plus **additional attacks**. An **IDC survey** ranked security among the top cloud barriers.
- **Why the cloud brings new threats**: traditional security means **keeping attackers out**, but the cloud allows **co-tenancy**, so an attacker can **legitimately sit on the same physical machine as the target**. Other new issues: the customer's **lack of control over their own data and applications**, and **reputation fate-sharing**.

**Security stack (who is responsible)** 📘
| Model | What the provider covers | What the customer covers |
|---|---|---|
| **IaaS** | Facilities and hardware (the infrastructure) | The **most** responsibility: OS, middleware, apps, data |
| **PaaS** | Platform and infrastructure security | The application, with the customer-side system administrator managing the rest |
| **SaaS** | A **self-contained operating environment** (content, presentation, apps, management) | **Least** responsibility. **Service levels, security, governance, compliance, liability** are defined by contract |

> [!tip] Memory trick
> Moving from **IaaS → SaaS**, the **provider's** security responsibility **increases** and the **customer's** decreases.

**Application security** 📘: cloud applications are **web-service based**, so the attacks are similar.
- **Injection attacks**: malicious code changes the path of execution.
- **XML Signature Element Wrapping**: the original body of an XML message is **moved to a new "wrapping" element inside the SOAP header**, and a **new (fake) body** is created.
- **Cross-Site Scripting (XSS)**: the attacker injects **client-side script** into pages viewed by others to bypass access controls.
- **Flooding**: the attacker sends a huge number of requests to a service.

**Data life-cycle management** 📘 (the questions a customer should ask)
- **Confidentiality**: will sensitive data stay confidential? Will the provider itself peek?
- **Integrity**: is the provider computing correctly, and storing my data without tampering?
- **Availability**: will critical systems go down in a DoS attack on the provider? What if the provider goes out of business?
- **Data location**: all copies and backups only where the contract, SLA or regulation allows.
- **Archive** and **access latency**.

**Identity management (IDM)** 📘: **authenticates users and services** from credentials and characteristics. **Preventing identity theft** is a major challenge, and the cloud stores a lot of client data that data mining can exploit.

## 5.3 Cloud security III: extra on the co-residence paper 📘
- **New risks**: **trust and dependence** (a new trust relationship between customer and provider) and **multi-tenancy** (VMs of different customers share a physical machine).
- **Attack model**: study how practical **cross-VM attacks** are on a real IaaS (**Amazon EC2**). Two steps: **placement** and **extraction**.
- **Threat-model assumptions**: the **provider and its infrastructure are trusted**; attacks that **subvert administrator functions** or **exploit VMM vulnerabilities** are **not** considered. Adversaries are **non-provider-affiliated** malicious parties and victims are users running confidentiality-requiring services.
- Like any customer, the attacker can run many instances (a **maximum of 20 in parallel** per EC2 account).
- Two kinds of attack: on a **known hosted service**, or on a **particular victim's service**.

## 5.4 Cloud security IV: collaborative SaaS clouds 📘

- **Unique features**: **co-tenancy** and **lack of control over outsourced data and applications**. Customers worry about **inadequate policies and practices** and **insufficient security controls**.
- **Collaboration types** in multi-domain clouds: **tightly coupled (federated)** and **loosely coupled**. Existing security mechanisms were designed mainly for **tightly coupled** systems, so securing **loosely coupled** collaboration is the challenge.
- The SaaS model has the **maximum lack of control** (no active data streams, audit trails or outage reports).
- **Four objectives of the framework**:
  1. **SelCSP**: a framework to select a **trustworthy and competent** collaboration service provider.
  2. Select access requests from **anonymous users** so both **access risk** and **security uncertainty** stay low.
  3. A heuristic for **IDRM** that grants **minimal excess privilege**.
  4. A **distributed** framework that uses **only local information** to **detect and remove access conflicts** dynamically.
- **Trust models**: most published work has **no mathematical formulation or validation** of trust and risk models. The aim is to model the **trust, reputation and competence** of a provider.
- **SLAs for clouds**: most providers guarantee only **availability**, and SLAs have **non-standard clauses** about assurances and compensation. The aim is to define a **standard set of SLA parameters**.
- **Risk-Based Access Control (RAC)**: gives access even when a subject **lacks the proper permissions**, balancing **access risk** against **security uncertainty** from information sharing. It is **more flexible than binary MLS** (multilevel security). The **distributed RAC** uses a **fuzzy inference system**.

## 5.5 Broker for the cloud marketplace: extra detail 📘

(Basic idea in Tier 2, Section 2.6.)
- **Introduction**: rapid growth of cloud services, huge numbers of providers with different QoS, and customers with different requirements.
- **Objectives**: choose the **most suitable provider** for the customer's QoS needs; calculate the **degree of SLA satisfaction** and a provider's **trustworthiness**; and make a decision system for **dynamic service migration** based on the QoS actually experienced.
- **Other approaches**: **CloudCmp** (compares providers' QoS), fuzzy provider selection, satisfaction-measure frameworks, and selection that considers **trust and competence**.
- **Customer QoS parameters** are given for IaaS and SaaS (more can be added). A provider has **promised QoS values** and **trust values**, kept **independent** because they measure different things.
- **Provider selection** uses a **fuzzy inference engine**: **input** = QoS offered by the provider and its **trustworthiness**; **output** = **suitability**; the request goes to the provider with the **maximum suitability**. The membership functions are built from the user's requirements.
- **Monitoring module**: gets performance data from the provider or a third party.
- **Migration decider**: a **fuzzy inference engine** whose output is the **degree of SLA satisfaction**. **If it falls below a threshold, migrate.**
- **Migration module**: selects the **target provider** the same way as provider selection.
- **Case studies** (IaaS and SaaS marketplaces): **10 providers** with different QoS, **500 requests**, **year-long simulation**. A few providers degrade (degradation follows a **Gaussian distribution**). The fuzzy broker is compared with a **conventional minimum-cost "crisp" broker**.
- **Future scope**: allow flexibility in QoS requirements, compare on production workloads, introduce service classes for customers.

---

# 6. Week 7 - mobile cloud extras, fog extras, geospatial extras

## 6.1 Mobile cloud computing extras 📘

(Core MCC material is in Tier 2, Section 5.)

- **Mobile Backend-as-a-Service (MBaaS)**: gives mobile developers a way to connect their app to **backend cloud storage and processing**. It hides the complexity of managing infrastructure, so they focus on **front-end** work. It helps with multiple apps, backends, developers and mobile platforms.
- **Examples of mobiles augmented by the cloud**: **Amazon Silk** (a *split* browser), **Apple Siri** (speech recognition in the cloud), **Apple iCloud** (unlimited storage and sync), image-recognition and **augmented-reality** apps (e.g. **Google Glass**).
- **Why MCC**: **speed and flexibility** (apps built or revised quickly and delivered to many device types), **shared resources** (not limited by the device's storage and processing).
- **Key features**: quick development, delivery and management of mobile apps; uses **fewer device resources**; supports many development approaches and devices.
- **Key requirements**: **simple APIs** to mobile services (no knowledge of the network technology), a **web interface**, and Internet access to remotely stored applications.
- **Dynamic runtime offloading** involves: dynamic **application profiling and a solver** on the mobile device, **runtime partitioning**, **migration of intensive components**, and **continuous synchronisation** during execution.

**MCC architecture (3 steps)** 📘
1. Mobile devices connect to **mobile networks through base stations**, and requests go to **central processors** connected to servers that provide mobile network services.
2. The **subscribers' requests are delivered to the cloud through the Internet**.
3. In the cloud, **cloud controllers** process the requests and provide the corresponding cloud services.

**More advantages** 📘: **extending battery life** (offloading), improving **data storage capacity and processing power**, and improving **reliability and availability** (data and applications stay in the cloud, and security services like **virus scanning and malicious-code detection** can run there). Also dynamic provisioning, scalability, multi-tenancy and easy integration.

**Challenges** 📘
- **Security** has two categories: **security for mobile users** and **securing data on clouds**. Mobile devices face malicious code, and **GPS** can cause privacy problems. Because devices are resource-constrained, **threat detection can move to the cloud**: a **host agent** checks whether a file is in a cache of already-analysed files, and if not, sends it to the **in-cloud network service** for verification.
- **Context-aware mobile cloud services**: use local context (data types, network status, device environment, user preferences) to improve QoS.
- **Network access management** (link performance and bandwidth use).
- **Quality of service**: network delay is the big issue. **CloneCloud** and **cloudlets** are expected to reduce it.
- **Standard interfaces**: interoperability between mobile users and the cloud needs standard protocols and signalling.
- **Service convergence**: services will differ by type, cost and so on.

**Applications of MCC** 📘: **mobile healthcare** (health monitoring, intelligent emergency management), **mobile gaming** (offload the game engine and graphic rendering), **mobile commerce**, and **mobile learning (m-learning)**, where the cloud solves the cost, low data rate and limited educational resources of traditional m-learning. Accessibility examples: a **pedestrian-crossing guide** and a **currency reader** for blind and visually impaired people.

**MuSIC** 📘: **Mobility-aware optimal Service allocation In Mobile Cloud computing**. User **mobility** complicates splitting tasks between the mobile client and a **tiered cloud**, while balancing **application delay, device power use and user cost**.

**Case study: context-aware dynamic parking service** 📘
- MCC integrated with **vehicular networks** gives scalable, data-driven **context-aware vehicular cyber-physical systems**.
- **Traditional parking garages**: a **wireless sensor network (WSN)** detects each space and forwards the information to the **traffic cloud**, which processes it and sends it to users.
- **Dynamic parking**: temporarily parking along the road when it **doesn't impede traffic**, using the regular pattern of road capacity (e.g. heavy traffic in the morning and evening).
- Three aspects: **service planning by traffic authorities** (using historical traffic flow, road and weather conditions), the **reservation process** (status of each space is monitored and updated in the traffic cloud, and drivers see it on their phones), and **context-aware optimisation** (including the **expected parking duration**, which depends on the purpose of the visit).

## 6.2 Fog computing extras 📘

(Core fog material is in Tier 1, Section 5.)
- **Use cases**: **emergency evacuation systems** (real-time information on affected areas and exit routes), **natural disaster management** (real-time landslide and flash-flood notifications), and large sensor deployments whose data is **pre-processed and summarised** before going to the cloud to reduce congestion.
- **Applicability**: smart traffic lights, **connected vehicles**, smart grid, IoT.
- **Connected vehicle (CV)**: connectivity between cars, cars and access points (**Wi-Fi, 3G, LTE, roadside units, smart traffic lights**), and access points to each other. Fog suits CV services like **infotainment, safety, traffic support and analytics**.
- **Fog challenges**: **resource allocation** among applications while guaranteeing **end-to-end latency**, raising system **throughput** with high availability and scalability, and **security** of applications, services and data.
- **Resource management goals**: use **idle fog nodes**, more parallel operations, **load balancing**, meeting **delay requirements** of real-time apps, **crash fault tolerance**, scalability.
- **Resource management challenges**: **data may not be at the executing node** (so it must be fetched), the executing node may **become unresponsive under load**, and choosing a **new node for micro-service migration** to reduce response time.
- **Approaches**: **execution migration to the nearest node**, minimising the **carbon footprint** of video streaming, resource **prediction, estimation and reservation**, **Docker as an edge platform** (fast deployment), and cost-efficient VM placement for fog-based medical cyber-physical systems.
- **Security issues**: **authentication** at the different gateway levels and at the fog nodes, **man-in-the-middle** attacks, and **privacy**. In a **smart grid**, a malicious user can tamper with their own smart meter, **report false readings** or **spoof IP addresses**.

## 6.3 Geospatial cloud extras 📘

(Core geospatial material is in Tier 3, Section 3.)
- **Information is linked to a location**, with many users and domains (legal/cadastral, political and others).
- **GIS users are shifting** from single users to societal, multi-user (enterprise) and group/team use.
- **Experimental geospatial cloud at IIT Kharagpur**, with two case studies on **service integration for queries**: (1) merging **highway and local road networks** into a merged road network and finding the shortest path; (2) merging **canal and river** data into a merged water network and doing a **buffer** on it.
- **Challenges in geospatial cloud**: implementing and **scaling spatial databases**, **multi-tenancy**, **policy management among tenants**, **geographically situated backups**, **security of data**.
- **Interoperability at three levels**: **data level** (ability to consume the information), **service level** (ability to exchange or obtain it), and **security level** (doing both in a reliable and trusted way).
- **Major security concerns**: **multi-tenancy** and **lack of complete control** over data, applications and services.
- **Questions before moving to the cloud**: which assets (data, applications, functions, processes)? What is their **value** to the organisation? **How could they be compromised** (made public, accessed by a provider employee, etc.)?

---

# 7. Week 8 - course summary and research areas

> [!note] Why this matters
> These are the **course's own summary slides**. They show how your teacher groups the syllabus, so they are a good "what is in scope" checklist.

**Course summary** 📘
- Introduction to cloud computing and the **NIST model**
- Properties, characteristics and disadvantages
- Cloud computing **architecture** and stack; service models (**XaaS**); deployment models
- Service management; **SLAs**; **cloud economics**; **resource management**
- **Data management**: data, scalability and cloud services; databases and data stores; **GFS, HDFS and the MapReduce paradigm**
- **Cloud security**: identity and access management, access control, **trust, reputation and risk**, authentication
- Case study on **open-source and commercial clouds**
- **Research trends**: **fog computing, sensor cloud, container technology, green cloud**

**Research areas** 📘
| Area | Topics |
|---|---|
| **Cloud infrastructure and services** | Architectures, storage and data architectures, distributed and cloud networking, infrastructure technologies, IaaS/PaaS/SaaS, **Storage-as-a-Service, Network-as-a-Service, Information-as-a-Service** |
| **Cloud management, operations and monitoring** | Cloud composition and service orchestration, **federation, bridging and bursting**, **migration**, hybrid cloud integration, **green and energy management**, configuration and capacity management, workload profiling and deployment control, **metering, monitoring, auditing**, service management |
| **Cloud security** | Data privacy, access control, identity management, **side-channel attacks**, **Security-as-a-Service** |
| **Performance, scalability, reliability** | Performance of cloud systems and applications, **availability and reliability**, **micro-services-based architecture** |
| **Systems software and hardware** | **Virtualization technology**, service composition, cloud provisioning orchestration, **hardware architecture support** for the cloud |
| **Data analytics in the cloud** | Analytics applications, scientific computing and data management, **big data** management and analytics, storage/data/analytics clouds |
| **Cloud service management** | Service **discovery and recommendation**, **composition**, **QoS management**, security and privacy, **semantic services**, service-oriented software engineering |
| **Cloud and other technologies** | **Fog computing, IoT cloud, container technology** |

---

# 8. Week 10 - Docker demo

(Docker theory is in Tier 1, Section 4. The demo lectures 49 and 50 repeat the same theory slides, plus this demo.) 📘

**Demo objective: MySQL and phpMyAdmin on the Docker platform**
- **MySQL** = a widely used, open-source relational database.
- **phpMyAdmin** = a **web-based graphical interface** for managing MySQL databases.

**Without containers (standalone system)**: you must **separately install** MySQL, a web server (**Apache**), **PHP** and phpMyAdmin. To move to another machine you again install everything, **back up** the old MySQL data and **restore** it on the new server.

**With containers**: the whole stack is packaged as images and run as containers, so setup is quick and repeatable and **moving to another machine doesn't need re-installation**.

**Container benefits shown** 📘: **separation of responsibility** (developers focus on application logic and dependencies, while IT operations focus on deployment and management) and portability. The three deployment eras (**traditional, virtualized, container**) are covered in Tier 1.

---

# 9. Week 12 - CPS, trajectory cloud, Internet of Health Things case study

## 9.1 More on CPS 📘

(Definition and CPCC are in Tier 2, Section 1.3.)
- CPS describes a broad range of **complex, multi-disciplinary, physically aware** next-generation engineered systems that **integrate embedded computing into the physical world**. Physical and software components are **deeply intertwined**.
- **CPCC benefits**: **efficient use of resources**, **modular composition**, **rapid development and scalability**, **smart adaptation** to the environment at every scale, and a **reliable and resilient** architecture.
- Examples shown: a **cloud-based CPS architecture for intelligent monitoring of machining processes**, and a **cloud-edge computing framework for cyber-physical-social services**.

## 9.2 Traj-Cloud (trajectory cloud) 📘

- **Why**: mobility-trace analysis maps **urban dynamics**, supports **location-based services** and **transport resource planning**. It is a key part of **intelligent transportation systems (ITS)**.
- **Aim**: an end-to-end cloud framework that **reduces the waiting and provisioning time** of location-based services like **food delivery** or **medical emergencies**.

| Service | Input | Output | GCP component |
|---|---|---|---|
| **TS1: Trajectory data indexing** | GPS trajectory trace + semantic information (geotagged locations, road network) | **Spatio-temporal indices** and storage | **BigQuery** and **Cloud SQL** |
| **TS2: Trajectory map-matching** | GPS trace + road network | **Projection of the trace onto the road network**, using a **MapReduce-based** platform in near real time | **Compute Engine** |
| **TS3: Trajectory query** | GPS trace log + a point or range query | A trajectory (point or line shape) | **Compute Engine** and **Cloud SQL** |

## 9.3 Internet of Health Things (IoHT): cloud-fog-edge case study 📘

**Idea**: **fog brings the cloud closer to the data-producing sensors.** Routers, servers and switches act as fog nodes when their processing power is used. The model targets **real-time health applications**.

**Why the hierarchy** 📘
- **Cloud limitations**: high latency, huge data volume, bandwidth need.
- **IoT device limitations**: limited processing, storage and power.
- **Fog-edge benefits**: reduced latency (real-time apps), **less network congestion**, **lower cloud execution cost**.

**Objectives** 📘: design a fog-edge health model to cut **latency, network usage and cloud cost**; test it with the **iFogSim** simulator; build a **customised wearable device** to collect health parameters; and implement the model on hardware.

**Hierarchy and devices** 📘
- The topology slide labels the levels **Cloud (Level 0), Fog (Level 1), Edge (Level 2), IoT (Level 3)**.
- The device-configuration table lists **Cloud (level 0), ISP (level 1), Area Gateway (level 2), Mobile (level 3)** and the sensor below it, with each device's MIPS, RAM, bandwidth, cost per MIPS, and busy/idle power.

**Application placement** 📘
| Module | Fog-based model | Cloud-based model |
|---|---|---|
| Client module | Mobile (edge) | Mobile (edge) |
| Data filtering | **Area gateway (fog)** | Cloud |
| Data processing | **Area gateway (fog)** | Cloud |
| Event handler | **Area gateway (fog)** | Cloud |
| Confirmatory module | **Cloud** | Cloud |

**Simulation configurations** 📘 (area gateways : total users): 1:4, 2:8, 4:16, 8:32, 16:64.

**Results (fog vs cloud)** 📘
| Metric | Result |
|---|---|
| **Latency of the control loop** | **Fog: fixed and low**, because the loop's modules sit at the area gateway. Cloud: higher, because modules sit in the cloud data centre |
| **Network usage** | **Fog: very low**, since the cloud's confirmatory module is reached only for a few positive cases. Cloud: much higher |
| **Cost of execution** | **Fog: lower**, because only the resources on the cloud incur cost, while the rest are owned by the organisation |
| **Energy** | Energy at the **mobile devices stays the same**. The difference shows up in the cloud's energy use |

**Hardware implementation** 📘: a **customised body sensor** (blood-pressure and pulse meter on a **NodeMCU ESP8266** board with an **ADXL345 accelerometer**), **simulated sensor data**, **Raspberry Pi 3 as the fog device** (64-bit, 1 GB RAM, Wi-Fi) and **AWS as the cloud**.

**Activity detection from accelerometer data** 📘
1. **Data extraction**: three components (x, y, z). Magnitude **A = √(x² + y² + z²)**.
2. **5-point smoothing** to reduce noise (each value averaged with two before and two after).
3. **Feature extraction**: maximum amplitude, minimum amplitude, mean amplitude, standard deviation, **energy in the time domain** and **energy in the frequency domain**.
4. **K-Nearest-Neighbour (KNN) classifier** to decide the activity.

**Cardiac attack prediction** 📘: alarm values are **BPM ≥ 170, diastolic ≥ 120, systolic ≥ 180**. The BPM, systolic and diastolic readings are scaled by a factor from the **KNN activity result** (f = KNN value + 1), and **HeartAttackAlarm = true only if all three scaled readings reach their alarm values**; otherwise false.

**Dew-based extension** 📘: **dew computing** = an on-premises software-hardware paradigm in which the on-premises computer provides functionality **independent of cloud services** and also **collaborates** with them. Workflow: the sensor collects data → fog processing → if the cloud connection is available, cloud data processing; if not, check whether **dew** has connectivity (**synchronise with the cloud**) or do **dew-based processing**, and display the result.

**Comparison: cloud vs cloud-fog-edge vs with dew** 📘 (from the health service provider's perspective)
| Feature | Cloud | Cloud-Fog-Edge | With Dew |
|---|---|---|---|
| **On-premise resource utilisation** | Low | Sub-optimal | **Optimal** |
| **Connectivity required** | **Internet** | Local | Local |
| **Uptime** | Low | High | High |
| **Bandwidth required** | **High** | Low | Low |
| **Latency** | **High** | Low | Low |
| **Infrastructure requirement** | Low | Moderate | Moderate |
| **Processing power** | **High** | Limited | Limited |
| **Data storage** | **High** | Low | **Moderate** |

> [!warning] Exam traps
> - Fog's network usage is **low** because only a few cases reach the cloud. Cloud-only needs **high bandwidth and has high latency**.
> - Dew gives **optimal** use of on-premise resources and works with **local** connectivity.
> - Only the **cloud's** resources incur cost in the fog-based model.

---

# 10. One-page cheat sheet

**Week 1**
- **Advantages**: lower hardware/software cost, instant updates, unlimited storage, data reliability, universal access, collaboration, device independence.
- **Disadvantages**: needs internet, can be slow, limited features, security and data-loss worries, poor for **HPC (MPI/OpenMP)**, no standard APIs.
- **Cloud-sourcing**: concerns = SLAs, data control, no standard API (SOAP + REST). **Storage examples**: EC2 and S3.
- **IaaS economics**: in-house **$1.36** vs cloud **$0.86** per effective hour (40% vs 80% efficiency). Private data centres use only **5 to 20%** of capacity.
- **Networking**: VLAN, VPN, OpenSSH, OpenVPN. **NFV** = network functions as **software on standard servers**.

**Network virtualization**
- Players: **InPs, SPs, end users, brokers**. Principles: **concurrence, recursion, inheritance, revisitation**.
- Goals: **flexibility, manageability, scalability, security/isolation, programmability, heterogeneity**, test beds (PlanetLab, GENI, VINI), legacy support.

**Meghamala** = IIT Kharagpur private cloud on **OpenStack**. VM creation → access via **X2Go** → termination.

**Economics assignments**: **cloud cheaper when U < P/A** (Assignment 2: 1.67 < 1.98, cloud cheaper). Assignment 3: **7.09 (in-house) vs 6.69 (cloud)** per core-hour. 📌

**Security extras**
- **Classes of threats**: Disclosure, Deception, Disruption, Usurpation.
- **Security stack**: IaaS → SaaS, the **provider's** share rises.
- **App attacks**: **injection, XML signature wrapping, XSS, flooding**.
- Threat model of the co-residence paper: provider is **trusted**, **max 20 instances**.
- **SaaS collaboration**: loosely coupled is the hard case. **SelCSP**, **RAC (fuzzy)**, **IDRM**, conflict detection and removal.
- **Broker**: fuzzy provider selection (QoS + trust → suitability). **Migration decider**: migrate if **SLA satisfaction < threshold**. Case study: 10 providers, 500 requests.

**Mobile cloud extras**
- **MBaaS**, Amazon Silk, Siri, iCloud, Google Glass. Architecture: **base stations → central processors → Internet → cloud controllers**.
- Challenges: security (users, data), **context-aware services**, **network access**, **QoS** (CloneCloud, cloudlets), **standard interfaces**, **service convergence**.
- Apps: health, gaming, commerce, learning. **MuSIC** = mobility-aware service allocation.

**Fog extras**: use cases = evacuation, disaster management, connected vehicles, smart traffic lights, smart grid. **Security**: authentication, **MITM**, smart-meter spoofing.

**Geospatial extras**: interoperability at **data, service and security** levels. Challenges: spatial DB scaling, multi-tenancy, backups. Concerns: multi-tenancy and loss of control.

**Course summary**: syllabus groups = NIST, architecture, SLA, economics, resource mgmt, data mgmt (GFS/HDFS/MapReduce), security (IAM, trust), research trends (fog, sensor cloud, containers, green cloud).

**Docker demo**: **MySQL + phpMyAdmin**. Standalone needs separate installs of MySQL, Apache, PHP and phpMyAdmin, plus backup/restore to move. Containers avoid that.

**Week 12 case studies**
- **Traj-Cloud**: **TS1 indexing** (BigQuery + Cloud SQL), **TS2 map-matching** (Compute Engine, MapReduce-based), **TS3 query** (Compute Engine + Cloud SQL).
- **IoHT**: simulated in **iFogSim**, **Raspberry Pi 3** = fog, **AWS** = cloud, **KNN** for activity detection. Fog gives **fixed low latency, low network usage, lower cost**.
- **Dew** column: **optimal** on-premise use, **local** connectivity, **moderate** storage.
