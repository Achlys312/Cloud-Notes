---
title: Cloud Computing - Tier 1 Notes
tags: [cloud-computing, exam, tier-1, nptel]
course: Cloud Computing (NPTEL, IIT Kharagpur, Prof. Soumya K. Ghosh)
exam-format: MCQ
---

# ☁️ Cloud Computing - Tier 1 Notes

> [!abstract] How to use this file
> Each topic has the same layout:
> 1. **Slide notes**: what the PPT actually says (short).
> 2. **In simple words**: an easy explanation or analogy.
> 3. **Exam traps**: wrong statements that appear in old papers (these are the "one wrong word makes it false" questions).
>
> **Label guide**
> - 📘 = taken from the Week slides.
> - 📌 = **not on the slides**, but the previous papers/mocks/assignments ask it. Learn it as a one-line fact.
>
> Tick the boxes as you finish each topic.

**Topics (in order of marks)**
- [ ] [[#1. Service models, deployment models and NIST]]
- [ ] [[#2. Virtualization and hypervisors]]
- [ ] [[#3. SLA, SLO, KPI and availability calculations]]
- [ ] [[#4. Docker, containers and Kubernetes]]
- [ ] [[#5. Fog, edge and dew computing]]
- [ ] [[#6. OpenStack]]
- [ ] [[#7. Azure and GCP]]

> [!note] Why 7 topics, not 6?
> Your Tier 1 list had 6. I added **OpenStack** because it is asked about as often as fog/edge and it is cheap to learn (Section 6). Everything else follows your list.

---

# 1. Service models, deployment models and NIST

## 1.1 What is cloud computing? (NIST definition) 📘

NIST (US National Institute of Standards and Technology) says cloud computing is a **model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources** (networks, servers, storage, applications, services) that can be **rapidly provisioned and released with minimal management effort**.

> [!tip] In simple words
> Instead of buying and running your own computers, you **rent** computing power over the internet, use as much as you need, and give it back when you are done. Like electricity: you do not own a power plant, you just plug in and pay for what you use.

## 1.2 The 5 NIST essential characteristics 📘

| # | Characteristic | Meaning | Easy way to remember |
|---|---|---|---|
| 1 | **On-demand self-service** | You can get server time or storage automatically, **no human** from the provider needed | You click, you get it |
| 2 | **Broad network access** | Available over the network from phones, tablets, laptops | Works from any device |
| 3 | **Resource pooling** | Provider's resources are shared by many customers (**multi-tenant**), assigned and reassigned by demand | One big shared pool |
| 4 | **Rapid elasticity** | Scale out and in quickly, sometimes automatically; looks unlimited to the user | Stretches like elastic |
| 5 | **Measured service** | Usage is metered, monitored and reported (pay for what you use) | Like an electricity meter |

> [!tip] Memory trick
> **O-B-R-R-M**: **O**n-demand, **B**road access, **R**esource pooling, **R**apid elasticity, **M**easured service.

> [!warning] Exam traps ("which is NOT a characteristic")
> - "Guaranteed zero downtime" is **not** a NIST characteristic.
> - These are *common* characteristics, **not** the 5 essential ones: massive scale, resilient computing, homogeneity, geographic distribution, virtualization, service orientation, low-cost software, advanced security.
> - Cloud vs traditional client-server: the core differentiator is **virtualization** (client-server has no virtualization concept).

## 1.3 Service models: SaaS, PaaS, IaaS 📘

| Model | You get | Examples | Who is it for |
|---|---|---|---|
| **SaaS** (Software) | Ready-made application used through a browser | Google Docs/Sheets, Gmail, Salesforce CRM, Microsoft Word Online | End users |
| **PaaS** (Platform) | Platform to build, test and deploy your own app; no server worries | Google App Engine, Azure App Service (Web Apps), Cloud Foundry | Developers |
| **IaaS** (Infrastructure) | Raw virtual machines, storage, network | Amazon EC2, Flexiscale, Rackspace, Compute Engine | System admins / IT |

**Who manages what (the key diagram)**

| Layer | IaaS | PaaS | SaaS |
|---|---|---|---|
| Applications | You | You | Provider |
| Data | You | You | Provider |
| Runtime | You | Provider | Provider |
| Middleware | You | Provider | Provider |
| Operating system | You | Provider | Provider |
| Virtualization | Provider | Provider | Provider |
| Servers | Provider | Provider | Provider |
| Storage | Provider | Provider | Provider |
| Network | Provider | Provider | Provider |

> [!tip] In simple words (pizza analogy)
> - **IaaS** = you get the kitchen. You buy ingredients, cook, and clean.
> - **PaaS** = you get a kitchen with ingredients ready. You just cook your recipe (your code).
> - **SaaS** = you order a cooked pizza. You just eat.
>
> Also from the slides: roads = infrastructure, cars/trucks = platform, goods and people = software.

**Simple one-line answers to scenario MCQs**
- You install and patch your own OS and web server on rented VMs → **IaaS**.
- You only write code and upload it; the provider handles servers and scaling → **PaaS**.
- You just log in and use the application → **SaaS**.

**When each model fits** 📘
- **SaaS** is good for: email, short-term needs, apps needing web/mobile access, software with demand spikes (tax/billing). **Not** good for: very fast real-time processing, or when law forbids hosting data externally.
- **PaaS** is good when many developers work together; the platform scales automatically and you do not manage servers.
- **IaaS** is good for: very volatile demand, startups with no capital for hardware, trial/temporary needs. **Not** good if regulations make outsourcing data hard, or you need the very highest performance on dedicated hardware.

> [!warning] Exam traps
> - "Which product belongs where": **Google Docs = SaaS, App Engine = PaaS, EC2 = IaaS**.
> - Azure covers both IaaS and PaaS.
> - SaaS: the consumer does **not** manage network, servers, OS or storage (only limited user settings).

## 1.4 XaaS 📘

**XaaS = "Anything as a Service" / "Everything as a Service".** Any IT capability delivered over the network. It comes from combining **Service-Oriented Infrastructure (SOI) + cloud computing**. XaaS is called "the essence of cloud computing".

Other examples: Business Process (BPaaS), Storage, Security (SECaaS), Database (DaaS), Monitoring/Management (MaaS), Communication/Content/Computing (CaaS), Identity (IDaaS), Backup (BaaS), Desktop (DaaS).

> [!tip] In simple words
> SaaS, PaaS and IaaS are just three famous members. XaaS is the **family name** for all of them, including ones you can invent ("Security as a Service").

> [!warning] Trap
> **FaaS** (Functions as a Service) is only **one** specific model, not the umbrella term. The umbrella is **XaaS**.

## 1.5 Deployment models 📘

| Model | Definition | Example |
|---|---|---|
| **Private** | Cloud operated **solely for one organization** (on-site or hosted by a third party) | Windows Server Hyper-V |
| **Community** | Shared by **several organizations** with shared concerns (mission, security, policy, compliance) | Google Apps for Government, Microsoft Government Community Cloud |
| **Public** | Open to the **general public**; owned by a provider | Google Docs, Spreadsheets |
| **Hybrid** | **Two or more** clouds (private/community/public) bound together by technology that allows data and application portability | Cloud bursting (spill extra load to public cloud) |

> [!tip] In simple words
> - Private = your own house.
> - Community = a shared flat for people with the same needs.
> - Public = a hotel anyone can book.
> - Hybrid = live in your house, rent a hotel room when guests come (**cloud bursting**).

## 1.6 Risks of each deployment type, especially outsourced private cloud 📘

**Outsourced private cloud** = a private cloud whose server side is run by a hosting company.
- It has **two security perimeters** (yours and the provider's), joined by a **protected communication link**. Security depends on the strength of **both perimeters and the link**.
- **Network dependency**: everything depends on the link between you and the provider.
- **Workload locations are hidden** from clients (provider can move workloads).
- **Multi-tenancy risk**: different clients' workloads share the same systems, separated **only by access policies in software**. A software or policy flaw can expose one client to another.
- **Data import/export is limited by network capacity**; real-time or critical work may suffer.
- **Up-front cost: modest to significant** (negotiating the SLA, upgrading network, switching/porting applications, training).
- Good: **potentially strong security** and **extensive resources available** (you can rent in any quantity).

**On-site private cloud**: significant-to-high up-front cost, **limited fixed resources**, you still need IT skills.

**Public cloud**: low up-front cost, elasticity (illusion of unlimited resources), but: workloads can be moved anywhere, **co-residence with competitors or attackers**, depends on the public Internet (DNS, routers), limited visibility and control, you cannot verify full data deletion, **restrictive default SLAs**.

**Community cloud**: access policy can be complex (use RBAC/attribute-based access control); depends on every member's perimeter and the links.

**Hybrid cloud**: can be extremely complex; the mix can change over time as clouds join and leave.

> [!tip] In simple words
> The "outsourced private cloud" risk story: *you gave your data to someone else's building, so you now depend on the road to it (network), on how well both buildings are guarded, and on strangers' data sharing the same server.*

## 1.7 Cloud vs client-server 📘

| Client-server | Cloud |
|---|---|
| Simple: server serves client requests | Complex models (IaaS, PaaS, SaaS) |
| May or may not be load balanced | Load balanced |
| Scalable only to some extent | Theoretically infinitely scalable |
| No concept of virtualization | **Virtualization is the core concept** |

---

# 2. Virtualization and hypervisors

## 2.1 Basic idea 📘

**Virtualization** lets one physical computer do the job of many by sharing its hardware across multiple isolated environments (virtual machines).

- **Virtual Machine (VM)** = a software "computer" that behaves like real hardware.
- **Hypervisor / Virtual Machine Monitor (VMM)** = the software layer that **creates, runs and manages VMs** and allocates physical resources to them. It sits between hardware and the VMs.
- **Host OS** = the operating system on the physical machine (only present when the hypervisor runs on top of an OS).
- **Guest OS** = the operating system that runs **inside** a VM.

> [!tip] In simple words
> Think of a big apartment building (the physical server). The **hypervisor is the building manager** who divides it into apartments (VMs) and makes sure tenants do not disturb each other. Each tenant (guest OS) lives in their own apartment as if it were a whole house.

**Virtualization vs dual boot** 📘
- Dual boot: you choose **one** OS at start-up; the other is off.
- Virtualization: **both OSes run at the same time**, completely isolated from each other.

**Who controls what in IaaS** 📘
- Provider: physical hardware + the **hypervisor layer**.
- Subscriber: **guest OS, middleware and applications**.

**Popek and Goldberg** (1974) say a virtual machine architecture should have three properties 📘: **Equivalence** (behaves like the real hardware), **Resource control** (VMM controls virtualized resources), **Efficiency** (most instructions run directly on the CPU). This works if **sensitive instructions are a subset of privileged instructions**.

**Advantages of VMs** 📘: run OSes the hardware cannot run, easy to create/back up/migrate, safe testing with clean installs, timeshare lightly loaded systems on one host, run legacy systems.

## 2.2 Type 1 vs Type 2 hypervisor 📌

| | **Type 1 (bare-metal)** | **Type 2 (hosted)** |
|---|---|---|
| Runs | **Directly on hardware**, no host OS | **As an application on top of a host OS** |
| Speed | Lower overhead, faster | More overhead (extra OS layer) |
| Examples | **VMware ESXi**, Xen, Microsoft Hyper-V | **VirtualBox**, VMware Workstation |
| Used in | Data centres and cloud | Laptops, testing |

> [!tip] In simple words
> Type 1 = the manager *is* the building (talks to hardware directly). Type 2 = the manager works *inside* another tenant's flat (needs the host OS first).

> [!warning] Exam traps
> - **ESXi = Type 1. VirtualBox = Type 2.**
> - **Docker and LXC are containers, not hypervisors.**
> - A Type 2 hypervisor **can** run many VMs (the option "cannot run more than one VM" is false).
> - "Type 2 always has lower overhead than Type 1" is false.

## 2.3 Full vs para vs hardware-assisted virtualization 📘

| | **Full virtualization** | **Para-virtualization** | **Hardware-assisted** |
|---|---|---|---|
| Generation | 1st | 2nd | 3rd |
| Guest OS modified? | **No** | **Yes** (aware it is virtual) | **No** |
| How privileged instructions are handled | VMM **traps and translates** them (binary translation) | Guest uses a **special API (hypercalls)** to talk to the VMM | CPU extensions (**Intel VT / AMD-V**) trap them |
| Hardware | **All hardware emulated** (even CPU) | VMM handles requests | Guest runs at ring 0, VMM sits in a more privileged "ring -1" |
| Speed | Slow (emulation cost) | **Close to raw hardware** (Xen) | Fast, but unmodified OS cannot use virtualization features |
| Examples | VMware, Microsoft, QEMU, Bochs | **Xen** | VMware and Xen on VT/AMD-V hardware |
| Plus point | Total portability (VM can move between dissimilar hardware) | No translation needed | Runs legacy/unmodified OSes |

> [!tip] In simple words
> - **Full**: the guest has **no idea** it is virtual, and the hypervisor fakes *everything* (slow but works with any OS).
> - **Para**: the guest **knows** it is virtual and politely asks the hypervisor for privileged work using **hypercalls** (fast, but the OS must be changed).
> - **Hardware-assisted**: the **CPU itself helps** the hypervisor, so unmodified OSes run fast.

> [!tip] Memory trick
> Para = **P**olite guest, modifies OS, **P**erformance near native, uses **hypercalls**.

> [!warning] Exam traps
> - Para-virtualization = **modified guest OS + hypercalls**.
> - Full virtualization = **unmodified** guest OS.
> - Hardware-assisted lets you run **unmodified** OSes.
> - "Virtualization prevents resource overcommitment" is false (overcommit is a normal feature).
> - "Virtualization is only possible in cloud environments" is false (it came before the cloud).
> - "Every VM shares the host OS kernel" is false for VMs (that describes **containers**).

## 2.4 How an IaaS cloud is organised 📘

Three levels: **Cloud Manager** (top: sign-up, authentication, top-level resource management) → **Cluster Manager** (manages a cluster of computers) → **Computer Manager** (on each machine; uses the hypervisor's commands to start, stop, suspend and reconfigure VMs).

---

# 3. SLA, SLO, KPI and availability calculations

## 3.1 Definitions 📘

| Term | Meaning | Example |
|---|---|---|
| **SLA** (Service Level Agreement) | A **formal contract** between service provider and consumer; basis of trust and of choosing a provider | The whole contract |
| **SLO** (Service Level Objective) | A **specific, measurable target** promised inside the SLA | "Availability ≥ 99.95%" |
| **KPI** (Key Performance Indicator) | A **raw, low-level measurement** of what actually happens | Downtime, uptime, bytes in/out, actual availability 99.7% |

> [!tip] In simple words (exam analogy)
> - **SLA** = the exam rules paper you both signed.
> - **SLO** = the target: "score at least 90%".
> - **KPI** = your actual marks.
>
> Compare **KPI with SLO** to see if the SLA was kept or violated.

**Hierarchy**: KPIs (base, raw metrics) → combined into SLOs → collected into the SLA.

> [!warning] Exam traps
> - KPI is the **base** layer (raw metrics like downtime), SLO is above it, SLA on top.
> - "Service request time is a KPI for response time" is **true**.
> - SLAs specify measurable commitments (uptime, MTTR, credits). They do **not** specify encryption algorithm details or developer salaries.

## 3.2 What an SLA contains 📘
List of services, specific definition of each, responsibilities of provider and consumer, **metrics**, an **auditing** mechanism, **remedies** if terms are broken, how the SLA changes over time.

**Types**: **Off-the-shelf (non-negotiable / direct) SLA**, where the provider writes the template (today's big clouds), or **negotiable SLA** (via one or more external agents).

**Metrics list** 📘: throughput, availability, reliability, load balancing, durability, elasticity, linearity, agility, automation, customer service response time, service-level violation rate, transaction time, resolution time.

**Cloud SLA vs web-service SLA** 📘: cloud SLAs care about security, privacy, trust and need **automation**; resources are allocated globally with no central directory (web services used UDDI).

**Limitations of today's SLAs** 📘: only measure uptime %, biased towards vendors, little active monitoring for customers, no formal way to verify compliance. A **neutral third party** should monitor.

## 3.3 Multilevel SLA 📌

A multilevel SLA has **three levels**:
1. **Corporate level**: provider-wide obligations that apply to everyone.
2. **Customer level**: terms for one customer across all their services.
3. **Service level**: terms for one specific service.

> [!tip] In simple words
> Like rules at three levels: company rules, your own contract, and the rules for one particular product you bought. For the **specific service**, the **service-level SLA** is the most specific commitment and the one that applies.

## 3.4 Availability and downtime formulas 📘

```
Total expected time = hours per day × number of days
Availability (%)    = (Total time − Downtime) ÷ Total time × 100
Allowed downtime    = (1 − guaranteed availability) × Total time
Uptime              = Total time − Downtime
```

> [!tip] In simple words
> Count only the hours the app is **supposed to run** (e.g. 12 hours/day, not 24). Availability is just "what fraction of that time was it up?".

> [!warning] The classic trap
> If the app runs **12 hours/day for 30 days**, total time is **360 hours**, not 720.

### Worked problem 1 (slide)
99% guarantee, runs 12 h/day, 30 days, outage 10.75 h. Violated?
- Total = 12 × 30 = **360 h**
- Uptime = 360 − 10.75 = 349.25 h
- Availability = 349.25 ÷ 360 = **97.01%**
- 97.01% < 99% → **SLA violated.**

### Worked problem 2 (slide, credits)
Guarantee 99.95%, 30 days, 12 h/day, cost **$50/day**. Credits: availability **< 99.95% → 10%**, **< 99% → 25%**. Outages: 5 h, 30 min, 1 h 30 min, 15 min, 2 h 25 min.
- Outage total = 5 + 0.5 + 1.5 + 0.25 + 2.4167 = **9.667 h**
- Availability = (360 − 9.667) ÷ 360 = **97.31%** → below 99% → **25% credit**
- Cost = 50 × 30 = **$1500** → effective cost = 1500 × 0.75 = **$1125**
- Mock version: 9 h downtime → 97.5% → 25% credit → **$1125**.

### Quick examples seen in papers 📌
- 99% guarantee, 12 h/day, 30 days → **max allowed downtime = 0.01 × 360 = 3.6 h**.
- Downtime 30 min and availability 0.80 → total = 30 ÷ 0.20 = 150 min → **uptime = 120 min** (not 150).
- Total 360 h, 3% downtime allowed → 10.8 h allowed.
- Solving for hours per day: 98.5% guarantee, downtime 11 h over 30 days. Allowed downtime = 0.015 × 30 × X ≥ 11 → X ≥ 24.44 (the key says "X is at least 24.44").

> [!bug] About the slide formula
> One Week 3 slide writes availability as `1 − (downtime/uptime)`. Do **not** use this. All the solved problems use **uptime ÷ total time** as above.

---

# 4. Docker, containers and Kubernetes

## 4.1 Containers 📘

A **container** is a lightweight package of an application's code **plus all its dependencies** (libraries, runtime, settings), so it runs the same everywhere. It is a **sandboxed process** that **shares the host OS kernel**.

> [!tip] In simple words
> A container is a **lunchbox**: your food and cutlery packed together, runs anywhere. A VM is a **whole mini-house** with its own kitchen, which is heavier.

**Three eras of deployment** 📘
- **Traditional**: apps run directly on a physical server. No resource boundaries → resource conflicts.
- **Virtualized**: many VMs on one server, each with its **own full OS**. Better isolation and utilisation.
- **Container**: like VMs but with **relaxed isolation, sharing the OS**, so they are lightweight and portable.

## 4.2 Containers vs VMs 📘

| | **Containers** | **Virtual machines** |
|---|---|---|
| Virtualize at | **OS level** | **Hardware level** |
| Kernel | **Share the host kernel** | Each VM has its own guest OS |
| Size | Tens of **MB** | Large (GBs) |
| Start-up | **Almost instant** | Slower (boots a whole OS) |
| Overhead | Very low (native-like process) | Higher (hypervisor + guest OS) |
| Isolation | Good, but weaker | **Stronger** |

> [!warning] Exam trap
> "VMs take up less space than containers" is **false**. Containers are lighter and smaller.

## 4.3 Docker basics 📘

**Docker** = an open platform to **build, ship and run** applications in containers ("develop, ship and run anywhere"; first released 2013).

| Term | What it is | Easy way to remember |
|---|---|---|
| **Dockerfile** | A **text build script** with instructions to create an image | The recipe |
| **Image** | A **read-only, packaged snapshot** with code, runtime, libraries, config | The frozen meal |
| **Container** | A **running instance of an image** | The meal being eaten |
| **Docker Hub** | A **public registry** where images are stored and shared | The supermarket / app store |
| **Docker Engine** | Builds images and **runs** containers (daemon + client) | The kitchen |
| **Docker Compose** | Defines **multi-container** applications | The full-course menu |

**Flow:** `Dockerfile → docker build → Image → docker run → Container`

**Commands from the slides** 📘
- Images: `images` (list), `run` (create a container from an image), `tag`, `pull` (download), `rmi` (delete image).
- Containers: `ps` (running), `ps -a` (all including stopped), `top`, `start`, `stop`, `pause`, `rm` (delete container), `commit` (make an image from a container).

**Architecture** 📘: Docker has a **client** and a **daemon** (server with a REST API over HTTP). The client sends requests; the **daemon** builds and manages images and containers. A **registry** stores images. 📌 The component that does the build from a Dockerfile is the **Docker daemon**.

> [!warning] Exam traps
> - "**Docker Hub** builds images and creates containers" is **false**. Hub is a **registry**. Docker **Engine** builds and runs.
> - "**Docker Compose** is a registry" is **false**. Compose orchestrates multi-container apps.
> - Docker images normally come from a **public registry (Docker Hub)** unless configured otherwise (not a private registry by default).

## 4.4 Volumes, networking, namespaces and cgroups 📌

| Topic | Fact |
|---|---|
| **Volumes** | Store data **outside the container's writable layer**, so data **survives when the container is deleted**. They are *not* deleted automatically with the container. |
| **Writable layer** | Data inside the container's own layer is **lost** when the container is removed. |
| **Networking** | Containers can talk to each other and the host. Default network mode is **bridge**, **not host**. |
| **Namespaces** | Give **isolation** (own process IDs, network, mount points). |
| **cgroups** | **Limit and monitor resource usage** (CPU, memory). |

> [!tip] In simple words
> - Container = a rented room that is **cleared when you leave**. A **volume** is a **storage locker outside the room** that keeps your stuff.
> - **Namespaces = walls** (each container sees only its own stuff). **cgroups = meters/limits** (each gets only so much CPU and memory).

> [!warning] Exam traps
> - "Docker volumes are deleted when the container is removed" → **false**.
> - "Containers launch in host network mode by default" → **false** (bridge).
> - "Data in the writable layer stays safe after the container is removed" → **false**.
> - "Namespaces provide resource quotas, cgroups provide isolation" → **swapped, false**.

## 4.5 Kubernetes 📘 + 📌

**Kubernetes (K8s)** = an open-source system to **automate deployment, scaling and management of containers** ("helmsman/pilot" in Greek). It works at the **container level, not the hardware level**, and gives PaaS-like features (deployment, scaling, load balancing).

> [!tip] In simple words
> Docker runs **one** container. Kubernetes is the **manager of hundreds of containers**: it restarts crashed ones, adds more when traffic rises, and decides which machine runs what.

**Cluster structure** 📘
- A cluster has **worker nodes** (machines that run containers) and a **control plane** (the brain that manages nodes and pods).
- Worker nodes host **Pods**, the parts of your application workload.
- In production, the control plane and nodes run on multiple computers for fault tolerance.

**Components asked in exams** 📌
| Component | Job |
|---|---|
| **Pod** | Smallest deployable unit; holds one or more containers |
| **etcd** | Distributed **key-value store** holding **cluster state and configuration** (the cluster's memory) |
| **kube-scheduler** | Picks **which node** a new Pod runs on (considers resources, affinity, constraints) |
| **kubelet** | Agent on each node; makes sure the Pod's containers are running |
| **API server** | The control plane's front door (general knowledge, not asked in the papers I checked) |

> [!warning] Exam traps
> - "Kubernetes operates at the **hardware** level" → **false** (container level).
> - **etcd stores state; the scheduler assigns pods** (don't swap them).
> - Docker is the container platform; Kubernetes is the **orchestrator**. They do not replace each other (Docker Engine does not "replace Kubernetes").

## 4.6 Why containers help (benefits) 📘
Separation of responsibility (devs do code, ops do deployment), **workload portability**, **application isolation**, agile development, efficient operations, run anywhere, can **replace VMs** when you only care about the app, quick prototyping, microservices, reproducible builds and continuous delivery.

---

# 5. Fog, edge and dew computing

## 5.1 Why they exist 📘

**Problems with cloud-only**
- The data centre is **far away** → **high latency**.
- Huge data from IoT devices → **bandwidth need** and **congestion** in the core network.
- Cloud was not designed for the **volume, variety and velocity** of IoT data.
- Some tasks (accident alerts, traffic control) need **very fast** responses.

> [!tip] In simple words
> If every tiny decision (like "brake now!") had to travel to a faraway cloud and back, it would be too slow. So we bring some of the thinking **closer to where data is produced**.

## 5.2 Cloud vs fog vs edge 📘

| | **Cloud** | **Fog** | **Edge** |
|---|---|---|---|
| Where | Remote data centre | **Between** cloud and devices: routers, gateways, base stations, Wi-Fi gateways | **At the device**: sensors, IoT devices, mobiles |
| Latency | **Highest** | Middle | **Lowest** |
| Resources | Huge | Moderate | Limited (processing, storage, power) |
| Role | Heavy processing, long-term storage | Real-time processing, filtering, aggregation | Basic data processing, data capture |

**Latency order: Edge (lowest) < Fog < Cloud (highest).**

> [!tip] Memory trick (sky to ground)
> **Cloud** is far in the sky (slow), **fog** is lower down near the ground, **edge** is right at the device, and **dew** (next section) is at the user's own end.

**How the layers work together** 📘: client layer (edge) → fog layer → cloud layer. If the **fog layer lacks resources, the request is passed to the cloud**.

## 5.3 Fog computing 📘

- **Fog computing** (introduced by **Cisco**) = data, processing and applications are concentrated in devices **at the network edge** rather than almost entirely in the cloud. It extends the cloud to the edge of the network.
- **Enablers**: virtualization, containers (e.g. Docker), service-oriented architecture, software-defined networking (SDN).
- **Advantages**: **low latency**, location awareness, wide geographic distribution, mobility, very large number of nodes, wireless access, real-time/streaming support, heterogeneity, **less network congestion and bandwidth**, lower cost at cloud.
- **Use cases**: **connected vehicles**, **smart grid**, **smart traffic lights**, emergency evacuation, natural disaster alerts, pre-processing sensor data before sending to the cloud, smart cities, IoT.
- **Challenges**: resource allocation while guaranteeing latency, load balancing, state migration when a node fails, **security** (authentication at gateways and fog nodes, **man-in-the-middle** attacks, privacy, smart-meter tampering/IP spoofing).

> [!warning] Exam traps
> - "Fog and edge are **substitutes/replacements** for the cloud" → **FALSE**. They **complement** the cloud (the slide title is literally "not a replacement of Cloud Computing").
> - Fog's advantage is **proximity to end users**, not larger capacity than the cloud.

## 5.4 Health case study (Cloud-Fog-Edge) 📘

- Five levels: **Level 0 Cloud → Level 1 ISP → Level 2 Area Gateway → Level 3 Mobile → Level 4 IoT devices.**
- Simulated with **iFogSim**; prototype used **Raspberry Pi as fog devices** and **AWS as cloud**.
- Results (fog vs cloud-only):
  - **Latency**: fixed and low in fog (control-loop modules sit at the area gateway); high in cloud-only.
  - **Network usage**: **much lower** with fog (only a few positive cases go to the cloud).
  - **Cost**: lower with fog (only cloud resources cost money; the rest are owned).
  - Energy: compared across DC, mobile and edge for different configurations.

## 5.5 Dew computing 📘

**Dew computing** combines the cloud with the **capabilities of the user's own device** (PC, phone). It tries to solve the cloud's **dependence on internet access**: the local device keeps working **offline** and **synchronises** with the cloud when connected.

> [!tip] In simple words
> **Dropbox** is the textbook example. Your files live in the cloud *and* on your device. With no internet you still open them; when internet returns they sync.
>
> **Cloud = far, fog = beside you, dew = on you (at the user end).** Like clouds high up, fog near the ground, dew on the ground.

**Two key features** 📘
1. **Independence**: the local device works without a continuous internet connection.
2. **Collaboration**: it connects to the cloud and **synchronises data** when appropriate.

**Dew service models and examples** 📘
| Model | Idea | Example |
|---|---|---|
| **Storage-in-Dew** | Local storage is copied to the cloud | Dropbox |
| **Web-in-Dew** | Local device keeps a copy of part of the WWW | Offline web |
| **Database-in-Dew** | Local and cloud both hold the same database (one acts as backup) | Replicated DB |
| **Software-in-Dew** | Software configuration/ownership saved in cloud | App Store, Google Play |
| **Platform-in-Dew** | Dev tools local, settings and data synced to cloud | GitHub |
| **Infrastructure-as-Dew** | Local device supported dynamically by cloud services | DVM copy in cloud |

**Architecture** 📘: a **Dew Virtual Machine (DVM)** on the local machine runs the **dew server**, which serves requests and does **replication, distribution and synchronisation**.

**Challenges** 📘: power management, processor utility, data storage, viability of the operating system.

### Dew vs fog (very likely MCQ) 📘 + simple view
|                 | **Fog**                                           | **Dew**                                                             |
| --------------- | ------------------------------------------------- | ------------------------------------------------------------------- |
| Location        | **In the network** (routers, gateways) near users | **On the user's own device**                                        |
| Needs internet? | Needs network connectivity                        | **Works offline**, syncs later                                      |
| Main goal       | **Cut latency** and bandwidth for real-time apps  | **Reduce dependence on the internet**, independence + collaboration |

---

# 6. OpenStack

## 6.1 What it is 📘
**OpenStack** is a **cloud operating system** that controls large pools of **compute, storage and networking** across a data centre, managed through a **dashboard**. Started as a collaboration between **NASA and Rackspace**. It is used for **IaaS** (and PaaS/SaaS can be built on top).

## 6.2 Components (learn this table fully) 📘

| Service        | Project        | Job                                                                           | Easy memory hook                                  |
| -------------- | -------------- | ----------------------------------------------------------------------------- | ------------------------------------------------- |
| Compute        | **Nova**       | Manages the **lifecycle of VMs**: spawn, schedule, decommission               | **N**ova = **N**ew VMs                            |
| Networking     | **Neutron**    | Network connectivity-as-a-service (networks, IPs, routers)                    | **N**eutron = **N**etwork                         |
| Object storage | **Swift**      | Stores **unstructured objects/files** via REST/HTTP, replicated across drives | **S**wift = **S**tore objects/files               |
| Block storage  | **Cinder**     | **Persistent block volumes** for running VMs                                  | **C**inder = **C**hunks (blocks) like a hard disk |
| Identity       | **Keystone**   | **Authentication and authorization**; catalog of endpoints                    | **K**eystone = **K**ey/login                      |
| Image          | **Glance**     | Stores and retrieves **VM disk images**                                       | **G**lance = **G**old copy of the OS              |
| Dashboard      | **Horizon**    | **Web dashboard** to launch instances, assign IPs, set access                 | **H**orizon = what you **see**                    |
| Telemetry      | **Ceilometer** | Monitors and **meters** usage for billing and benchmarking                    | **C**eilometer = **C**ounts usage                 |

📌 Also asked: **Heat** = orchestration. **Nova Scheduler** *chooses* which host runs the VM; **Nova Compute** *actually runs* it.

## 6.3 Three kinds of storage 📘

| Type | Lasts | Managed by | Used for |
|---|---|---|---|
| **Ephemeral** | Until the VM is terminated; local file system | **Nova** | OS and scratch space |
| **Block** | Until you delete it; seen as a disk (e.g. /dev/vdc) | **Cinder** | Extra persistent disk for a VM |
| **Object** | Until you delete it; accessible from anywhere | **Swift** | Files, VM images |

## 6.4 What happens when you launch a VM (summary) 📘
1. User logs in to **Horizon** and clicks create.
2. **Keystone** authenticates and gives a token.
3. **Nova** starts provisioning and saves state in the DB.
4. **Nova Scheduler** finds a suitable host.
5. **Neutron** sets up networking (IP, gateway, DNS).
6. **Cinder** provides a block device.
7. **Glance** looks up the image; the image is retrieved via **Swift**.
8. The VM is run by the **hypervisor**.

> [!tip] Memory trick for the order
> **H-K-N-S-N-C-G-S**: "**H**ow **K**ind **N**ew **S**tudents **N**eed **C**ool **G**reat **S**ongs" (Horizon, Keystone, Nova, Scheduler, Neutron, Cinder, Glance, Swift).

> [!warning] Exam traps
> - "**Swift** provides block storage" → **FALSE**. Swift = **object**; **Cinder = block**.
> - VMs cannot reach the internet → likely **Neutron router** not configured. VMs get no IP address automatically → **Neutron DHCP** agent problem.
> - **Cinder volume stays** if the VM is deleted (unless you delete it); ephemeral storage is released.
> - Horizon is the **official web dashboard**.

---

# 7. Azure and GCP

## 7.1 Azure 📘

**Microsoft Azure** = a collection of integrated cloud services to build, deploy and manage apps. It supports **hybrid cloud** and is a **public cloud platform**.

**Azure App Service / Web Apps** = a **highly scalable, self-patching web hosting service** (PaaS).

**Steps to deploy a Python web app (slide demo)**: set up a deployment user → create a **resource group** → create an **App Service plan** → create the **web app** → configure Python → configure **local Git** deployment → **push** to the Azure remote → browse to `<name>.azurewebsites.net`.

| Term | Meaning |
|---|---|
| **Resource group** | A **logical container** that holds related Azure resources (web apps, databases, storage) |
| **App Service plan** | Defines the **region, instance size (small/medium/large), scale count (1 to 20 instances) and SKU (Free, Shared, Basic, Standard, Premium)** of the servers that host your app. Several apps can **share one plan to save money.** |

> [!tip] In simple words
> The **App Service plan = the rented server package** (where, how big, how many, which tier). The **web app = your site that lives on that package**.

> [!warning] Exam trap
> "App Service plan **defines security**" → **false**. It defines **compute and scaling** (region, size, instances, tier).

### Extra Azure facts asked in papers 📌 (one-liners)
- **Deployment slots**: separate **live-like staging copies** of your web app (e.g. staging) that you can **swap** with production. **Premium (P1v3 and higher) allows up to 20 slots.** Premium also gives **traffic warm-up before the swap**.
- **Azure SQL Database tiers**: **Business Critical** = mission-critical, high performance, built-in replicas/HA. **Hyperscale** = storage that **grows automatically beyond 100 TB**.
- **Availability Zones**: **physically separate locations within one region** → protects against a data-centre failure.
- **Securely access secrets from App Service**: **Managed Identity + Key Vault** (no credentials stored in code).
- **Force HTTPS** in App Service: the **"HTTPS Only"** setting.
- Maximum number of **data disks on a VM** is limited by **VM size/SKU**.

## 7.2 Google Cloud Platform (GCP) 📘

GCP = a set of **modular cloud services** to build, test and deploy apps on Google's infrastructure. Features: managed services, auto scale-up and **scale-down (pay only for what you use)**, global network.

| GCP service | Type | What it is |
|---|---|---|
| **App Engine** | **PaaS** | Focus on your code; no patching or maintenance |
| **Compute Engine** | **IaaS** | Raw virtual machines, build anything |
| **Cloud SQL** | Database | **MySQL** (relational) |
| **Cloud Datastore** | Database | **NoSQL** database |
| **Cloud Storage** | Object storage | **Flexible object storage with global edge caching**; can host a static website |
| **Google APIs / Cloud Endpoints** | Integration | Add ready-made Google features to your app / scale APIs |

> [!warning] Exam traps
> - "**Cloud Datastore** provides object storage with edge caching" → **FALSE**. That is **Cloud Storage**. Datastore is a NoSQL database.
> - App Engine is **PaaS**, Compute Engine is **IaaS**.

### App Engine deployment steps and commands 📘
- Every app needs **`app.yaml`** (config) and code like **`main.py`**.
- `dev_appserver.py $PWD` → **starts the local development server** (it reloads when files change).
- `gcloud app deploy app.yaml --project <id>` → **deploys** to App Engine.
- `gcloud app browse` → **opens the deployed app** in the browser (**it does NOT start the local server**).
- A deployed app is reachable through its **appspot URL**.

### Traffic splitting 📌
App Engine can send, for example, **70% of traffic to version v1 and 30% to v2** using the `set-traffic` command with `--splits v1=0.7,v2=0.3`. Key idea: **splits assign percentages to deployed versions** (useful for gradual rollouts and testing). In the old paper the key picks the option `gcloud app services set-traffic ... splits v1=0.7,v2=0.3`.

### GKE vs Cloud Run 📌
| | **GKE** (Google Kubernetes Engine) | **Cloud Run** |
|---|---|---|
| What | **Managed Kubernetes**: manages your **clusters** | **Serverless containers**: run a container **without managing any cluster** |
| Best for | Complex, long-running container platforms where you want Kubernetes control | **Event-driven**, request-driven container workloads, pay per use |

> [!tip] In simple words
> **GKE** = you get a Kubernetes cluster to run (more control, more setup). **Cloud Run** = hand over a container and Google runs it (zero cluster management).

### Which GCP database fits which job 📌 (high-yield)
| Need                                                                                                   | Pick                          | Memory hook                             |
| ------------------------------------------------------------------------------------------------------ | ----------------------------- | --------------------------------------- |
| **Global, strongly consistent, multi-row transactions** (SQL-like)                                     | **Cloud Spanner**             | **Span**s the whole world               |
| **Petabytes of time-series/IoT data, very high write throughput, millisecond reads, no complex joins** | **Cloud Bigtable**            | **Big** and fast, key-value/wide-column |
| **Scalable NoSQL document DB, global replication**                                                     | **Firestore** (and Datastore) | Flexible documents                      |
| **Analytics / data warehouse, SQL over huge data (serverless)**                                        | **BigQuery**                  | **Big** **Query** = big analysis        |
| **Normal relational DB (MySQL/Postgres)**                                                              | **Cloud SQL**                 | Regular SQL                             |
| **Streaming data ingestion**                                                                           | **Pub/Sub**                   | Publish and subscribe messages          |

Typical analytics pipeline answer: **Pub/Sub (ingest) → BigQuery (analyse) → Data Studio/Looker (dashboards)**.



