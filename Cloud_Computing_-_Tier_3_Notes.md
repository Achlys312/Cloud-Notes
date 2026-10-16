---
title: Cloud Computing - Tier 3 Notes
tags: [cloud-computing, exam, tier-3, nptel]
course: Cloud Computing (NPTEL, IIT Kharagpur, Prof. Soumya K. Ghosh)
exam-format: MCQ
---

# ☁️ Cloud Computing - Tier 3 Notes

> [!abstract] How to use this file
> Tier 3 topics get fewer questions each, but several of them are **quick marks**, especially the calculation topics (economics, HDFS blocks, MapReduce average).
>
> Each topic has: **slide notes**, **in simple words**, and **exam traps**.
>
> **Label guide**
> - 📘 = taken from the Week slides.
> - 📌 = **not on the slides**, but the previous papers/mocks ask it, or it is standard knowledge. Learn it as a one-line fact.
>
> Read [[Cloud_Computing_-_Tier_1_Notes]] and [[Cloud_Computing_-_Tier_2_Notes]] first. Cloud brokers are covered in Tier 2 (Section 2.6), and the green cloud material is also in Tier 2.

**Topics**
- [ ] [[#1. MapReduce, HDFS/GFS and cloud data storage]]
- [ ] [[#2. Cloud federation]]
- [ ] [[#3. Geospatial and spatial cloud]]
- [ ] [[#4. Resource management]]
- [ ] [[#5. Cloud economics]]
- [ ] [[#6. 5G and cloud]]
- [ ] [[#7. Distributed, grid, cluster and utility computing]]

> [!tip] If you are short on time
> Do **5 (economics)**, **1.1 to 1.3 (MapReduce, HDFS blocks)** and **7 (grid vs cluster vs utility)** first. They are the easiest marks in Tier 3.

---

# 1. MapReduce, HDFS/GFS and cloud data storage

## 1.1 MapReduce 📘

**MapReduce** = a parallel programming model developed at **Google**.
- **Purpose**: large-scale search and text processing on massively scalable web data stored in **BigTable and GFS**.
- Built for **massively parallel** computation (tens of thousands of processors) and is **fault tolerant**: progress continues even if processors and networks fail.
- **Hadoop** is the open-source example.

**The model**
- Two phases: **Map** and **Reduce**.
- A configurable number of **M mappers** and **R reducers**, coordinated by a **single master** process.

| Phase | What happens |
|---|---|
| **Map** | Each mapper reads about **1/M of the input** from the global file system (locations given by the master). It transforms one set of **key-value pairs** into another. It writes **one file per reducer**, **sorted by key**, to its **local** file system. The master keeps track of where these files are |
| **Reduce** | The master tells reducers where the partial results are. Reducers fetch the files with **remote procedure calls**, **group results by key**, and apply a function `f` to the list of values for each key. Final results are written back to the **GFS** |

📌 **Combiner** (optional, a mini-reducer on the mapper side that cuts network traffic) and **partitioner** (decides which reducer gets which key) are standard MapReduce parts that are **not on the slides**.

> [!tip] In simple words
> Counting words in a huge library. **Map**: many helpers each take some books and write "word, 1" for every word. **Shuffle/sort**: all slips for the same word go to the same person. **Reduce**: that person adds the slips up.

**Fault tolerance** 📘
- The master and workers exchange **heartbeat** messages.
- If a worker communicates but **makes no progress**, the master **duplicates that task** and gives it to a processor that has already finished its own work.
- If a **mapper fails**, the master **reassigns its key range to another node to re-run it**. Re-execution is needed because the mapper's partial results are on its **local files, not in GFS**.

**Applications** 📘
- **Indexing** documents: map emits `(word, document-id)`, and reduce builds `(word, list of documents)`.
- **Relational operations**: joins and group-by on large data sets.

## 1.2 Parallel efficiency 📘

- A task taking time **T** on one processor **should** take **T/p** on p processors.
- Losses come from **synchronisation**, **message-passing overhead** and **imbalance** in the work.
- 📌 Parallel efficiency = T₁ ÷ (p × T_p). It is 1 when the speedup is perfect.
- A **scalable** implementation keeps efficiency **constant as the data size and the processor count grow together**.

**Word-count illustration** 📘 (it is the reason MapReduce splits by documents)

| Approach | Efficiency |
|---|---|
| **Divide the words** among processors | **Poor**. Each processor reads many documents but only uses a few words, so there is a lot of **wasted reading** |
| **Divide the documents** among processors | **Good**. **Every read is useful**. Efficiency stays constant as n and p grow, and tends to 1 for a fixed p and growing n. **This matches MapReduce** |

> [!warning] Exam traps
> - "Dividing the words is more efficient, and MapReduce does this" → false.
> - MapReduce's goal is to **keep efficiency high as data and processors grow together** (not to minimise processors, and not to remove fault tolerance).
> - The **Reducer** *aggregates the intermediate key-value pairs* from the mappers into the final result. It does not split input data (that is the framework) and it does not run the user function on raw chunks (that is the Mapper).

## 1.3 MapReduce practice problems 📘

**Problem 1: HDFS blocks.** Block size 64 MB. Files of **64 KB, 65 MB and 127 MB**. How many blocks?
- 64 KB → **1** block (a small file still takes one block and uses only its own size)
- 65 MB → **2** blocks (64 MB + 1 MB)
- 127 MB → **2** blocks (64 MB + 63 MB)
- **Total = 5 blocks.**

**Problem 2: Average of a set of integers.** A = (10, 20, 30, 40, 50).
- **Map** emits partial `(sum, count)` pairs, for example `(key, (10,1))`, `(key, (20,1))`...
- **Reduce** adds all the sums and all the counts and divides: 150 ÷ 5 = **30**.
- **Why not average the mappers' local averages?** The local averages may be based on **different numbers of elements**, so you must pass the **sum and count** and divide at the end.

**Problem 3 and 4** (salary by gender; word-length categories): the pattern is always the same. **Map** emits `(group-key, value)` (for example `(M, 10000)` or `(tiny, 1)`), and **Reduce** sums or averages the values for each key.

## 1.4 Google File System (GFS) and HDFS 📘

- **GFS** manages **large files** over a very large cluster of **commodity servers** on a fast network.
- It **handles failures even during reads and writes**. With N components, P(system failure) = 1 − (1 − p)ᴺ → close to 1 for large N, so fault tolerance is a must.
- Supports **parallel reads, writes and appends** by many clients.
- **HDFS** is the open-source counterpart.

| Concept | GFS name | HDFS name |
|---|---|---|
| Single controller (namespace, metadata) | **Master** | **Name Node** |
| Pieces of a file | **Chunks** | **Blocks** |
| Servers storing the pieces | **Chunk servers** | **Data nodes** |

- Typical chunk/block size: **64 MB**.
- Each chunk is **replicated three times**, on different **racks** and **network segments**.

**Read operation** 📘
1. The client sends the **full path and offset** to the master/Name Node.
2. The master returns the **metadata** for one replica of the chunk.
3. The client **caches the metadata**.
4. The client **reads directly from the chunk server**.

**Write/append operation** 📘
1. The client sends the file path to the master.
2. The master returns metadata for **all replicas** of the chunk.
3. The client sends the data to **all chunk servers**, and they acknowledge.
4. The master designates one chunk server as the **primary**.
5. The primary appends the data at an **offset it chooses**. 📌 It then tells the other replicas to append at the same offset.

**Fault tolerance** 📘: the master and chunk servers exchange **heartbeat** messages. On a failure the metadata is updated, and if the **primary fails the master assigns a new primary**. Clients refresh their metadata and retry.

> [!tip] In simple words
> The master is the **librarian** who only knows where each part of every book is kept. The chunk servers are the **shelves**. You ask the librarian once, then walk straight to the shelf.

> [!warning] Exam traps
> - GFS/HDFS key feature = **breaking files into large chunks and replicating them** (not small encrypted blocks, not a single central server for all data).
> - "GFS prioritises immediate consistency over availability" → false.
> - Data does **not** flow through the master. The master only hands out metadata.

## 1.5 BigTable 📘

- A distributed **structured storage** system **built on GFS**.
- A **sparse, persistent, multi-dimensional sorted map** of key-value pairs.
- Accessed by **row key + column key + timestamp**.
- **Column families** are fixed when the table is created, and labels inside a family can be added any time. Each cell can store **multiple versions**, newest first.
- Each table is split into row ranges called **tablets**, managed by **tablet servers**. Each column family of a tablet is stored in separate files called **SSTables**. A **metadata table** (managed by a metadata server) locates the tablets.
- It is **column-oriented**, so it suits **analytics and sparse data**. A traditional relational database is typically **row-oriented**.

## 1.6 Dynamo 📘

- Developed by **Amazon**. Built for a **large volume of concurrent small updates** (BigTable is about bulk reads and writes).
- Data model: a simple **key-value pair**, well suited to e-commerce. It does **not depend on a distributed file system** like GFS/HDFS.
- Keys are hashed with **MD5 (128-bit)**. The hash range is mapped to **virtual nodes arranged in a ring**. An object is stored at its primary virtual node and replicated at **N−1 more**.
- **Quorum protocol** gives **eventual consistency**. A read touches **R** replicas and a write touches **W** replicas. If **R + W > N** the system is **quorum consistent**.
  - To make **writes cheap**, read more replicas. To make **reads cheap**, write more replicas.
- **Versioning** uses vector timestamps. Conflicting versions are kept and resolved by the application.
- 📌 In CAP terms Dynamo favours **availability and partition tolerance** over immediate consistency, so it is good for "always-on" services.

## 1.7 Datastore (Google App Engine) 📘

- Google App Engine **Datastore** and Amazon **SimpleDB** are simple **transactional key-value** stores.
- All entities live in **one BigTable table** and it does **not** use column-oriented storage.
- Indexes: **single-property** (automatic), **kind** (automatic) and **composite** (configurable). The query uses the index with the **highest selectivity**.
- Entities can be **grouped** for transactions and stored close together.

## 1.8 Relational and parallel databases 📘

- **Relational DB**: default data store since the 1980s, accessed with **SQL**, efficient for **transaction processing**.
- **Parallel DB architectures**

| Architecture | Meaning |
|---|---|
| **Shared memory** | Multiple CPUs share one memory address space (SMP) |
| **Shared nothing** | A cluster of independent servers, **each with its own disk**, connected by a network |
| **Shared disk** | Hybrid: independent server clusters **share storage** over a high-speed network |
- **Advantages over a plain relational DB**: SQL runs on multiple processors, tables are partitioned across nodes, distributed joins and **two-phase commit**, fault tolerance with stand-by systems. Examples: Oracle, DB2, SQL Server, Netezza, Vertica, Teradata.

> [!warning] Exam traps
> - Dynamo = **Amazon**, key-value, **availability** first. BigTable = **Google**, column-oriented, built **on GFS**.
> - "Bigtable is row-oriented while relational databases are column-oriented" → **false** (it is the reverse).
> - "Bigtable uses SQL while relational databases use NoSQL" → false.

---

# 2. Cloud federation

## 2.1 What it is 📘

- **Cloud federation** = the deployment and management of **multiple external and internal cloud services** to match business needs. A federation is the union of several smaller parts that perform a common action.
- It is **collaboration between cloud service providers (CSPs)** to get: **capacity utilisation, interoperability, a catalogue of services, and insight about providers and SLAs**.

**Motivation** 📘: maximise **resource utilisation**, minimise **power consumption**, **load balancing**, **global utility**, and expand a CSP's global footprint.

**Characteristics** 📘
- Overcomes limits like **service interruptions, lack of interoperability and degraded service**.
- It is an **inter-cloud organisation with voluntary characteristics**.
- It should have **maximum geographical separation**.

## 2.2 Levels of coupling 📘

| | **Loosely coupled** | **Partially coupled** | **Tightly coupled** |
|---|---|---|---|
| Interoperation | **Limited** | Through a **contract or framework agreement** | **Same cloud administration** |
| Control over remote resources | **Little or none** (no say in VM placement) | **Some control**, for example **affinity rules** (keep VMs on the same cluster) | **Advanced control**, including the **exact placement** of a remote VM |
| Monitoring info | Limited (CPU, memory, disk of each VM) | Depends on the contract | **All** monitoring information |
| Example | A private cloud topping up from an external commercial cloud | Partner clouds under an agreement | Sites of one corporation |

## 2.3 Four federation architectures 📘

| Architecture | Idea | Coupling |
|---|---|---|
| **Hybrid / Bursting** | **On-premise (private) cloud + public cloud(s)** to get **extra capacity at peak demand**. The local cloud OS has no advanced control over resources in the external cloud | Loosely coupled |
| **Broker** | One **broker** serves users and has access to **several public clouds**. A simple broker deploys resources where the user chooses. An **advanced broker** schedules on **cost, performance or energy**. **The most common scenario** | Loosely coupled |
| **Aggregated** | **Two or more partner clouds interoperate and pool their resources** into a larger virtual infrastructure | Usually **partially coupled** |
| **Multitier** | **Two or more cloud sites**, each with its **own cloud OS** and usually in the **same corporation**, managed by a **third (root) cloud OS** in a hierarchy. The root has **full control** and shows the sites as if they were one | **Tightly coupled** |

> [!note] Slide quirk
> The picture caption on the slide says "(d) **Multiplier**", but the text calls it **Multitier**. Use **Multitier**.

> [!tip] In simple words
> - **Bursting** = your own kitchen is full, so you borrow a neighbour's kitchen for the party.
> - **Broker** = a travel agent who books you across several hotels.
> - **Aggregated** = two friends pool their kitchens into one bigger kitchen.
> - **Multitier** = a head office running several branches.

> [!warning] Exam traps
> - Hybrid/bursting = **loosely coupled**, multitier = **tightly coupled**.
> - **Brokering is the most common** federation scenario.
> - 📌 For an intelligent broker (provider selection with fuzzy inference), see [[Cloud_Computing_-_Tier_2_Notes]] (Section 2.6).

---

# 3. Geospatial and spatial cloud

## 3.1 Geospatial information and GIS 📘

- **Geospatial data** describes objects, events or features with a **location on or near the earth's surface**. It combines **location** (coordinates), **attribute** information and **temporal** information.
- **Data sources**: social surveys, natural surveys (such as Survey of India maps), **remote sensing** (air photos, satellite imagery), reporting networks (weather stations), **field data collection** (GPS).
- **GIS (Geographic Information System)** = a computer system for **capturing, storing, querying, analysing and displaying** geospatial data.
- **Five components of a GIS**: **hardware, software, data management and analysis procedures, spatial data, and people**.

**GIS challenges** 📘
- **Data intensive** and **computation intensive**.
- **Variable load** on the GIS server, so it needs **dynamic scaling in and out**.
- Needs **high reliability and performance**.
- Uses **network-intensive web services**.
- **Heterogeneity**: GIS layers are built by different departments on different systems. The fixes are **homogeneous data description, standard data encoding and a standard sharing mechanism**.

**SDI (Spatial Data Infrastructure)** 📘: the coordinated policy and infrastructure that provides a basis for **spatial data discovery, evaluation and application** for governments, business, academia and citizens.

## 3.2 Why a geospatial cloud 📘

- **Huge volumes** of data and metadata.
- Need for **services and service orchestration**, and **evolving standards and policies**.
- Organisations can **share spatial data** and use others' spatial services.
- **Less infrastructure and spatial web-service expertise** is needed, and a spatial service image is **easy to port to multiple VMs**.
- **Shared resource pooling**, a **choice of deployment, service and business models**, and **managed services** that prevent loss from outages.

**Geospatial cloud architecture** 📘
- The cloud acts as a **service provider** with a collection of **enterprise GIS (eGIS) instances**, and three kinds of service:
  - **Resource service**: resource allocation, VM and network properties, monitoring.
  - **Data service**: persistent user and system data.
  - **Interface service**: user-facing interfaces, authentication and management tools.
- **Web services are the key technology.** Data from **heterogeneous back-end data services** (inside or outside the cloud) is integrated. Data services inside the cloud can run on **PaaS**, which makes **load balancing, replicas and dynamic scaling transparent**.

## 3.3 Spatial cloud 📘

- **Spatial analysis** tries to solve **location-oriented problems**. It goes **beyond mapping** by studying the characteristics of places and the relationships between them.
- Cloud gives an **elastic, on-demand platform** for spatial analytics.
- **Advantages**: easy to use, **scalability**, **cost** based on usage, **reliability**, and low risk (can change instantly, even the OS).
- 📌 **Real-time mobility analytics** benefit: **dynamic traffic-signal optimisation based on live vehicle density**.

> [!warning] Exam traps
> - GIS components are **five** (hardware, software, procedures, data, people).
> - Real-time mobility analytics does **not** eliminate traffic laws or prevent all accidents.

---

# 4. Resource management

## 4.1 Basics 📘

**Resource management** = the operations used to control how the capabilities of cloud resources and services are made available to users, applications and services **efficiently**.

- **Resource types**: **physical** (computers, disks, databases, networks, scientific instruments) and **logical** (execution, monitoring, communication).
- It is one of the **major challenges in IaaS** (VMs, block storage, firewalls, load balancers, network devices).

**Objectives** 📘: scalability, **QoS**, optimal utility, reduced overheads, improved throughput, reduced latency, specialised environment, **cost effectiveness**, simplified interface.

**Challenges** 📘: *hardware* (CPU, memory, storage, workstations, network elements, sensors/actuators) and *logical* (OS, **energy**, network bandwidth, **load balancing**, security, delays, APIs, protocols).

**Performance metrics** 📘: **reliability, ease of deployment, QoS, delay, control overhead**.

## 4.2 Resource management aspects 📘

| Aspect | Meaning |
|---|---|
| **Provisioning** | Allocating a **service provider's resources to a customer** |
| **Allocation** | Distributing resources **economically among competing** groups or programs |
| **Mapping (requirement mapping)** | Matching the resources **required by users** to those **available with the provider** |
| **Adaptation** | The system's ability to **adjust resources dynamically** to meet user requirements |
| **Discovery and selection** | Finding the list of **authenticated resources** available for job submission and picking the best |
| **Brokering** | **Negotiating resources through an agent** so they are available at the right time |
| **Estimation** | A close guess of the resources an application needs |
| **Modeling** | Predicting resource requirements for later time intervals |
| **Scheduling** | A timetable of events and resources (**when** an activity should run) |

**Example approaches from the slides** 📘: provisioning → **Nash equilibrium (game theory)** and a **network queuing model**; allocation → **market-oriented** allocation; mapping → **symmetric mapping pattern**; adaptation → **reinforcement learning**.

## 4.3 Resource management in cloud-fog-edge 📘

Three-way classification (a favourite question):

| Group | What it covers |
|---|---|
| **Architectures** | Classified by **data flow** (direction of workloads/data), **control** (single/central vs distributed) and **tenancy** |
| **Infrastructure** | **Hardware** (gateways, Wi-Fi access points, set-top boxes, small home servers, edge ISP servers, cars, even drones), **system software**, and **middleware** (performance monitoring, coordination and orchestration, communication) |
| **Algorithms** | **Discovery, benchmarking, load balancing, placement** |

**Service/application placement problem** 📘
- **Mapping application components and links onto the infrastructure graph** (devices and links).
- **Constraints**: **resource** (CPU, RAM, storage, bandwidth), **network** (latency, bandwidth) and **application** (such as locality requirements).
- **Objectives**: **latency, resource utilisation, cost, energy**.
- **Offloading** = moving a server, application and its data to the **edge of the network**, for example from a user device to an edge node (usually **one hop** away).
- **Control** can be **centralised** or **distributed**.

> [!warning] Exam traps
> - Fog/edge resource management is classified by **architectures, infrastructure and algorithms** (not by cost, speed and security).
> - **Provisioning** = provider resources to a customer. **Allocation** = sharing among competitors. Don't swap them.
> - **Resource brokering** = negotiation through an **intermediary agent**.

---

# 5. Cloud economics

## 5.1 Cloud properties from an economic view 📘

1. **Common infrastructure**: pooled, standardised resources, with benefits from **statistical multiplexing**.
2. **Location independence**: available everywhere, with benefits from **latency reduction** and better user experience.
3. **Online connectivity**: the enabler of the other properties.
4. **Utility pricing**: **pay-per-use**, useful when **demand varies**.
5. **On-demand resources**: **scalable, elastic** resources provisioned and released **without delay or cost**.

## 5.2 Value of common infrastructure 📘

- **Economies of scale**: reduced overhead costs, **buyer power** from volume purchasing. 📌 Economies of scale = cost per unit **falls** as the scale grows.
- **Statistics of scale** (statistical multiplexing): mixing many demands gives **higher utilisation** and **lower cost per delivered resource**.
- Real world: if demands are **independent**, **mid-size providers get nearly the same statistical economies as a huge one**. If demands are correlated, they don't.

**Coefficient of Variation (CV)** 📘: a measure of how "smooth" demand is.

```
CV = σ / |μ|        (standard deviation ÷ absolute value of the mean)
```
- **Smoother** demand = **lower CV** (large mean for a given σ, or small σ for a given mean).
- A facility with fixed assets serving **highly variable** demand gets **low utilisation**.
- **Adding n independent demands** (same σ, same μ): mean = n·μ, variance = n·σ², so
```
CV(aggregate) = (σ·√n) / (n·μ) = CV / √n
```
  → CV falls by **√n**. **Aggregating 100 workloads brings the penalty down to 10%.**

> [!tip] In simple words
> One shop with random customers has bursty demand. Merge 100 such shops into one warehouse and the ups and downs cancel out, so demand is smoother and the warehouse stays busy.

## 5.3 Value of location independence 📘
- Applications and content now **come to us** over networks.
- **Latency depends strongly on distance** (light in fibre covers only about 124 miles per millisecond).
- A global user base needs a **dispersed service architecture**, which brings issues of **coordination, consistency, availability and partition tolerance**.

## 5.4 Value of utility pricing (rent vs own) 📘

```
D(t)  = demand at time t          P = peak demand = max D(t)
A     = average demand            B = baseline (owned) unit cost
C     = cloud unit cost           U = utility premium = C / B

Baseline (own)  total cost:  B_T = P × B × T      (you build for the peak)
Cloud (rent)    total cost:  C_T = U × B × A × T  (you pay only for what you use)

Cloud is cheaper when  C_T < B_T   →   U < P / A    (equivalently P/A > U)
```

- Car analogy from the slides: leasing = ₹10,000 a day, renting = ₹45,000 a day, so **U = 4.5**. If you need a car for only 2 days of a long period, renting is far cheaper, because **P/A** is high.
- Real demand is often **spiky** (promotions, flash crowds, tax season), so a **hybrid** works best: **own the baseline, rent for spikes**.
- 📌 Example from a mock: P/A = 5, U = 3 → 5 > 3 → **cloud is cheaper**.

> [!warning] Exam traps
> - The condition is **P/A > U**. Not "P/A < U", not "P × A = U", not "P + A = U".
> - A cloud that is more expensive **per unit** can still be cheaper **overall** if P/A is large.
> - Utility pricing says a cloud service doesn't need to be cheaper per unit to be economical.

## 5.5 Value of on-demand services (penalty cost) 📘

When you own resources, you pay a **penalty** whenever resources don't match demand: either you **pay for unused resources** or you **lose service**.

```
Penalty  ∝  ∫ | D(t) − R(t) | dt
```

| Demand pattern | Result |
|---|---|
| **Flat** | Penalty = **0** |
| **Linear** | **Periodic provisioning is acceptable** |
| **Exponential** (D = eᵗ) | Any fixed provisioning delay `tp` makes resources **fall exponentially behind**: D − R = eᵗ(1 − e^(−tp)) = k₁eᵗ, so the **penalty ∝ k₁eᵗ**, which keeps growing |

**Assignment 1 (practice)**: R(t) = D(t) + δ·dD/dt, where δ is the **provisioning delay**. The penalty is the area between D(t) and R(t), multiplied by the cost of a unit resource per unit time (0.9 in the slide).

## 5.6 Effective cost per hour (IaaS comparison) 📌

A frequently asked calculation, from the Week 5 assignment and the mocks:

```
Raw hourly cost   = purchase cost ÷ total hours
Effective cost    = raw cost ÷ efficiency
In-house total    = effective cost + power + management

Example: ₹/$ 600,000 over 3 years      → 3 × 365 × 24 = 26,280 h → 22.83 per hour
         efficiency 40%                → 22.83 ÷ 0.4 = 57.08 per effective hour
         + power 22 + management 6     → 85.08 per hour    (in-house)
Cloud:   42 per hour at 80% efficiency → 42 ÷ 0.8 = 52.50
         + management 1                → 53.50 per hour    (cloud)
```
Cloud is cheaper at 40% in-house efficiency. 📌 One mock asks at what efficiency the in-house server would break even with the cloud, and the answer key says about **90%**.

> [!warning] Exam trap
> Don't forget to divide by **efficiency** before adding power and management.

## 5.7 Where else cloud economics shows up 📘
- Why private data centres are built for **peak load**, so average use is low (5 to 20%).
- IaaS, PaaS and SaaS benefits (no hardware purchase, auto-scaling, subscription instead of licences).
- Uses of cloud in organisations: backup, CRM/ERP, development and testing, traffic spikes, data analysis.

---

# 6. 5G and cloud

## 6.1 5G basics 📘

- **5G** = the **5th generation mobile network**, a new global wireless standard after 1G, 2G, 3G and 4G, designed to connect people, machines, objects and devices.
- Delivers **multi-Gbps peak data rates, ultra-low latency, high reliability, massive network capacity** and better availability.

| Generation | Decade | What it brought |
|---|---|---|
| **1G** | 1980s | **Analog voice** |
| **2G** | early 1990s | **Digital voice** (CDMA) |
| **3G** | early 2000s | **Mobile data** |
| **4G LTE** | 2010s | **Mobile broadband** |
| **5G** | now | More speed, lower latency, massive connectivity |

**The three 5G service categories** 📘 (a very likely MCQ)

| Category | Full name | Typical uses |
|---|---|---|
| **eMBB** | Enhanced Mobile Broadband | Fast broadband, **VR/AR**, high-resolution video, enterprise collaboration |
| **mMTC** | Massive Machine-Type Communications | **IoT**, asset tracking, smart agriculture, smart cities, energy monitoring |
| **URLLC** | Ultra-Reliable Low-Latency Communications | **Autonomous vehicles, smart grids, remote patient monitoring** |

> [!tip] Memory trick
> **e**MBB = **e**ntertainment (video, VR). **m**MTC = **m**any things (IoT). **U**RLLC = **u**rgent (cars, surgery, grid).

## 6.2 5G and cloud 📘

- 5G is the **perfect companion to cloud computing**. Edge and on-premise data centres close the gap between low-latency devices and distant clouds, leading to **heterogeneous and distributed** architectures.
- **Two aspects**:
  1. Cloud computing must **meet 5G needs**, shown by the growing role of **edge, mobile edge and fog** computing.
  2. 5G itself is being **"cloudified"** through **network softwarisation, NFV and SDN**.
- **Edge computing in 5G**: brings cloud capability **near the users** to cut latency. 5G must handle **massive data** from devices and IoT, **strict QoS** for interactive apps, and **heterogeneous** equipment.
- **Applications**: healthcare, entertainment and multimedia, **VR/AR/mixed reality**, **tactile internet**, IoT, factories of the future, emergency response, intelligent transportation.
- **5G and MCC**: sharing resources for mobile applications, improved reliability (data is backed up in the cloud), and fewer device resources used because processing is offloaded.

> [!warning] Exam traps
> - Multimedia/AR delivery to mobile users → **eMBB**. **NFC is not a 5G service category.**
> - mMTC = massive **IoT**. URLLC = **critical, low-latency** uses.
> - Fog and edge **extend** the cloud for 5G. They don't replace it.

---

# 7. Distributed, grid, cluster and utility computing

## 7.1 Distributed computing 📘

- **Centralised** computing = a single processor. A **distributed system** = several **autonomous computing entities**, each with its **own local memory**, that **communicate by message passing**.
- Examples: the **Internet**, ATMs, intranets.
- **Common properties**: **fault tolerance** (system still works if nodes fail), **resource sharing**, **load sharing**. Each node has only a limited, partial view of the system.
- **Why distributed**: **performance** (compute-intensive or data-intensive tasks) and **robustness** (**no single point of failure, SPOF**).
- Application styles: **client-server** (resource management centralised at the server) and **peer-to-peer** (truly distributed).
- 📌 Distributed computing is called the **"mother of the things"** for cloud, because it gives the building blocks like **fault tolerance, resource sharing and scalability**.

## 7.2 Grid computing 📘

- **Grid computing** harnesses the **unused processing cycles** of computers in a network to solve problems too big for a single machine.
- **IBM's view**: it **virtualises distributed computing and data resources** (processing, bandwidth, storage) to create a **single system image**.
- **Power grid analogy**: you plug into a socket and don't care where the electricity is generated. In a grid, users get computing resources without knowing where they are.
- **Use**: sharing more than information (data, computing power, applications) across **many institutions** as a **virtual organisation**; efficient use of resources; transparent access.
- 📌 **Loosely coupled** and **geographically dispersed**, like a single virtual supercomputer.

**Five types of grid** 📘

| Type | What it offers |
|---|---|
| **Computational grid** | Secure access to a huge pool of **processing power** for high-throughput, compute-heavy work |
| **Data grid** | Storage, discovery, handling and publication of **large volumes of data** across heterogeneous databases |
| **Collaboration grid** | Better **collaboration** between people and groups |
| **Network grid** | **Fault-tolerant, high-performance communication**. Each node acts as a data router with caching |
| **Utility grid** | The ultimate form: **software and special equipment** (any resource) is shared |

## 7.3 Cluster computing 📘

- A **cluster** = a collection of **interconnected standalone computers** working together as **one integrated computing resource**.
- Components: multiple standalone computers (PCs, workstations or SMPs), operating systems, **high-performance interconnects**, middleware, parallel programming environments and applications.
- Used to improve **speed and/or reliability**, more **cost effectively** than one big computer. The network is **faster and closer** than a typical LAN, with **low-latency protocols**.
- **Three types**: **High-availability (failover)**, **load-balancing**, **parallel/distributed-processing** clusters.
- **Benefits**: system availability (redundancy), hardware fault tolerance, OS and application reliability, scalability (add servers or clusters).
- 📌 Cluster = **tightly coupled** machines in one place, aimed at **high performance and availability**.

## 7.4 Utility computing 📘

- **Utility computing** is **purely a concept** that **cloud computing practically implements**.
- A service model where the provider makes computing resources and infrastructure management available **as needed** and charges for **specific usage rather than a flat rate**.
- **Low or no initial cost**: resources are essentially **rented**. The word "utility" is an analogy to gas, electricity, water and telecom.
- **Payment models**: **flat rate, tiered, subscription, metered, pay-as-you-go, standing charges**.

## 7.5 Comparing them (a classic question)

| | **Distributed** | **Grid** | **Cluster** | **Utility** | **Cloud** |
|---|---|---|---|---|---|
| Core idea | Independent nodes cooperating by message passing | **Virtual supercomputer** from dispersed resources and **unused cycles** | Standalone computers acting as **one resource** | **Metered, pay-per-use** model | **Implements** utility computing with virtualization |
| Coupling | Varies | **Loosely coupled** | **Tightly coupled** | Not applicable (a business model) | Virtualized, elastic |
| Location | Any | **Many institutions**, geographically spread | **Usually one site** | Any | Provider data centres |
| Main goal | Fault tolerance, resource sharing | Share and harness idle resources | High performance and availability | Pay only for use | On-demand, elastic services |

> [!warning] Exam traps
> - "**Cluster** is loosely coupled and grid is tightly coupled" → **false**. Cluster = **tightly coupled, high performance and availability**. Grid = **loosely coupled, virtualising resources from many locations**.
> - The paradigm that introduced **metered pay-per-use** (not a flat rate) = **Utility computing**.
> - The paradigm that laid the groundwork for NIST's "rapidly provisioned and released" on-demand access = **Utility computing**.
> - The paradigm that taps **underutilised compute cycles** and treats dispersed resources as **a single virtual supercomputer** = **Grid**.
> - The "**mother of the things**" for cloud = **Distributed computing**.

---

# ✅ One-page cheat sheet (read this last)


