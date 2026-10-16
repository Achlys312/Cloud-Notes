**Models / NIST**
- 5 NIST: **On-demand, Broad access, Pooling, Elasticity, Measured**. "Zero downtime guaranteed" is not one.
- IaaS = VMs (EC2) · PaaS = platform (App Engine) · SaaS = app (Google Docs) · **XaaS = umbrella term**.
- Private (one org) · Community (shared concerns) · Public (open) · Hybrid (mix, bursting).
- Outsourced private: **two perimeters + link**, network dependency, multi-tenancy via software policies only.

**Virtualization**
- **Hypervisor (VMM)** creates VMs. Host OS = on hardware; Guest OS = inside the VM.
- **ESXi = Type 1 (bare metal)**, **VirtualBox = Type 2 (on host OS)**.
- **Full** (unmodified, emulate all) · **Para** (modified guest, **hypercalls**, Xen) · **Hardware-assisted** (Intel VT / AMD-V).
- Virtualization = both OSes **at once**; dual boot = **one at a time**.

**SLA**
- **SLA = contract, SLO = target, KPI = raw measurement.**
- Availability = (total − downtime) ÷ total; total = **hours/day × days**.
- 99% of 360 h → **3.6 h** allowed. Credit tiers: <99.95% → 10%, <99% → 25%.
- Multilevel SLA = **corporate + customer + service**.

**Docker / K8s**
- Dockerfile → **build** → image → **run** → container. Hub = **registry**. Compose = multi-container.
- Containers **share kernel**, light, fast; VMs have own OS, heavier, stronger isolation.
- Volumes **persist**. Default network = **bridge**. **Namespaces isolate, cgroups limit.**
- K8s = **container level**, **etcd stores state**, **scheduler picks node**, Pods run on worker nodes.

**Fog / Edge / Dew**
- Latency: **Edge < Fog < Cloud**. Fog/edge **complement** (not replace) cloud.
- Fog use cases: **connected vehicles, smart grid, smart traffic lights**.
- **Dew** = works **offline** on user's device, **independence + collaboration**, Dropbox.

**OpenStack**
- **Nova** compute · **Neutron** network · **Swift** object · **Cinder** block · **Keystone** identity · **Glance** images · **Horizon** dashboard · **Ceilometer** metering.
- **Swift ≠ block.** Nova Scheduler **chooses** host, Nova Compute **runs** VM.

**Azure / GCP**
- **App Service plan** = region + size + instances + SKU (not security). Premium = up to **20 slots**.
- Azure: **Managed Identity + Key Vault**, **HTTPS Only**, Availability Zones = separate locations.
- GCP: App Engine = PaaS, Compute Engine = IaaS, **Datastore ≠ object storage (Cloud Storage is)**.
- **Spanner** (global SQL) · **Bigtable** (IoT time-series) · **Firestore** (NoSQL docs) · **BigQuery** (analytics) · **Cloud SQL** (MySQL).
- **GKE** = managed Kubernetes · **Cloud Run** = serverless containers.
- `gcloud app deploy` deploys · `gcloud app browse` opens the app (**doesn't start the local server**) · `dev_appserver.py` = local server.

**IoT / sensor / CPS**
- IoT = **Things + Gateway + Network/Cloud**. Gateway bridges device protocols to a standard format.
- **Virtual sensor** = software copy of a physical sensor. **Derived** = built from **multiple, different** physical sensors.
- Sensor-cloud proxy = interface to the cloud. Sensor-network proxy = connects sensors with no direct cloud link.
- **CPS** = computing + physical processes with feedback loops. **CPCC** = CPS built from cloud sensor, processing, control and data services.

**Security**
- **I-I-M-F → A-C-I-A**: Interruption (availability), Interception (**confidentiality**), Modification (integrity), Fabrication (authenticity).
- **Passive** = eavesdrop, traffic analysis (hard to detect). **Active** = masquerade, replay, modification, DoS.
- Goals: **Prevention, Detection, Recovery**.
- **Gartner 7**: Privileged access, Regulatory compliance and audit, Data location, Data segregation, Recovery (RPO/RTO), Investigative support, Long-term viability.
- **Co-residence**: Placement then Extraction; check with **matching Dom0 IP**; Dom0 = privileged Xen VM. Compromised hypervisor = control **all VMs on the host**.
- **SoD violation** = one user does a critical task alone using permissions from several domains. **Cyclic inheritance** = cycle of roles across domains gives unauthorised permissions. **IDRM** = minimal role set.
- Broker: **fuzzy inference** (QoS + trust → suitability). **Fuzzification** = crisp → fuzzy sets.

**Serverless**
- **FaaS** (functions, event-driven, pay per run) vs **BaaS** (ready-made backend like Firebase).
- Lambda, Cloud Functions, Azure Functions. Almost stateless, ephemeral, event-triggered.
- Challenges: async calls, function chains (double cost), too many libraries (warm-up), too many functions.

**Green / sustainable**
- DC power: **IT 45%, cooling 40%, distribution 15%**. Idle server ≈ **66%** of peak.
- **Workload consolidation** = fewest servers, switch off idle ones. Power-aware scheduling packs VMs (485 W vs 552 W).
- VM image smaller: boot 38 s → 8 s, 4 GB → 635 MB.
- **PUE = total facility power ÷ IT power**.
- Sustainable cloud: renewable energy, ATS, thermal-aware scheduling, capacity planning, waste heat.

**Mobile cloud**
- Components: **Profiler, Solver, Synchronizer**.
- **Offload when C is large, D is small, B is high, F is large.**
- MAUI (annotate "remoteable"), COMET (unmodified apps), **Cloudlet** = middle tier, single hop, low latency.

**VM migration**
- Cold (suspended) vs **live** (keeps running). **Pre-copy** = copy memory in rounds, resend dirty pages, then stop-and-copy. **Post-copy** = CPU state first, start at destination, pull pages on demand.
- Non-live: **T_mig = Vm/R** and **T_down = T_mig**.
- Pre-copy stops when: rounds exceed limit / memory sent exceeds limit / dirty pages fall below threshold.

**XML / web services**
- XML = **structure and transport data for machines**. HTML = display.
- **Well-formed** = syntax OK, **one root**, tags closed and nested. **Valid** = well-formed **+** follows DTD/Schema.
- **SAX** = event-based, low memory, large files. **DOM** = tree in memory, can modify.
- **SOA**: provider, requestor, registry; **Publish, Find, Bind**.
- **XML** data · **SOAP** message · **WSDL** description (user manual) · **UDDI** registry (yellow pages).


**MapReduce / data**
- **Map** → key-value pairs, sorted, written to **local** disk. **Reduce** → fetches, **groups by key**, aggregates, writes to **GFS**. One **master**.
- Fault tolerance: **heartbeats**, re-run tasks (mapper results are on local disk, so a failed mapper is re-executed).
- **Divide the documents** (not the words) → every read is useful → efficient and scalable.
- **Average**: pass **(sum, count)** and divide at the end. **HDFS blocks**: 64 KB → 1, 65 MB → 2, 127 MB → 2 = **5**.
- **GFS = HDFS**: Master = Name Node, Chunk server = Data node, **64 MB** chunks, **3 replicas**. Read: client → master (metadata) → chunk server.
- **BigTable** = Google, column-oriented, on GFS, tablets + SSTables. **Dynamo** = Amazon, key-value, ring of virtual nodes, **R + W > N**, availability first.
- Parallel DB: **shared memory / shared nothing / shared disk**.

**Federation**
- Coupling: **loose** (little control) → **partial** (contract, affinity rules) → **tight** (same admin, exact VM placement).
- Architectures: **Hybrid/Bursting**, **Broker** (most common), **Aggregated**, **Multitier** (root cloud OS, tightly coupled).

**Geospatial**
- GIS = capture, store, query, analyse, display. **5 components**: hardware, software, procedures, data, people.
- Challenges: data/compute intensive, variable load, reliability, web services, **heterogeneity**. **SDI** = coordinated spatial infrastructure.
- Geo-cloud: eGIS instances with **Resource, Data and Interface services**; web services are the key technology; PaaS gives transparent scaling.

**Resource management**
- Provisioning (provider → customer) · allocation (among competitors) · mapping · adaptation · discovery · **brokering (agent negotiation)** · estimation · modelling · scheduling.
- Fog/edge classes: **Architectures, Infrastructure, Algorithms** (discovery, benchmarking, load balancing, placement).
- Placement constraints: resource, network, application. Objectives: latency, utilisation, cost, energy.

**Economics**
- **Cloud cheaper when P/A > U** (U = C/B). **CV = σ/|μ|**, aggregating n demands → **CV/√n**.
- Penalty ∝ ∫|D − R|dt. Flat = 0, linear = periodic provisioning OK, **exponential = keeps growing**.
- Effective cost = **raw ÷ efficiency**, then add power and management.

**5G**
- 1G analog voice · 2G digital voice · 3G mobile data · 4G mobile broadband.
- **eMBB** (VR/AR, video) · **mMTC** (massive IoT) · **URLLC** (cars, grid, remote patient care). NFC is not a category.
- 5G is "cloudified" (NFV, SDN) and uses edge/fog to cut latency.

**Grid / cluster / utility**
- **Distributed** = mother of the things (message passing, fault tolerance, no SPOF).
- **Grid** = loosely coupled, many institutions, idle cycles, virtual supercomputer. **Cluster** = tightly coupled, one place, one resource.
- **Utility** = metered pay-per-use concept. **Cloud implements it.**

**From Week 1**
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

**From Week 12 case studies**
- **Traj-Cloud**: **TS1 indexing** (BigQuery + Cloud SQL), **TS2 map-matching** (Compute Engine, MapReduce-based), **TS3 query** (Compute Engine + Cloud SQL).
- **IoHT**: simulated in **iFogSim**, **Raspberry Pi 3** = fog, **AWS** = cloud, **KNN** for activity detection. Fog gives **fixed low latency, low network usage, lower cost**.
- **Dew** column: **optimal** on-premise use, **local** connectivity, **moderate** storage.