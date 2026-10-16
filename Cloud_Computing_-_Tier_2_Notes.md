---
title: Cloud Computing - Tier 2 Notes
tags: [cloud-computing, exam, tier-2, nptel]
course: Cloud Computing (NPTEL, IIT Kharagpur, Prof. Soumya K. Ghosh)
exam-format: MCQ
---

# ☁️ Cloud Computing - Tier 2 Notes

> [!abstract] How to use this file
> Each topic has the same layout:
> 1. **Slide notes**: what the PPT actually says (short).
> 2. **In simple words**: an easy explanation or analogy.
> 3. **Exam traps**: wrong statements that appear in old papers and mocks (the "one wrong word makes it false" questions).
>
> **Label guide**
> - 📘 = taken from the Week slides.
> - 📌 = **not on the slides**, but the previous papers/mocks/assignments ask it, or it is standard knowledge. Learn it as a one-line fact.
>
> Tick the boxes as you finish each topic. Read [[Cloud_Computing_-_Tier_1_Notes]] first.

**Topics (in order of marks)**
- [ ] [[#1. IoT, sensor cloud and CPS]]
- [ ] [[#2. Cloud security]]
- [ ] [[#3. Serverless computing]]
- [ ] [[#4. Green and sustainable cloud]]
- [ ] [[#5. Mobile cloud computing]]
- [ ] [[#6. VM migration]]
- [ ] [[#7. XML and web services]]

> [!note] OpenStack is not here
> OpenStack was in Tier 2 on the topic list, but it is already in the Tier 1 notes file (Section 6). Study it there.

---

# 1. IoT, sensor cloud and CPS

## 1.1 Internet of Things (IoT) 📘

**IoT** = extending the Internet so that devices and physical objects ("things") are connected, can communicate and can network with each other. Sensors (RFID, cameras, mobile phones) collect data from the environment and let things respond to changes in the physical world.

**Basic IoT architecture: three building blocks** 📘
1. **Things** (sensors and actuators)
2. **Gateway**
3. **Network and Cloud**

**Several aspects of IoT systems** 📘
- **Scalability**: more sensors, networks, data and processing power.
- **Big data**: advanced IoT systems analyse vast amounts of data to find patterns.
- **Role of cloud computing**: IoT needs cloud storage, processing and management.
- **Real time**: data flows in continually and responses must be timely.
- **Highly distributed**: can span buildings, cities, even the globe; processing can happen centrally (cloud) or at the edge (gateways, smarter sensors).

**IoT-cloud integration** 📘: IoT infrastructures (logistics, smart cities, healthcare) create high demand for storage, processing and management, so IoT and cloud have to be integrated.
- **iCOMOT** is a toolset for managing IoT cloud systems. Top layer = IoT applications running across IoT and cloud. Middle layer = the software layer (the IoT cloud system built on cloud services and IoT elements). Bottom layer = tools to monitor, control and configure the software layer.
- **Vehicular data cloud** is the motivating example: a multilayer platform using cloud and IoT to help with transportation problems.

> [!tip] In simple words
> Things collect data, the **gateway** collects it from many things and passes it on, and the **cloud** stores and analyses it.

**IoT gateway role** 📌: it **bridges the different IoT device protocols into a standard format** for the cloud. It does **not** replace cloud storage, and it is not a central server for every device in the world.

> [!warning] Exam traps
> - "The IoT gateway performs all analytics in the cloud" → false.
> - "The IoT gateway replaces the need for cloud storage" → false.
> - Fog's motivation is to **reduce latency and network load** for edge-heavy apps. It does **not** replace the cloud (Tier 1, Section 5).

## 1.2 Sensor cloud 📘

**Sensor cloud** = an infrastructure that allows truly pervasive computation, using **sensors as the interface between the physical and cyber worlds**, **data-compute clusters as the cyber backbone** and the **Internet as the communication medium**. It integrates large sensor networks with sensing applications and cloud computing.

- Lets users collect, access, process, visualise, archive, share and search large amounts of sensor data.
- Supports the **complete sensor data life cycle**, from collection to backend decision support.
- Lets different sensor networks, spread over huge areas, be connected together.

**Two proxies** 📘

| Component | Job |
|---|---|
| **Sensor-Cloud Proxy** | Interface between the sensor resources and the cloud fabric. Exposes sensors as **cloud services**, manages connectivity, indexing and sensing jobs |
| **Sensor Network Proxy** | For sensors **without a direct connection** to the cloud, it provides the connection. The sensor network is still managed from the cloud, and it improves **scalability** |

**Virtual sensor** 📘: a **software emulation of a physical sensor** that gets its data from underlying physical sensors. It gives users a **customised view** with **distribution and location transparency**. Wireless sensors can barely run multiple tasks, so they are hard to run on multiple VMs, and virtual sensors solve this.

**Virtual sensor configurations** 📘

| Configuration | Meaning |
|---|---|
| **One-to-many** | One physical sensor serves many virtual sensors (the physical sensor is shared) |
| **Many-to-one** | Many physical sensors or sensor networks (e.g. a region) feed one virtual sensor that gives aggregated data |
| **Many-to-many** | A mix of the two above |
| **Derived** | A virtual sensor made from a **combination of multiple, often different types of, physical sensors**. It generalises the other three |

Example from the slides: the question "Are the overall environmental conditions safe in a wildlife habitat?" is answered by a **derived** virtual sensor that combines readings from several environmental sensors into a safety level.

> [!tip] In simple words
> A **physical sensor** is the real thermometer. A **virtual sensor** is your own "copy" of it on the cloud. A **derived sensor** is a smart combined sensor, like a "habitat safety" sensor made from temperature + humidity + air quality sensors.

> [!warning] Exam traps
> - **Derived sensor** = a virtual sensor generating output by **combining data from multiple, often heterogeneous, physical sensors** (it is **not** "a modified physical sensor" and **not** "only raw data").
> - **Virtual sensor** = software emulation of a physical sensor that gets data from physical sensors.

## 1.3 Cyber-physical systems (CPS) 📘

- **CPS** = an orchestration of computers and physical systems. Embedded computers monitor and control physical processes, usually with **feedback loops**, where physical processes affect computations and vice versa.
- Term coined around **2006** by **Helen Gill** at the US National Science Foundation.
- CPS is about the **intersection, not the union**, of the physical and the cyber.
- Uses **sensors and actuators** to link computation with the physical world. "Computing as a physical act".
- The networks of sensors, actuators and processing devices form what the slides call **Smart Networked Systems and Societies (SNSS)**.
- **Cyber-Physical Cloud Computing (CPCC)** = a system environment that can **rapidly build, modify and provision** cyber-physical systems made of cloud-based **sensor, processing, control and data services** (NIST report, 2013).

---

# 2. Cloud security

## 2.1 Security attacks 📘

**Security attack** = any action that compromises the security of information. **Four types**, each hits a different goal:

| Attack | What happens | Hits |
|---|---|---|
| **Interruption** | Source-to-destination flow is cut | **Availability** |
| **Interception** | A third party gets access to the flow | **Confidentiality** |
| **Modification** | The message is altered | **Integrity** |
| **Fabrication** | A false message is inserted | **Authenticity** |

> [!tip] Memory trick
> **I-I-M-F** matches **A-C-I-A**: **I**nterruption → **A**vailability, **I**nterception → **C**onfidentiality, **M**odification → **I**ntegrity, **F**abrication → **A**uthenticity.

**Passive vs active attacks** 📘

| | **Passive** | **Active** |
|---|---|---|
| Goal | **Obtain** information being transmitted (eavesdropping) | **Modify** the data stream or **create a false stream** |
| Types | Release of message contents, **traffic analysis** | **Masquerade**, **replay**, **modification**, **denial of service** |
| Detection | **Very difficult** | Involve changing data, so they leave traces |

**CIA triad** 📌: **Confidentiality** (only authorised access), **Integrity** (data stays unaltered and accurate), **Availability** (data and service are reachable when needed).

**Goals of security** 📘: **Prevention** (stop attackers violating policy), **Detection** (detect violations), **Recovery** (stop the attack, assess and repair damage, keep functioning even if the attack succeeded).

**Six steps of network security** 📘
1. Determine the security policy
2. Implement the security policy (firewalls and IDS)
3. Reconnaissance
4. Vulnerability scanning
5. Penetration testing
6. Post-attack investigation

**Firewall types** 📘: **packet filter** (by destination IP, port or protocol), **stateful** (tracks ongoing TCP sessions and drops out-of-session packets), **application proxy** (acts as a proxy for one application and scans all layers). An **IDS** scans incoming messages and raises alerts for suspected scans or attacks.

> [!warning] Exam traps
> - "**Interception** is an attack on **integrity**" → **false** (it is confidentiality).
> - "Passive attacks involve modifying data" → false.
> - The three goals of security management are **Prevention, Detection, Recovery** (not CIA, which is the set of security properties).

## 2.2 Gartner's seven cloud security risks 📘

| #   | Risk                                | One-line meaning                                                                                                                                       |
| --- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | **Privileged user access**          | Outsourced services bypass your physical, logical and personnel controls. Ask who manages your data                                                    |
| 2   | **Regulatory compliance and audit** | Hard to **audit data held outside your organisation** and to prove compliance. Providers that refuse external audits can only be used for trivial work |
| 3   | **Data location**                   | Data may sit in different **jurisdictions** with different laws. Who is responsible for compliance (SOX, HIPAA)?                                       |
| 4   | **Data segregation**                | Your data sits in a **shared environment** with other customers. Encryption helps but isn't a cure-all                                                 |
| 5   | **Recovery**                        | What happens in a disaster? Needs replication across sites. **RPO** = maximum data loss allowed. **RTO** = time allowed for recovery                   |
| 6   | **Investigative support**           | Logs of many customers are co-located, so investigations are hard. A neutral third-party monitor is the best fix                                       |
| 7   | **Long-term viability**             | Can you get your data back, in a usable format, if the provider shuts down or you switch? Leads to **vendor lock-in**                                  |

> [!tip] Memory trick
> **P-R-D-D-R-I-L**: **P**rivileged, **R**egulatory, **D**ata location, **D**ata segregation, **R**ecovery, **I**nvestigative, **L**ong-term.

> [!warning] Exam trap
> Difficulty **proving compliance when a third party holds the data, maybe in another country** → **Regulatory Compliance and Audit** (not Data Location, not Privileged User Access).

## 2.3 Virtualization and hypervisor risks 📘

- **Multi-tenancy**: VMs of different customers run on the same hardware, and you can't stop your VM from sharing a host with an attacker.
- Hypervisor vulnerabilities: **keystroke logging**, **VM backdoors** (covert channels), **ARP poisoning** (redirecting a VM's packets).
- **Rogue hypervisor rootkits**: a fake hypervisor is started underneath the OS and hides itself.
- **External modification** of a poorly protected hypervisor.
- **VM escape**: bad VM configuration lets malicious code **bypass the virtual environment** and get root or kernel access to the **physical host**.
- **Denial of service** by one VM hogging resources.
- **Access control and identity management**: needs proper access control for CIA; identity theft is a major challenge.

	**Compromised hypervisor = "key to the kingdom"** 📌: the attacker can control **all the VMs on that physical machine**. 

> [!warning] Exam trap
> "A compromised hypervisor only affects one VM" → false.

## 2.4 Co-residence attack ("Hey, You, Get Off of My Cloud") 📘

**The paper**: Ristenpart, Tromer, Shacham, Savage, ACM CCS 2009. It is the first work on **cloud cartography**. It was tried on **Amazon EC2**, with up to **40%** success at co-residing with a target VM.

**Two steps of the attack**
1. **Placement**: put the attacker's malicious VM on the **same physical machine** as the target.
2. **Extraction**: steal confidential data through a **side channel**.

**The four questions the paper answers**

| Q | Question | Key idea |
|---|---|---|
| Q1 | Where is an instance located in the cloud? | **Cloud cartography** (map the IP address space, instance types, zones) |
| Q2 | Are two instances **co-resident**? | Network checks (below) |
| Q3 | Can an attacker launch instances that become **co-resident** with a target? | **Brute-force placement** and **placement locality** |
| Q4 | Can the attacker **exploit** the co-residence? | Cross-VM information leakage (side channels) |

**How co-residence is checked (Q2)** 📘: two instances are likely on the same machine if they have
- a **matching Dom0 IP address** (found with a TCP SYN traceroute, the last hop is **Dom0**, the privileged Xen domain), or
- **small round-trip times**, or
- **numerically close internal IP addresses**.

**Dom0** = the privileged VM in Xen. It manages guest images, provisions resources, and routes packets for guests.

**Causing co-residence (Q3)** 📘
- **Brute force**: many probe instances over time. Result: **141 of 1686** targets (**8.4%**).
- **Placement locality**: launch the attacker's instances **soon after** the victim's. 20 probes in 5 minutes gave **40%** success.

**Exploiting co-residence (Q4)** 📘: **cache-based load measurement** (prime, trigger, probe), **traffic-rate estimation**, and **keystroke timing** (to recover passwords).

**Preventive measures** 📘: randomise IP allocation, block tools like nmap and traceroute, hide Dom0, or disallow co-residence entirely. The last is good for users but **inefficient for the provider**, and **there is no solution for side-channel leakage**.

> [!warning] Exam traps
> - **Placement phase** goal = put a malicious VM on the **same physical machine** as the victim (not to steal bandwidth, not to encrypt data).
> - A **matching Dom0 IP** for two instances strongly suggests the **same physical machine** (it is not the target's public IP).
> - Extraction uses a **side channel**.

## 2.5 Secure collaboration in SaaS clouds 📘

When different domains (organisations) share a SaaS cloud, their **role-based access control (RBAC)** policies must be mapped to each other.

- **IDRM (Inter-Domain Role Mapping)**: finds a **minimal set of roles** that covers the requested permissions. No polynomial-time exact solution, so **greedy heuristics** are used. Two variants: **IDRM-safety** and **IDRM-availability**.
- **Two kinds of access conflict**:
  - **Cyclic inheritance conflict**: a user gains **unauthorised permissions by going around a cycle of roles** across collaborating domains.
  - **Violation of Separation of Duty (SoD)**: a user uses permissions from **several domains** to do a critical task **alone** that should need more than one person.
- **Detection**: needs at least one exit role. **Removal**: replace the relation with a safe one (hybrid hierarchy) or introduce a **virtual role**.

> [!tip] In simple words
> **SoD** = the person who writes the cheque should not be the one who approves it. In multi-domain clouds, someone could quietly collect both powers and do both. **Cyclic inheritance** = role A inherits from B, B from C, and C from A across domains, so someone ends up with more power than intended.

## 2.6 Cloud broker and provider selection 📘

- **Why**: flexible choice of provider, trustworthiness of provider, monitoring services, avoiding **vendor lock-in**.
- **Approach**: the broker uses a **fuzzy inference engine**.
  - **Input**: QoS offered by a provider and its **trustworthiness**.
  - **Output**: **suitability** of the provider for the customer.
  - The request goes to the provider with **maximum suitability**.
- **CloudCmp** compares providers to measure the QoS they offer.
- 📌 **Fuzzification** = mapping **crisp inputs** (like 99.98% uptime) to **linguistic fuzzy sets** (like "Excellent").
- 📌 **Role of an intelligent cloud broker**: help customers **select the optimal provider and manage the service lifecycle**.
- 📌 **Resource brokering** = negotiating resources through an intermediary agent so they are available at the right time and price.

> [!warning] Exam trap
> Fuzzification is **not** "converting linguistic values into crisp numbers" (that is the reverse, defuzzification) and **not** "applying the rule base".

---

# 3. Serverless computing

## 3.1 What it is 📘

**Serverless computing** = providing backend services on an **as-used basis**. Developers write and deploy code without worrying about the underlying infrastructure. It removes the need for system administration, so developers focus on core logic and don't create VMs or containers.

- Developers submit logic as **functions**, and the provider runs them in a **shared runtime environment** and handles scaling by running many functions in parallel.
- The code runs in **almost stateless containers** that are **event-triggered and ephemeral** (may last for one invocation).
- Servers still exist, they are just **invisible** to the developer.
- The target audience shifts from **system administrators (cloud)** to **programmers (serverless)**.

> [!tip] In simple words
> Normal cloud: you rent a kitchen. Serverless: you hand over a recipe, the restaurant cooks it when an order comes in, and you pay only per dish cooked.

## 3.2 FaaS vs BaaS 📘

| | **FaaS** (Function as a Service) | **BaaS** (Backend as a Service) |
|---|---|---|
| Idea | You give **small, stateless functions**. The provider manages resources, lifecycle and event-driven execution | You replace server-side parts with **ready-made services** and write app logic only in the frontend |
| Triggered by | Events | API calls from the app |
| Examples | AWS Lambda, Google Cloud Functions, Azure Functions | Authentication systems, database management, cloud storage, hosting, **Google Firebase** |
| Notes | Each function is a small part of an app. Execution time is **limited** | Developer outsources everything behind the scenes |

Serverless = **BaaS + FaaS**. 📘

## 3.3 Providers 📘

| Provider | Key points |
|---|---|
| **AWS Lambda** | Event-driven platform. You upload code (Java, Python, Go, C# and others), and it runs when triggered by AWS services (e.g. a file added to **S3**, an HTTP request through **API Gateway**). **Charges only while the code runs.** Concepts: function, runtime, event source |
| **Google Cloud Functions** | Single-purpose functions attached to events. **Trigger = event + event data.** Event sources: **HTTP, Cloud Storage, Pub/Sub, Firebase, Stackdriver Logging, Firestore, Compute Engine, BigQuery** |
| **Azure Functions** | A function = **code + configuration**. Languages: C#, Java, JavaScript, PowerShell, Python. **Consumption plan = you pay only while the functions run**. Premium and App Service plans give extra features |

📌 **Maximum run time of one AWS Lambda invocation: 15 minutes.** This is general knowledge, not on the slides, and one old paper asked it, so check it against your own paper's wording.

## 3.4 Challenges 📘
- **Asynchronous calls** between functions make the system complex.
- **Functions calling other functions** make debugging hard and can **double the cost** (you pay for both while they run).
- **Too many libraries** raise the image size and the **warm-up time**.
- **Too many technologies** raise maintenance complexity and skill needs.
- **Too many functions** or unused functions need housekeeping.

> [!warning] Exam traps
> - Serverless means **no servers exist** → false. Servers exist but are managed by the provider.
> - In FaaS the provider manages the resources and lifecycle; developers still write the functions.
> - Lambda charges for **time the code runs**, not for idle time.

---

# 4. Green and sustainable cloud

## 4.1 Why it matters 📘

- **Green computing** = environmentally responsible use of computers. Green cloud aims for efficient processing **and** a lower environmental impact.
- IT industry = **2%** of world CO2 emissions (Gartner 2007).
- Data centres use **10 to 100 times** more energy per square foot than an office.
- Energy is **10%** of data centre operating cost, and could reach **50%**.
- Amazon estimates energy-related costs at **42%** of its data-centre budget.

**Where the energy goes in a data centre** 📘

| Part | Share |
|---|---|
| **IT equipment** | **45%** |
| **Cooling system** | **40%** |
| **Power distribution** | **15%** |

So **more than half** of the power is **not** used by IT equipment (and not for computation itself). 📌

**Server energy** 📘: an **idle server consumes about 66% of its peak power**. This is the key reason to turn off or consolidate idle servers.

> [!tip] In simple words
> A server that does nothing still burns two thirds of the power it uses at full work. So it is far cheaper to pack work onto fewer servers and switch the rest off.

## 4.2 Green Cloud Framework 📘

Two main branches:
- **Virtual machine controls**: **scheduling** (power-aware, thermal-aware), **management** (live **migration**, **dynamic shutdown**), and **VM image design**.
- **Data centre design**: **server and rack design**, **air conditioning and recirculation**.

**Power-aware scheduling** 📘
- Power use is **non-linear** with the number of cores used, so schedule **as many VMs as possible onto one multi-core node** (greedy algorithm: track cores per node and match VM needs to node capacity).
- Slide example: 8 VMs packed onto **one node** (the other three idle) used **485 W**, while spreading them evenly (2 per node over four nodes) used **552 W**.

**VM management** 📘
- **Load drops**: live-migrate VMs onto **more utilised nodes** and **shut down unused nodes**.
- **Load rises**: use **Wake-on-LAN (WOL)** to start waiting nodes and place new VMs there.

**Minimising VM images** 📘 (smaller images save energy and time)
- Boot time cut from **38 s to 8 s**, and image size from **4 GB to 635 MB**.
- A smaller image **reduces live-migration time**. A leaner image is also better for a service-oriented architecture.

**Green broker** 📘: a cloud broker that adds carbon awareness, in 3 layers: **(1)** analyse user requirements, **(2)** calculate **cost and carbon footprint** of services, **(3)** **carbon-aware scheduling**. The framework is called the **Carbon Aware Green Cloud Framework**.

**Workload consolidation** 📌 = packing VMs onto the **minimum number of physical servers** and powering down the idle ones. This is the main energy-saving strategy asked about in papers.

**PUE (Power Usage Effectiveness)** 📌 = **total facility power ÷ IT equipment power**. Lower is better, and 1.0 is the ideal. Example from a paper: 90 total, 75 to IT, PUE = 90 ÷ 75 = **1.2**.

> [!warning] Exam traps
> - A server at 0% load uses **almost no** power → false (it still uses about 66% of peak).
> - The **majority** of data-centre power goes to computation → false (IT equipment is 45%).
> - **VM image minimisation** and **live migration** are *supporting* techniques. The strategy of **packing VMs onto the fewest servers and switching off idle ones** is **workload consolidation**.

## 4.3 Sustainable cloud computing 📘

**Sustainable cloud** = running cloud data centres (CDCs) to **minimise energy use and carbon footprint while keeping reliability**.

- CDC energy use is expected to reach **8000 TWh by 2030**.
- Big CSPs (Google, Amazon, Microsoft, IBM) plan to power data centres with **renewable energy**.
- Data centres can be placed or relocated based on **waste heat recovery**, access to **green resources** and **free cooling**.

**Conceptual model components** 📘
- **Cloud architecture**: SaaS, PaaS, IaaS layers.
- **Power manager**: controls renewable energy and grid (fossil) electricity. Deadline-driven workloads can use grid power. An **Automatic Transfer Switch (ATS)** switches between the two.
- **Application model**: data parallel, function parallel, message passing.
- **Thermal-aware scheduling**: architecture (single-core or multi-core) and mechanism (**reactive** or **proactive**) to avoid heating problems.
- **Capacity planning**: for power infrastructure, IT resources and workloads, to reach the expected return on investment (ROI).
- **Waste heat utilisation**: for example **vapour-absorption cooling** that uses waste heat.

**Reliability vs sustainability trade-off** 📘
- Replicating services for reliability needs **extra resources and energy**.
- Switching servers on and off too often **reduces the reliability** of components like storage and memory.

---

# 5. Mobile cloud computing (MCC)

## 5.1 Basics 📘

**MCC** = the combination of **cloud computing, mobile computing and wireless networks** to bring rich computational resources to mobile users. Resource-intensive work runs in the cloud, so phones don't need powerful hardware.

**Advantages** 📘: **extends battery life** (computation offloading), more storage and processing power, better reliability and availability, dynamic provisioning, scalability, multi-tenancy, easy integration.

**Pros and cons** 📘

| Pros | Cons |
|---|---|
| Saves battery power | Program state must be **sent to the cloud**, which uses battery |
| Makes execution faster | **Network latency** can delay execution |

> [!tip] In simple words
> Like asking a friend with a powerful laptop to do your heavy video render. It is worth it only if the file you send is small and the job is big.

## 5.2 Key components 📘

| Component        | Job                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------- |
| **Profiler**     | Monitors the app to collect execution time, power use and network traffic                       |
| **Solver**       | Decides **which parts run on the mobile and which on the cloud**                                |
| **Synchronizer** | Collects the results of the split execution, combines them, and hides the details from the user |

## 5.3 Offloading: when is it worth it? 📘

Energy saved by offloading:

```
Energy saved = Pc × (C / M)  −  Pi × (C / S)  −  Ptr × (D / B)
with S = F × M, this becomes:
             = (C / M) × (Pc − Pi / F)  −  Ptr × (D / B)
```

| Symbol | Meaning |
|---|---|
| **C** | Amount of computation (instructions) |
| **D** | Data to be transmitted |
| **M** | Mobile speed |
| **S** | Cloud speed, **S = F × M** (the server is **F times faster**) |
| **B** | Wireless bandwidth |
| **Pc / Pi / Ptr** | Energy per second when the phone is computing / idle / transmitting |

**Rule**: energy is saved when the result is positive, i.e. when **D/B is small compared with C/M** and **F is large**. In plain words: **offload when computation C is large, data D is small, bandwidth B is high, and the cloud is much faster.**

> [!warning] Exam traps
> - Offloading is good when the task is **light on computation and heavy on data transfer** → **false** (it is the opposite).
> - Offloading is good when **bandwidth is low** → **false**.
> - "Not all applications save energy when moved to the cloud" is **true**.

## 5.4 Partitioning and systems 📘
- **Task partitioning problem**: split an app's call graph into methods that run **locally** and methods that run **remotely**. It is solved as a **0-1 integer linear program** (Iv = 0 local, 1 remote). Some methods are **native** and must run on the device. The problem is **NP-hard**, so heuristics are used.
- **Static partitioning**: decided once, when the app launches. **Dynamic/adaptive partitioning**: re-decided at runtime as conditions change.
- **MAUI**: the programmer marks each method **"remoteable"** or not. Native methods cannot be remoteable. It saves energy and time.
- **COMET**: works on **unmodified applications** (no source code needed). Threads can migrate between machines depending on load.
- **CloneCloud**: clones the phone's apps and data onto the cloud and selectively runs operations there.
- **Cloudlet**: a **trusted, resource-rich computer or cluster, well connected to the Internet, close to mobile devices**. It is the **middle tier** of mobile device ↔ cloudlet ↔ cloud. A single-hop network gives **low latency** and **lower battery use** (Wi-Fi instead of cellular).

**MCC challenges** 📘: low bandwidth, service availability, heterogeneity, security and privacy (for users and for data on the cloud), context-aware services, QoS, standard interfaces.

**How MCC performance is judged** 📘: energy consumption, time to completion, monetary cost, and security.

---

# 6. VM migration

## 6.1 Basics 📘

**VM migration** = moving a **running application or VM** from one physical host to another. The **processor state, storage, memory and network connections** move too.

**Why migrate** 📘: **load balancing**, **maintenance** (move VMs off a server transparently), **power management** (consolidate VMs on fewer servers, put idle ones on low power), **QoS violations**, **fault tolerance** (move VMs away from a failing server).

## 6.2 Types 📘

| | **Cold / non-live** | **Hot / live** |
|---|---|---|
| During migration | The VM is **turned off or suspended** | The VM **keeps serving** users |
| Downtime | Long for big VMs | Short |
| Real-time apps | Not tolerable | Suitable |

Live migration has two main approaches: **pre-copy** and **post-copy**.

**Two metrics to minimise** 📘
- **Downtime**: the total time the service is **unavailable**.
- **Total migration time**: the time to move the VM from source to destination.

**Memory migration steps** 📘
- **Push**: the source VM keeps running and pages are pushed. Pages modified meanwhile must be **re-sent**.
- **Stop-and-copy**: the source VM is **stopped**, pages are copied, then the new VM starts.
- **Pull**: the new VM runs and, if it needs a page not yet copied, it is **faulted in (pulled)** from the source.

## 6.3 Pre-copy vs post-copy 📘

| | **Pre-copy** | **Post-copy** |
|---|---|---|
| Order | Copy **memory first** (iterative rounds), **then** switch the VM | Transfer **CPU state first**, **start the VM at the destination**, then fetch memory |
| Phases | Pre-copy rounds → termination → **stop-and-copy** | Stop → restart → **on-demand copy** (demand paging, active push, pre-paging) |
| Dirty pages | Pages modified during copying (**dirty pages**) are **resent** in later rounds | No resending of dirty pages. Memory is **empty** at restart |
| Weak point | Frequently changed pages are sent many times → **long total migration time** | A needed page not yet copied must be **pulled from the source** (page faults) |

**Pre-copy termination: stop when any one of these is true** 📘
1. The **number of rounds** exceeds a threshold.
2. The **total memory sent** exceeds a threshold.
3. The **number of dirty pages** in the previous round falls below a threshold.

> [!tip] In simple words
> **Pre-copy** = keep photocopying the book while the author is still editing it. You re-copy the edited pages until few changes remain, then pause the author briefly to copy the rest.
> **Post-copy** = move the author to the new office first, and bring the pages from the old office only when he asks for them.

## 6.4 Migration analysis (formulas from the slides) 📘

**Non-live migration of one VM**
```
T_mig  = Vm / R        (Vm = memory size of the VM, R = transmission rate)
T_down = T_mig         (the VM is suspended the whole time)
```

**Pre-copy (live) migration**
```
r      = (P × D) / R   (P = page size, D = dirtying rate, R = transmission rate)
T_mig  = (Vm / R) × (1 + r + r² + ... + rⁿ) + T_res
T_down = (Vm / R) × rⁿ + T_res
n      = min( ⌈ log_r (V_th / Vm) ⌉ , n_max )
```
(`V_th` = threshold to stop the rounds, `n_max` = maximum number of rounds, `T_res` = time to restart the VM at the destination.)

> [!warning] Exam traps
> - For **non-live migration, downtime equals total migration time**. For **live migration, downtime is much smaller than total migration time**.
> - Pre-copy gives **longer total migration time** but **short downtime**. It does **not** start the VM at the destination first (that is post-copy).

**Quick example (my own, for practice)**: VM memory 1024 MB, transmission rate 128 MB/s, non-live migration → T_mig = 1024 ÷ 128 = **8 s**, and downtime is also **8 s**.

## 6.5 Multiple VMs 📘
- **Serial migration**: VMs move one after another. While the first VM is in its stop-and-copy phase, the remaining VMs are **suspended** so they stop dirtying memory.
- **Parallel migration**: all **m** VMs start their pre-copy cycles **at the same time**, and each gets **R/m** of the bandwidth.

---

# 7. XML and web services

## 7.1 XML basics 📘

- **XML (eXtensible Markup Language)** = a text-based syntax for encoding data. It is **extensible** (you define your own tags), **self-describing** and a **universal format**. It separates **content from presentation**, was developed from **SGML**, and is backed by the **W3C**.
- Purpose in cloud and web services: **to structure and transport data for machine-to-machine communication.** It is **not** for displaying data to humans.

**XML vs HTML** 📘

| | **HTML** | **XML** |
|---|---|---|
| Describes | **How data is displayed** | **What the data is** (meaning/structure) |
| Tags | Predefined | **You define them** |
| Reading | Easy for humans, hard for machines to extract data | Readable by **both humans and machines** |

**Well-formed vs valid** 📘 (a top exam question)

| | **Well-formed** | **Valid** |
|---|---|---|
| Meaning | **Syntactically correct**: tags closed, properly nested, **one root element** | Well-formed **and** follows a **DTD or XML Schema** |
| Parser | The **minimum requirement** to "be XML". A parser **must stop** if the data isn't well-formed | Checked by a **validating** parser |

> [!tip] Memory trick
> **Valid ⊂ well-formed**. Every valid document is well-formed, but not every well-formed document is valid.

**DTD vs XML Schema** 📘

| | **DTD** (Document Type Definition) | **XML Schema** |
|---|---|---|
| Age | Part of the **core XML spec** (older) | **New spec (2001)** |
| Syntax | Special DTD grammar | **Pure XML** |
| Power | Weaker | **Stronger**: data types (integers, dates, numbers in a range) |

**XML namespaces** 📘: a way to separate names from different dialects so they don't clash (for example `<key/>` as a security key vs a database key). Uses the **`xmlns`** attribute. Lets you mix dialects in one document (like XHTML and MathML).

**Parser types** 📘
- **Validating parser**: must read all entities and process all DTD content, and stops with a failure if it can't.
- **Non-validating parser**: does not require that. Non-validating is always **faster**.

## 7.2 XML processing: SAX vs DOM 📘

| | **SAX** (Simple API for XML) | **DOM** (Document Object Model) |
|---|---|---|
| Model | **Event-based** (parser reports events and you attach event handlers) | **Tree-based**: builds a **full in-memory tree** |
| Memory | **Low**: doesn't read the whole document at once | **High** |
| Speed | **Very fast** | Slower |
| Good for | **Very large files and streaming data** | **Dynamic modification**, random access and complex queries |
| Weak point | **Can't modify the document structure** | Memory-hungry for huge files |

- **JDOM** and **dom4j** are Java tree-based interfaces. dom4j can do "mixed" SAX/DOM parsing.
- **XSLT** (eXtensible Stylesheet Language Transformations) = an XML language that **transforms XML into a new document with a different structure**, using a stylesheet.

> [!warning] Exam traps
> - SAX = **event-driven, minimal memory, read-only streaming**. DOM = **full tree in memory, allows modification**.
> - "DOM is best for very large streaming files" → false.
> - "A parser that builds the entire tree for random access and editing" = **DOM**.

## 7.3 Web services and SOA 📘

**Web service** = a software component identified by a **URI** whose interfaces can be defined, described and discovered as **XML artifacts** (W3C). It:
- communicates over open protocols (HTTP, SMTP),
- processes XML messages framed with **SOAP**,
- describes its messages with **XML Schema**,
- describes its endpoint with **WSDL**,
- can be discovered with **UDDI**.

**History** 📘: structured programming → object-oriented programming → distributed computing → **EDI** → World Wide Web → web services.

**EDI (Electronic Data Interchange)** 📘: computer-to-computer exchange of **business data between companies** in standard formats. Web services give similar abilities but are **simpler and cheaper**.

**Problems web services solve** 📘
- **Interoperability**: DCOM was tied to Windows and RMI to Java.
- **Firewall traversal**: CORBA and DCOM used non-standard ports. Web services use **HTTP (port 80)**, which firewalls usually allow.
- **Complexity**.

**SOA (Service-Oriented Architecture)** 📘: IBM's model with three entities

| Role | Job |
|---|---|
| **Service provider** | Owns the service and hosts access to it |
| **Service requestor** | Needs a function and looks for and invokes the service |
| **Service registry / broker** | Searchable registry where providers **publish** service descriptions (like the telephone **yellow pages**) |

**Three SOA operations** 📘: **Publish** (provider lists the service), **Find** (requestor searches the registry), **Bind** (requestor invokes the service at runtime).

**The four web service components** 📘

| Component | Full name | Job |
|---|---|---|
| **XML** | eXtensible Markup Language | Uniform **data format** |
| **SOAP** | Simple Object Access Protocol | **Message format** (an XML envelope) for communication |
| **WSDL** | Web Services Description Language | **Describes** the service: operations, messages, data types, location and protocol. It is the **contract / "user manual"** |
| **UDDI** | Universal Description, Discovery and Integration | **Registry** to register and locate services (**yellow pages**) |

**SOAP** 📘: XML-based, platform and language independent, mainly over **HTTP**, stateless and one-way. A SOAP message has an **Envelope (required)**, a **Header (optional)**, a **Body (required)**, and an optional **Fault** for errors. Three characteristics: **extensibility, neutrality (any transport: HTTP, SMTP, TCP) and independence**. It uses **WS-Security** and **HTTP over SSL** for security.

**WSDL structure** 📘: **types** (data types), **message** (messages used), **portType** (operations performed), **binding** (communication protocol).

**Steps of operation** 📘
1. The client asks the **UDDI registry** to locate a service.
2. The registry points the client to the **WSDL document**.
3. The client reads the **WSDL**.
4. The WSDL tells the client how to talk to the service.
5. The client sends a **SOAP request**.
6. The service returns a **SOAP response**.

> [!tip] In simple words
> **UDDI** = phone directory (find the shop). **WSDL** = the shop's menu and rules (what you can order and how). **SOAP** = the order slip you send. **XML** = the language everything is written in.

> [!warning] Exam traps
> - **WSDL** is the "user manual/contract". **UDDI** is the "yellow pages". **SOAP** is the message protocol. **XML** is the data format. Don't mix them.
> - SOA operations are **Publish, Find, Bind**.


