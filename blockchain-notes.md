
# Blockchain and its Applications: Lecture Notes

---

# Week 1

## Lecture 1: Introduction, Myths, Decentralization

### Myths about blockchain

**Myth 1: Blockchain = Bitcoin / cryptocurrency**
- Wrong. Bitcoin (cryptocurrency) is an **application**. Blockchain is the **technology** used to build it.
- Analogy: Bitcoin is the electrical equipment, blockchain is the electricity powering it.
- Blockchain has many applications that have nothing to do with cryptocurrency.

**Myth 2: Blockchain can solve every problem**
- Wrong. Blockchain has advantages and limitations, like any technology.
- Before using it, check the **trade-off** (pros vs cons). A better technology may exist for your problem.

**Myth 3: Blockchain = Distributed database**
- Wrong. Blockchain is **not** a distributed database. It is a replicated data structure.
- You cannot store everything on it, and storing large files is a bad use case.
- Databases and blockchains each have their own use cases.

### Decentralization

**Use case: petroleum supply chain (India)**
- Flow: crude purchase → crude storage → refinery → products (petrol, diesel) → retailers.
- **Upstream** players: exploration and production of crude oil (ONGC, OVL, Oil India).
- **Downstream** players: refining and marketing (Indian Oil, BPCL, HPCL, Reliance).
- Many other industry bodies are involved, some government and some private.

**The problem**
- Every company wants to maximize its **own profit**, so they are competitors.
- But for the supply chain to work well, they need **strong coordination** (for example, sharing demand and stock information).
- There is **no central coordinator**.

**Why a simple web portal fails**
1. Who will manage the portal?
2. Who validates that the submitted information is correct?
3. What if someone later **denies** they submitted the information?

**Decentralization (definition):** A network of different players (businesses, government bodies, private bodies, individuals), each with their own interest, who **do not trust each other** but still want to reach a common goal.

**Key idea:** Blockchain gives **trustless decentralization**. The players do not trust each other, but they can still coordinate.

---

## Lecture 2: Blockchain Idea and Formal Definition

### The "Blackboard" idea
Imagine a blackboard where all stakeholders write down everything that happens in the supply chain.

**Properties of this blackboard:**
1. **Infinite space**: nothing is ever erased, so all historical data stays.
2. **Everyone can see it**: this gives transparency and verification.
3. **Changes are visible to everyone**: if you made a mistake, you cannot erase it. You add a correction, and everyone can see it.
4. **Not erasable**: once written, it stays. Nobody can later **deny** what they wrote, because each entry carries their signature.

**Advantages:**
- **One-step auditing**: a simple computer program can check for discrepancies (e.g., 100 barrels produced, only 60 transported, so 40 are missing).
- **Matchmaking**: a company can easily find who has extra petrol or who sells cheaper.

### Problem: who maintains the board?
- One central entity (government, a cloud provider like Amazon, or one company) is a bad option:
  - If it fails or is attacked, everything is lost (single point of failure).
  - Competitors cannot trust one of their own to maintain it.
- **Decentralization improves security.** If 100 sources hold the same data and we go by majority, an attacker must compromise at least **51** of them instead of just one.
- "No free lunch": decentralization also has overhead, which is covered later.

### Solution: everyone keeps their own copy
- Every organization keeps its **own copy** of the board.
- New problem: how do we make sure every copy has the **same** information? This is the **distributed consensus problem** (covered later).

### Blockchain definition
> **Blockchain** is an **immutable, append-only, ever-growing chain of data**. Data once added cannot be deleted or modified later.

- **Immutable**: no one can change it.
- **Append-only**: you can only add new data, not erase.
- **Ever-growing**: new blocks keep getting added.
- New information is added as a **block**, and the same block is appended to **every** local copy. A chain of blocks gives the name **blockchain**.

### Formal definition (important for the exam)
> **Blockchain is a decentralized, immutable, append-only, public ledger.**

| Keyword | Meaning |
|---|---|
| Decentralized | Everyone keeps their own copy, with no central owner |
| Immutable | Existing data cannot be changed |
| Append-only | You can only add new data |
| Public | Everyone can see and verify the information |

---

## Lecture 3: Cryptographic Hash Functions (Part 1)

### Why study this?
Hash functions are used to connect blocks in a chain in a **tamper-proof** way. Digital signatures (covered later) are also a core building block.

### Definition
> A **cryptographic hash function** takes an input of **any size** (message *M*) and produces a **fixed-size output** called the **message digest**, written H(M).

- In blockchain the digest is usually **256 bits**.
- It must be **very fast** to compute.

### Properties of cryptographic hash functions

1. **Deterministic**: the same message always gives the same digest. There is no randomness.
2. **Collision-free**: two different messages should not give the same digest. If M1 ≠ M2, then H(M1) ≠ H(M2).
3. **Hiding (information hiding)**: even a tiny change in the message gives a completely different digest. From a digest you cannot work out the message, and knowing H(M1) does not help you predict H(M2).
4. **Puzzle friendliness**: see below.

Also: hash functions are **one-way**. Given x, finding H(x) is easy. Given H(x), finding x is practically impossible.

### Collision resistance and the Birthday Paradox
- "Difficult to find" a collision means it is not strictly impossible, but it would take far too long.
- **Birthday paradox**: with only 23 people the chance that two share a birthday is 0.5, and with 70 people it is 0.999. Collisions happen sooner than you expect.
- For a hash with **n-bit output**, an attacker needs about **2^(n/2)** hash operations to find a collision.
- For n = 256 that is **2^128** operations. Even at 1 microsecond per hash, it takes about **10^25 years**.
- So with a long enough digest (256 bits), finding two messages with the same hash is practically impossible.

### Hash as a message digest
- If H(x) = H(y), we safely assume x = y.
- So instead of storing or comparing long documents, we store or compare only their **short, fixed-length digests**. This is efficient.

### Hiding and commitment
- You can **commit** to a value by storing its hash.
- Later, if someone claims the original value was y, hash y and compare it with the stored hash. If it matches, the claim is verified. If not, it is false.

### Puzzle friendliness
> Given a message **x** and a desired output property **y**, it is hard to find a value **k** such that **H(x ‖ k) = y** (‖ means concatenation).

- y is usually not one exact value but a **set of acceptable values** (for example, a hash with certain properties).
- **Random searching** is the best strategy to solve the puzzle.
- Used in **mining** and **Proof of Work** (Bitcoin).

### Demo (from the lecture)
- Hash of "hello world" and hash of "hello world 1" are **completely different**, even though the input changed by only a tiny bit.
- SHA-256 output = **64 hexadecimal digits** = 256 bits (each hex digit = 4 bits).
- Other hash functions: MD5, SHA-1, SHA-512 (different output lengths).

---

## Lecture 4: SHA-256 and Patterns of Hashing

### SHA-256
- SHA = **Secure Hash Algorithm**. SHA-256 gives a **256-bit** message digest.
- It is used in **Bitcoin mining** and is central to Bitcoin's blockchain.
- It is part of a family of hash functions designed by the **US National Security Agency (NSA)**.
- The output is always 256 bits, no matter the input length.

### Steps of SHA-256

**Step 1: Preprocessing (padding)**
- The message length must become a **multiple of 512**.
- If the message length is *l*:
  1. Append bit **1** at the end.
  2. Append *k* zero bits, where *k* is the smallest non-negative solution of **l + 1 + k ≡ 448 (mod 512)**.
  3. Append a **64-bit block** that is the number *l* written in binary.
- The total length is now divisible by 512.

**Step 2: Split into blocks**
- Divide the padded message into *n* blocks of **512 bits**: M1, M2, ..., Mn.
- Each 512-bit block is split into **sixteen 32-bit sub-blocks**: M(i,0) to M(i,15).

**Step 3: Process sequentially**
- Start with a fixed initial hash value **H0** (the initialization vector).
- Compute: **Hi = C(Mi, Hi-1) + Hi-1**
  - **C** = the SHA-256 compression function.
  - **+** = addition modulo 2^32.
- Process the blocks one at a time: H0 → H1 → H2 → ... → Hn.
- **Hn is the hash of M.**

### Patterns of hashing data (two inputs: "Hello" and "World!")

| Pattern | What you do |
|---|---|
| **Independent** | Hash each message separately: H(Hello), H(World!) |
| **Repeated** | Hash the output again: H(H(Hello World)) |
| **Combined** | Concatenate the messages first, then hash: H(Hello ‖ World!) |
| **Sequential** | Hash the first message, join the digest with the second message, then hash: H(H(Hello) ‖ World!) |
| **Hierarchical** | Hash each message separately, join the two digests, then hash that: H( H(Hello) ‖ H(World!) ) |

**Important points:**
- Different ways of combining give **different final hashes**, and the order of combining also matters.
- **Hierarchical hashing** is the basis of the **Merkle tree**, which is covered in the next lecture.
- In the slides only the **first 8 hex digits** are shown for brevity. The real hash is always the full **256 bits**. In hierarchical hashing the two **full** 256-bit digests are joined to make a 512-bit input.

---

## Lecture 5: Hash Pointers, Hash Chain and Merkle Tree

### Recap of hash properties used here
- **One-way**: from H(M) = D you cannot get back M.
- **Collision-free**: if M1 ≠ M2 then D1 ≠ D2. So if D1 = D2, the messages are the same.

### Hash pointer
> A **cryptographic hash pointer** (also called a **hash reference**) is a **pointer to the location where information is stored**, together with a **hash of that information**.

**Uses:**
1. **Retrieve** the information (like any pointer).
2. **Check that the information has not been modified.** Go to the location, **recompute the hash** of the data and **match it with the stored hash**. If they match, the data was not tampered with.

- A hash pointer is like a **linked list**, but each pointer also carries a hash of the data it points to.
- Useful when data is stored once and **not modified later**, but you want to **detect any modification**. Blockchain is such an application.

### Tampering example
- Data "Hello World!" has a hash pointer storing H("Hello World!").
- If the data changes to "Hello World?", the new hash does not match the stored hash, so the pointer **breaks** and the tampering is **detected**.
- **Smart attacker**: changes the data **and also updates the stored hash** in the pointer. Then the mismatch is not detected.
- So we must make it **computationally hard** for the attacker to recompute the hashes.

### Analogy (locker token)
- You leave a bag in locker 5 and get a token saying "locker 5". A normal pointer only says where it is, so someone could swap your bag.
- If the token also says "red backpack", you can prove what you left. This is like **storing the hash along with the pointer**.

### Making tampering harder: nonce and restrictions
- **Nonce** = a number used only once.
- Instead of H(data), we find a nonce so that **H(data ‖ nonce)** satisfies a **restriction**, usually a number of **leading zeros** in the hash (in hexadecimal).
- This uses the **puzzle friendliness** property. You can only find the nonce by **trying values one by one**.

**Demo from the lecture (more leading zeros = more work):**

| Leading zeros required | Nonce found |
|---|---|
| 1 | 3 |
| 2 | 57 |
| 3 | 614 |
| 5 | 1006908 |

- Each extra leading zero makes the puzzle much harder.
- So an attacker who changes data must **redo this work** for the hash, which takes time and computing power.

### Hash chain
> A **hash chain** is a set of blocks connected by hash pointers. Each block stores the **hash of the previous block**.

- If an attacker changes data in one block, its hash changes, so the **next block's pointer breaks**.
- To hide the change, the attacker must **recompute the hash of every later block**, and each hash needs a valid nonce (leading zeros).
- The more blocks in the chain, the **more work** is needed. So tampering becomes **computationally very difficult**.

### Merkle tree
> A **Merkle tree** is a **binary tree of hash pointers**. Leaf nodes hold the hashes of data (transactions), and each parent holds the hash of its two children joined together.

**Example with 4 transactions T1, T2, T3, T4:**
1. Leaves: H(T1), H(T2), H(T3), H(T4).
2. Next level: H0 = H( H(T1) ‖ H(T2) ) and H1 = H( H(T3) ‖ H(T4) ).
3. Top: **Root hash = H( H0 ‖ H1 )**. This is the **Merkle root**.

- This is **hierarchical hashing** (from Lecture 4).
- If any transaction changes, every hash on the path up to the root changes.
- In blockchain, a Merkle tree is used to **store the transactions of a block**.

### Block and blockchain structure (preview)
- Each block has a **block header** containing:
  - the **hash of the previous block** (the hash pointer)
  - the **Merkle root**
  - a **nonce**
  - the hash of the block itself
- The block also holds the **transactions**.
- Blocks are linked by hash pointers.
> **A blockchain is a hash chain of blocks**, connected in a tamper-proof way.

---

## Quick Revision (Week 1)

- **Blockchain** = decentralized, immutable, append-only, public ledger.
- **Trustless decentralization** = players do not trust each other but still coordinate.
- **Hash function** = arbitrary-size input → fixed-size digest.
- **Hash properties**: deterministic, collision-free, hiding, puzzle friendly (plus one-way and fast to compute).
- **Collision attack on n-bit hash** ≈ 2^(n/2) operations (2^128 for SHA-256).
- **Puzzle**: find k such that H(x ‖ k) = y. This is the basis of mining.
- **SHA-256**: pad to a multiple of 512 bits → split into 512-bit blocks → H0 → ... → Hn.
- **Five hashing patterns**: independent, repeated, combined, sequential, hierarchical.
- **Hash pointer** = pointer to data + hash of the data. Recompute the hash and compare to detect tampering.
- **Nonce**: find a value so H(data ‖ nonce) has a set number of leading zeros. More zeros = harder.
- **Hash chain**: each block stores the previous block's hash, so changing one block breaks all later ones.
- **Merkle tree**: binary tree of hashes. Root hash = Merkle root, used to store a block's transactions.
- **Block header**: previous hash, Merkle root, nonce, own hash. **Blockchain = hash chain of blocks.**

---

# Week 2

## Lecture 6: Public Key Cryptography

### Basic terms
- **Cryptography**: sending a message securely from A to B over a channel that may not be secure (an intruder may read or change it).
- **Plain text**: the original message.
- **Cipher text**: the scrambled message that is actually sent.
- **Encryption**: converting plain text into cipher text.
- **Decryption**: converting cipher text back into plain text.
- **Key**: a parameter that decides the output of a cryptographic algorithm.
- Hash functions cannot be used for this, because even the receiver could not get the message back.

### Two types of cryptography

| | Symmetric key | Asymmetric key (Public key) |
|---|---|---|
| Keys | **Same key** for encryption and decryption | **Different keys**: one for encryption, another for decryption |
| Problem | How to share the key securely | Solves this problem |

### Properties of a good cryptographic key
1. **Random**: generated truly randomly so an attacker cannot guess it.
2. **Sufficient length**: otherwise brute force (trying every possibility) works.
3. **Sufficient entropy**: every bit of the key should be equally random.

### Public key and private key
- Every user has a **key pair**.
- **Private key**: known **only to the owner**.
- **Public key**: known to **everyone**.

### Sending a secret message (confidentiality)
Alice wants to send message M to Bob:
1. Alice encrypts M with **Bob's public key** → cipher text M'.
2. M' is sent over the unsecured link.
3. Bob decrypts M' with **his own private key** → gets M.

An adversary who sees M' cannot read it, because only Bob has the private key. Anyone (Alice, Tom) can send to Bob using Bob's public key.

### RSA algorithm
- Named after **Rivest, Shamir, Adleman**. It is one of the first public key algorithms.
- Four steps: **key generation → key distribution → encryption → decryption**.

**RSA key generation**
1. Choose two distinct large **random prime numbers** p and q.
2. Compute **n = p × q**. The length of n is the **key length**.
3. Compute **φ(n) = (p − 1) × (q − 1)** (Euler's totient function).
4. Choose e such that **1 < e < φ(n)** and **gcd(e, φ(n)) = 1** (e and φ(n) are co-prime).
5. Find d such that **d × e ≡ 1 (mod φ(n))** (d is the modular multiplicative inverse of e).

**Public key = (e, n). Private key = (d, n).**

### Important property
- Encrypt with the public key → decrypt with the private key. This gives confidentiality.
- Encrypt with the private key → decrypt with the public key. **This is used for digital signatures** (next lecture).

### Digital signature (intro)
> A **digital signature** is a digital code attached to an electronically sent document, used to **verify the content**, **authenticate the sender's identity** and **prevent non-repudiation** (the sender cannot deny sending it).

- Only the signer can sign, but **everyone can verify**.
- A signature is tied to **one document** and cannot be reused on another.

---

## Lecture 7: RSA Encryption/Decryption and Digital Signature

### RSA encryption and decryption
- Plain text M is converted to an integer m.
- **Encryption**: **C = m^e mod n** (using the public key (e, n)).
- **Decryption**: **m = C^d mod n** (using the private key (d, n)).
- Why it works: (m^e)^d ≡ m (mod n).

### Worked example (from Stallings)
- p = 17, q = 11
- n = 17 × 11 = **187**
- φ(n) = 16 × 10 = **160**
- Choose **e = 7** (co-prime with 160)
- d = **23**, because 23 × 7 = 161 ≡ 1 (mod 160)
- **Public key = (7, 187)**, **Private key = (23, 187)**
- Plain text m = 88
- Encryption: C = 88^7 mod 187 = **11**
- Decryption: 11^23 mod 187 = **88**

In practice, libraries and online tools generate key pairs (for example, 1024-bit keys). You do not do this by hand.

### Digital signature using public key cryptography

**Simple form**
1. Alice **encrypts the message with her private key** (this is signing).
2. Bob **decrypts it with Alice's public key**.
3. If the result matches the message, it must have come from Alice, because only her private key could have produced it.

**Better form (using a hash)**: this makes the signature small.
1. Alice computes the digest **H(M)**.
2. Alice encrypts the digest with her private key → **signature S**.
3. Alice sends **M and S** to Bob.
4. Bob decrypts S with Alice's public key → gets a digest.
5. Bob computes H(M) himself on the received M.
6. **If both digests match, the signature is valid.**

### Use of digital signatures in blockchain
- They **validate the origin of a transaction**.
- They give **non-repudiation**: Alice cannot deny her own transactions.
- No one else (e.g., Carol) can claim Alice's transaction, because the signature can only be verified with Alice's public key.
- Example: Alice creates 10 coins and signs the transaction. Then Alice sends 5 coins to Bob and signs that transaction too.
- **Bitcoin uses ECDSA**, which is based on **elliptic curve cryptography**.

### Summary of the two main cryptographic tools
1. **Cryptographic hash functions**
2. **Digital signatures**

---

## Lecture 8: History of Blockchain and Distributed Consensus

### Background
- Blockchain became popular around 2014-15, but its ideas are old (**1970s-80s**, from distributed systems research).
- **Three pillars of blockchain**:
  1. Distributed systems
  2. Cryptographic techniques
  3. Economic models (mainly useful for cryptocurrencies)

### Distributed consensus problem
> When one node proposes something (e.g., a new block), **all other nodes must collectively agree** on it. This is the **distributed consensus problem**.

- In blockchain, the peers are the participating organizations (refinery, distributor, retailer, and so on).
- Once consensus is done, everyone holds the **same copy** of the data.

### Example: burger or pizza
- **Centralized way**: one friend acts as leader, collects choices and announces the result. You must **trust** the leader.
- **Distributed way**: everyone calls everyone else and shares their choice. Each person counts the majority. **No leader is needed.**
- **Trade-off**: centralized needs about 6 calls, while distributed needs 4 × 3 = **12 calls**. Distributed costs more messages but needs no trust.

### Byzantine behavior
- A node that tells **different information to different people** (e.g., "pizza" to one friend, "burger" to another) shows **Byzantine behavior**.

### Types of communication
- **Synchronous**: messages arrive in real time (like a phone call).
- **Asynchronous**: there is **no bound on message delay** (like an SMS). The internet is mostly asynchronous.

### Types of faults
- **Crash fault**: a node stops responding because of a hardware or software failure. It is easier to handle.
- **Byzantine fault**: a node responds but gives **wrong or inconsistent information**. It is harder to handle.

### Safety and liveness
- **Safety**: correct processes produce the **correct output**.
- **Liveness**: the output is produced in a **finite amount of time** (the algorithm eventually terminates).

### FLP Impossibility Theorem (1985)
> By **Fischer, Lynch and Patterson**: consensus is **impossible in a fully asynchronous system, even with a single crash fault**.

- It means **safety and liveness cannot both be guaranteed together**.
- Classical systems give **priority to safety over liveness**.

### Timeline

| Year | Event |
|---|---|
| 1985 | FLP impossibility theorem |
| 1989 | **Paxos** proposed by **Leslie Lamport** (supports safety, not liveness) |
| 1998 | Paxos finally accepted and published (ACM Transactions on Computer Systems) |
| 2001 | FLP paper wins the Dijkstra Prize |
| 2009 | **ZooKeeper** released |
| 2010 onwards | MultiPaxos, Raft, **PBFT** (Byzantine fault tolerance) |

- Paxos and PBFT will be studied in detail later.
- Open question: can these classical algorithms be used for blockchain? (Answered in Lecture 10.)

---

## Lecture 9: Cryptocurrency History

### Problems with physical currency
1. **Management**: notes can get torn, and exchanging them is a hassle.
2. **Theft**: notes can be stolen (pickpocketing).

This led to the idea of **digital money**.

### Three requirements for a cryptocurrency
1. **Third parties cannot determine the payee, the time or the amount** of payments (privacy).
2. **Proof of payment**: you can prove you paid (like a cash memo).
3. **Ability to stop the use of payment media reported stolen.**

### eCash (1983)
- Invented by **David Chaum**.
- Money is stored on the computer and is **digitally signed by the bank**.
- It uses a **blind signature** to make payments anonymous.

**Blind signature (carbon paper analogy)**
- A professor wants to send a letter to NPTEL with proof that he is from IIT Kharagpur, but without the director seeing the content or the receiver.
- He puts carbon paper on the letter and writes his credentials on it. The director signs the carbon paper, and the signature goes through to the letter.
- The director **verified the credential but never saw the message**.
- So the signer **verifies the person but does not see the content, receiver or amount**.

**Why eCash failed**
- Every payment needed an **interaction with the bank** (to get a blind signature), so the overhead was higher than physical cash.
- Chaum's company **DigiCash went bankrupt around 1998**.

### Move to full decentralization
- New idea: **remove the bank and government completely**. People transact directly, with no third party watching.
- Attraction: it is untraceable and free from government control (but this raises legal and tax debates).

### b-money and Bit Gold (1998)
- **b-money**: by **Wei Dai**, an anonymous distributed electronic cash system.
- **Bit Gold**: by **Nick Szabo**. It used **cryptographic puzzles**, but puzzle verification still needed **some central involvement**, so it was not fully decentralized.
- Open question: can puzzle solving be verified in a **fully distributed** way?

### Double spending
> **Double spending** means using the same money more than once.

- Example: you have ₹100, and you send ₹60 to A and ₹80 to B. Both cannot be valid.
- A **consensus mechanism** is needed so the community can detect this by checking transaction history.
- Next question: can classical consensus algorithms be used here?

---

## Lecture 10: Bitcoin and Proof of Work

### Open network
- In an **open network**, **anyone can join** and no central authority exists.
- This is a problem for classical consensus, because it uses **message passing** and needs the **identity of all participants**.
- So classical algorithms work **only in closed systems**.

### Bitcoin paper (2008)
- Title: **"Bitcoin: A Peer-to-Peer Electronic Cash System"**.
- Author: **Satoshi Nakamoto**.
- It showed how to reach consensus in an open network **without message passing**.

### Idea: elect a leader by puzzle solving
- The network gives everyone a **hard puzzle**.
- **The first person to solve it becomes the leader** for that round, and the leader's decision (the next set of valid transactions) is accepted.
- Different people win in different rounds.

### Properties of a good puzzle
1. **Difficult to solve**, so that only one person (usually) solves it first.
2. **Easy to verify**, so everyone can quickly check the answer.

### Puzzle using hash functions
- Puzzle: given **x** and **y**, find a **nonce N** such that **y = H(x ‖ N)**.
- There is no shortcut, so you must try different nonces (**random search**). This is hard.
- Verification is easy: compute H(x ‖ N) once and compare.

### Proof of Work (PoW)
> **Proof of Work** is the consensus algorithm where a participant does hard computational work to solve a puzzle, and the solution acts as **proof** that the work was done.

- Also called **Nakamoto consensus**.
- The idea of puzzle solving as proof first came from **Bit Gold**. Bitcoin formalized it and added **coin mining** in an open peer-to-peer network.

### Safety vs Liveness in Bitcoin
- Classical algorithms: priority to **safety**.
- **PoW (Nakamoto consensus): priority to liveness.**
- Result: **no immediate finality**. A transaction may be accepted now but is not final until later.
- Reason: more than one person may solve the puzzle at the same time, so the network cannot decide immediately which transaction to keep (for example, the ₹60 vs ₹80 double spend). This gets resolved over later rounds.

### Timeline
| Year | Event |
|---|---|
| 2008 | Bitcoin white paper (the term "blockchain" was **not** used; it said "block" and "chain" separately) |
| 2011 | **Litecoin** |
| 2015 | **Ethereum** goes live (supports decentralized applications, or **DApps**) |
| 2016 | Term **"blockchain"** becomes popular |

### Open question for next lecture
- Why would anyone spend computing power to solve the puzzle? (Incentives.)

---

## Quick Revision (Week 2)

- **Symmetric key**: the same key encrypts and decrypts. **Asymmetric key**: a public key and a private key.
- **Confidentiality**: encrypt with the receiver's **public key**, decrypt with the receiver's **private key**.
- **Digital signature**: sign with your **private key**, verify with your **public key**.
- **RSA**: n = p × q, φ(n) = (p − 1)(q − 1), d × e ≡ 1 (mod φ(n)). Public key (e, n), private key (d, n). C = m^e mod n, m = C^d mod n.
- **Signing with a hash**: S = Encrypt(H(M), private key). Bob compares the decrypted S with H(M).
- **Bitcoin signature scheme**: ECDSA.
- **FLP**: consensus is impossible in a fully asynchronous system with even one crash fault (safety and liveness cannot both hold).
- **Paxos** (Lamport): safety over liveness. **Faults**: crash and Byzantine.
- **eCash** (1983, Chaum): blind signature, failed due to bank overhead. **b-money** (Wei Dai) and **Bit Gold** (Szabo) were 1998 ideas.
- **Double spending**: spending the same money twice.
- **PoW puzzle**: find nonce N so that H(x ‖ N) = y. Hard to solve, easy to verify.
- **PoW** gives priority to **liveness**, with no immediate finality.

---

# Week 3

## Lecture 11: Bitcoin Mining and Incentives

### Bitcoin mining
- The open consensus method used in Bitcoin (puzzle solving) is called **mining**.
- **Miners** are special nodes in the Bitcoin network. Anyone can be a miner, with no registration (just run the miner software).
- **Task of a miner**: collect the transactions floating in the network, combine them into a **block** and propose it for the blockchain.

### How the winning block is chosen
- Many miners build **different blocks**, but only **one** block can be added.
- The network gives a **hard puzzle**: find a nonce so that the hash meets the target (y = H(x ‖ n), where x and y are given and n must be found).
- There is no shortcut, so miners keep **retrying randomly** and spend computing power.
- The **first miner to solve it** gets their block added. The nonce they found is the **proof** attached to the block.
- Other nodes **easily verify** the proof, so the block is valid.
- Different miners win in different rounds, so **no single miner controls the blockchain**.
- This is called **Proof of Work**: the solution is proof that real work was done.

### Incentive: why would anyone mine?
- Solving the puzzle costs a lot of computing power, so there must be a reward.
- **A miner who successfully adds a block gets new bitcoins as a reward.**
- This is also how **new bitcoins enter the system**. It is like a government minting new money, which is why it is called **mining**.
- The Bitcoin network acts like a **reserve bank without any explicit governance**: it controls the flow of money and creates new currency over time.

### Three pillars of blockchain
1. **Distributed systems** (distributed consensus)
2. **Cryptographic techniques** (hash chain, puzzles, signatures)
3. **Economic model** (mining reward, controlled coin supply)

Satoshi Nakamoto did not invent entirely new things. He or she **combined existing ideas** from different domains. The identity of Satoshi Nakamoto is unknown.

### Legal debate
- Bitcoin transactions cannot be easily tracked, so some governments do not allow it.

### Blockchain 1.0: Distributed Ledger Technology (DLT)
> A **ledger** is where transactions are logged. Bitcoin's is a **distributed public ledger**: anyone can see and verify it.

### Bitcoin facts and timeline

| When | Event |
|---|---|
| 3 Jan 2009 | Nakamoto mined the first block, the **Genesis block** |
| May 2010 | 1 BTC ≈ $0.01 |
| 2013 | Coinbase reported selling about $1 million of Bitcoin |
| Apr 2014 | 1 BTC ≈ $340 to $530 |
| Dec 2017 | 1 BTC ≈ $13,800 |
| After 2018 | Popularity dropped because of the legal debate, then rose again |

- Other cryptocurrencies followed: **Litecoin, Ethereum**, and more.
- Ethereum grew fast around 2018 because of **DApps (decentralized applications)**.

### Beyond financial transactions
- Idea: instead of logging only financial transactions, **submit executable code as a transaction**.
- Because the platform is distributed and runs consensus, the **code execution itself is agreed upon by everyone**.
- This gives rise to **smart contracts** (next lecture).

---

## Lecture 12: Smart Contracts and Permissioned Blockchain

### Smart contract
> A **smart contract** is a contract or code that is **executed automatically** over a **decentralized platform**.

### Problems with the traditional way (centralized cloud)
- Two parties agree on a contract and run it on a cloud platform. Problems:
  1. How do you check that the **inputs are valid**?
  2. A user can later **deny** submitting an input, or claim someone **impersonated** them.
  3. You must **trust the third party** (the cloud). An attacker on the cloud could change the computation.

### Example code (lecture)
- `pay(sender, receiver, amount)`: if the sender has less than the amount → return −1 (failure). Otherwise deduct from the sender, add to the receiver, return 1 (success).
- `deliverGoods(count, pricePerCount)`: calls pay. If payment succeeds, schedule the logistics and return 1. Otherwise return 0.

### How decentralized execution works
- Any code can be seen as a **state machine**. After each step the **state** changes (e.g., sender balance, receiver balance, count).
- The **state of execution is stored on the blockchain**, so everyone knows how far the code ran and where it continues.
- The contract is submitted to the blockchain instead of a central server. Other nodes **monitor and verify** the execution.
- This solves the three problems above.
- Examples: **Ethereum DApps**, **Hyperledger Fabric**, and the game **CryptoKitties** (game state kept on blockchain, no central game server).

### Blockchain generations

| Version | What it is |
|---|---|
| **Blockchain 1.0** | Distributed ledger technology (cryptocurrency, financial transactions) |
| **Blockchain 2.0** | **Smart contracts** (code execution on blockchain) |
| **Blockchain 3.0** | **Trustless decentralization** for enterprise (permissioned blockchain) |

### Problem with Proof of Work for enterprises
- PoW works in an open network, but has **high transaction latency** and **low throughput**.
- Bitcoin takes about **10 minutes per block**. Ethereum takes a few seconds to a few minutes.
- Enterprise applications (like supply chain) need **real-time logging**, **high throughput** and **low latency**. Delays can allow fraud.

### Permissioned blockchain
- Many enterprise applications **do not need an open network**. The participants are limited and known.
- Examples: food supply chain (a consortium of distributors and suppliers), **KYC**, **trade financing** (a network of banks).
- Since the network is closed, we can go back to **classical consensus algorithms** (low latency, high throughput).
- Instead of "proof of mining", we can use **witness cosigning**: digital signatures from all participants agreeing on the block.

> **Trustless decentralization**: a closed network where organizations **know each other but do not trust each other** (they are competitors) and still transact and run smart contracts together.

| | Permissionless | Permissioned |
|---|---|---|
| Network | Open, anyone can join | Closed, known participants |
| Participants | Unknown | **Pre-authenticated and pre-authorized**, but can still behave maliciously |
| Consensus | Proof of Work (Nakamoto) | Classical consensus + digital signatures |
| Speed | Slow | Fast, low latency |
| Example | Bitcoin | Enterprise blockchains (e.g., Hyperledger Fabric) |

---

## Lecture 13: Blockchain Elements 1 (Block Structure and Header)

### Blockchain
- A platform for executing **transactional services** (e.g., Alice sends 5 bitcoins to Bob, or a vehicle title is transferred).
- An **append-only shared ledger of digitally signed and encrypted transactions**, **replicated across a network of peer nodes**.
- It can span organizations and individuals who **need not trust each other**.
- Peers verify transactions. Security comes from the cryptographic techniques studied earlier.

### Block structure
> A **block** is a container data structure with two parts: **block header** and **list of transactions**.

- Blocks are linked using **hash pointers**: each block's header holds the hash of the previous block.
- **Size**: a Bitcoin block is about **1 MB** (set by Satoshi Nakamoto), holding roughly 500 to 1000+ transactions.
- **Larger blocks (e.g., 8 MB)**: more transactions per block, but longer verification and propagation time, so higher latency.

### Block header contains
1. **Previous block hash**
2. **Merkle root** (of the block's transactions)
3. **Timestamp**
4. **Difficulty bits** (the target)
5. **Nonce**
6. **Version**

The **block hash** is the hash of this header. It is the block's identifier.

### Why it is tamper-proof
- Changing one transaction in an old block (say block 600,000) changes the **Merkle root** → changes that **block's hash** → the next block's "previous hash" no longer matches.
- The attacker must **recompute the hash of every later block** (e.g., all blocks up to 700,000), and each one needs a nonce with the required leading zeros.
- This is computationally very hard unless the attacker has huge computing power.

### Mining a block
> **Mining** is generating the hash of a block (using the previous hash, timestamp, Merkle root, difficulty bits, version, and a nonce) so that the hash satisfies the required **number of leading zeros**.

- The **block generation puzzle** is to find the **nonce**.

### Difficulty bits (target)
- "bits" is an 8-hex-digit value, e.g. `0x170e2632`.
  - **First byte** = **index** (0x17 = 23).
  - **Next three bytes** = **coefficient** (0e2632).
- **Target = coefficient × 2^(8 × (index − 3))**
- Written as a 64-hex-digit (256-bit) number, the target decides how many **leading zeros** the block hash needs.
- A block's hash must meet or beat this requirement. In the lecture's example the real block hash had more leading zeros than the minimum required.
- The difficulty **changes over time** (explained later).

### Verification demo
- Using a block hash verification tool, enter **version, Merkle root, bits, timestamp, nonce, previous block hash** → it computes the block hash, which matches the real block.
- **Verifying is easy; finding the nonce is the hard part.**
- Block explorers: **btc.com** and **blockchain.com**.

---

## Lecture 14: Block Generation Cost, Transactions, Scripts (Intro)

### Cost of block generation
- Finding the nonce is **computationally expensive** (many leading zeros needed).
- It needs special hardware called **ASICs** (application-specific integrated circuits), which are expensive.
- Only the **first miner** to solve the puzzle gets the **block reward**, so the work of all others is **wasted**.
- The total **hash rate** of the Bitcoin network is huge (about 150 million tera-hashes per second in the lecture).
- It uses a very large amount of electricity (the lecture compared it to powering around 20,000 households; figures vary because no one knows the exact value).
- Individuals cannot compete, so miners form **mining pools** (e.g., F2Pool, AntPool, Binance Pool) that combine their resources.
- **Security assumption**: the **majority of computing power** must be in the hands of **honest nodes**.

### Peer nodes
- Each node keeps a **full local copy** of the blockchain (about 350 GB at the time).
- All copies must stay **consistent** with the latest mined block.

### Transactions in a block
- Transactions are organized as a **Merkle tree**. The Merkle root goes into the block header.
- Each transaction has its own **hash**.

### Inputs and outputs
- A transaction has **inputs** and **outputs**.
- Example: Alice has 100 BTC (the input) and pays Bob 40 BTC. Alice keeps the remaining 60 as **change** in the same transaction.
- Each recipient can later spend their coins in the same way (Bob spends 30 of his 40, and so on).

### Proving ownership
- Alice **signs** the transaction with her **private key** and sends her **public key**. Bob verifies it using Alice's public key (digital signature).
- Bob must prove later that he truly owns the 40 bitcoins before spending them.
- In Bitcoin this is done with **scripts**.

### Scripts
- **scriptPubKey**: used by the sender (Alice) to **lock** the payment to Bob (the **output**).
- **scriptSig**: used by the receiver (Bob) to **unlock and claim** it (the **input** of his next transaction).
- Bob can spend the coins **only if both scripts together execute to TRUE**.

**Bitcoin script language:**
- Simple, compact, **stack-based**, processed **left to right** (similar to the Forth language).
- **Not Turing complete**: **no loops**, so the script always terminates. This avoids coins getting stuck because a script never ends.

### Pay to Public Key Hash (P2PKH)
- Bob gives Alice the **hash of his public key**, not the public key itself.
- Alice pays to that **public key hash**.
- Later Bob provides his **public key** (which must hash to that address) and a **signature** proving he owns the matching private key.

### Summary
- Block generation is very costly, with a lot of wasted energy. This is the cost of **proof of work**.
- Transactions are included in blocks, and scripts are used to make and claim payments.

---

## Lecture 15: Bitcoin Scripts in Detail

### Input vs output
- **Transaction output** (Alice → Bob, 40 BTC): uses **scriptPubKey**.
- **Transaction input** (Bob claims and spends, e.g., pays 30 BTC to Carol): uses **scriptSig**.
- Alice also had to claim her own 100 BTC the same way earlier.

### Why a public key hash?
- A public key can be linked to a person, so paying to the **hash of the public key** keeps the payment more **anonymous**.

### Script P2PKH
**scriptSig:** `<sig> <pubKey>`
**scriptPubKey:** `OP_DUP OP_HASH160 <pubKeyHash> OP_EQUALVERIFY OP_CHECKSIG`

Both are combined (scriptSig first, then scriptPubKey) and run on an **empty stack**.

| Step | Operation | What happens |
|---|---|---|
| 1 | `<sig>` | Push sig onto the stack |
| 2 | `<pubKey>` | Push Bob's public key |
| 3 | `OP_DUP` | **Duplicate** the top item (pubKey) |
| 4 | `OP_HASH160` | **Hash** the top item (pubKey → pubKeyHash computed) |
| 5 | `<pubKeyHash>` | Push the hash Alice used in her payment |
| 6 | `OP_EQUALVERIFY` | Check the **top two items are equal**. If not equal, the script **fails**. If equal, pop both |
| 7 | `OP_CHECKSIG` | **Verify the signature** using the public key. If valid, result is TRUE |

### What each check proves
- **OP_EQUALVERIFY**: the public key Bob gave hashes to the **same hash Alice paid to**, so the payment was meant for Bob.
- **OP_CHECKSIG**: Bob really holds the **private key** for that public key (he signed with it). So he is not an impersonator.
- Together: Alice paid Bob's key hash, and Bob proved ownership, so **Bob is the right person to claim the coins**.
- This uses **hash functions** and **digital signatures** from the earlier lectures.

### Real example
- A transaction in a real block (viewed on btc.com) showed **P2PKH** inputs and two outputs with the same script pattern (OP_DUP, OP_HASH160, pubKeyHash, OP_EQUALVERIFY, OP_CHECKSIG).

### Types of operations (op codes)
- Arithmetic
- If/then conditions
- Logical operators
- Data handling (e.g., OP_DUP)
- Cryptographic (hash functions, signature verification)
- **Multi-signature** verification (more than one party must sign, e.g., Alice and Bob together)

### Other interesting scripts
- **Anyone can spend**: the unlocking script is simply `OP_TRUE`, so anyone can claim the funds.
- **OP_RETURN**: stops further processing of the script.
- **Time lock (freezing funds)**: uses **OP_CHECKLOCKTIMEVERIFY**. The funds cannot be claimed until a set future time (e.g., 15 Nov 2021). If the current time is before that, the script returns **false**.
- A good online resource lists many such scripts.

### Next lecture
- How blocks are tied together, how nodes receive blocks, how blocks propagate, and how miners generate blocks.

---

## Quick Revision (Week 3)

- **Miner**: collects transactions, builds a block, solves the puzzle (finds the nonce). First solver's block is added. The nonce is the **proof of work**.
- **Incentive**: block reward in **new bitcoins**. This is also how new coins are created ("mining").
- **Three pillars**: distributed systems, cryptography, economic model.
- **Blockchain 1.0** = DLT (cryptocurrency). **2.0** = smart contracts. **3.0** = trustless decentralization (permissioned, enterprise).
- **Smart contract** = code executed automatically on a decentralized platform, with execution state stored on the blockchain.
- **PoW problem for enterprises**: high latency, low throughput (Bitcoin about 10 min per block).
- **Permissioned**: known, pre-authenticated participants. Uses classical consensus plus signatures (witness cosigning).
- **Block** = header + transactions. Size about 1 MB.
- **Header**: previous hash, Merkle root, timestamp, difficulty bits, nonce, version.
- **Target** = coefficient × 2^(8 × (index − 3)). Block hash must meet the leading-zero requirement.
- **Mining** is costly: ASICs, huge energy, mining pools. Security depends on an **honest majority of computing power**.
- **scriptPubKey** locks the output. **scriptSig** unlocks the input. Both must run to TRUE.
- **Script language**: stack-based, left to right, **not Turing complete, no loops**.
- **P2PKH** steps: OP_DUP → OP_HASH160 → push pubKeyHash → OP_EQUALVERIFY → OP_CHECKSIG.
- **Time lock** uses OP_CHECKLOCKTIMEVERIFY. **Multisig** needs multiple signatures.

---

# Week 4

## Lecture 16: Joining the Network, Transaction Flooding, Block Propagation, Forks

### Bitcoin peer-to-peer network
- **Ad hoc** network with a **random topology**, running over **TCP**.
- **All nodes are equal**: no client-server and no master-slave structure.
- New nodes can join **at any time**.
- Nodes that stop responding are **removed after about 3 hours** of inactivity.

### How a new node joins
1. Install and run the Bitcoin software on your machine.
2. Ask a **seed node** for an address list.
3. The seed node sends the **addresses of some peers (neighbors)**. The new node connects only to a few neighbors, not to all nodes.
4. Ask the neighbors for the **latest blockchain** and download it.
5. Now the node is at par with all other nodes and is a **valid node**.

- You do **not** have to make transactions or mine. You can just watch the network (new blocks, transactions).

### Transaction flooding
Example: Alice makes a transaction A → B of 10 BTC.
1. Alice sends it to her **neighbors**.
2. Each neighbor **validates** it, then **relays it to its own neighbors**, and so on. This spreads across the whole network (**flooding**).
3. If a node receives the **same transaction again**, it ignores it, so duplicates do not loop forever.

**What a node checks before relaying a transaction:**
- It is valid in the current blockchain (no conflict).
- **No double spending.**
- The **script** matches the allowed (whitelisted) script types, with no risk of infinite loops.

- Because everything is asynchronous, **different nodes have different transaction pools** (cache) at any moment, and in different orders.

### Mining and block propagation
1. Each mining node collects transactions received **since the last block** and builds a **Merkle tree**. Block size is at most **1 MB**.
2. Different miners can have **different sets of transactions**. That is fine.
3. Miners search for a **nonce** (the five other header items are known). **Not all nodes mine.** Many nodes lack the hardware, and some miners combine resources in pools.
4. The **first miner to solve the puzzle** creates the block and gets the **reward**. The work of the other miners is wasted.
5. The winner **floods the new block** to its peers.
6. Peers **verify** the block (hash with the required leading zeros) and add it to their chain, then relay it onward.
7. Other miners **stop** working on that block. They **remove** the transactions included in the new block from their pool, then start the next block.

**Rewards for the winning miner:**
1. **Block generation reward** (new bitcoins).
2. **Transaction fees**: users commit a small fee for getting their transaction included.

### Fork
- If **two miners mine a block at almost the same time**, different parts of the network receive different blocks (say block 2 and block 3 after block 1).
- Nodes add whichever they received first (usually based on what the majority of neighbors send), so the chain splits temporarily.
- As more blocks are added, one branch becomes the **longest chain**. The majority accepts it as the **main chain**, and the other branch **dies out**.
- **Only the longest chain prevails.**
- **Accidental forks** are rare.
- **Intentional forks** (**hard fork** and **soft fork**) are used to upgrade the software version or create new versions of the network (e.g., Bitcoin Cash).

---

## Lecture 17: Block Reward, Double Spending, Anonymity, Exchanges

### Generating coins
- Like any currency, supply must be **controlled**, otherwise there is **inflation**.
- **Counterfeit** (invalid) bitcoins are rejected because nodes validate every transaction using the scripts.
- New bitcoins are created **only through mining**, as the **block reward**.

### Block reward and fees
- The miner gets a **block reward** (6.25 BTC in the lecture) **plus transaction fees** (small amounts paid by users, measured in **satoshis per virtual byte**).
- **Block 0** (the first block) had a reward of **50 BTC**.

### Difficulty adjustment
- Target time to mine a block is about **10 minutes**.
- Hardware keeps getting faster, so the **difficulty (leading zeros) is increased** to keep this 10 minutes.
- Difficulty is adjusted **every 2016 blocks** (about **2 weeks**).

### Reward halving
- The block reward is cut by **50% every 210,000 blocks** (about **4 years**).

| Period | Reward per block |
|---|---|
| Start (2009) | 50 BTC |
| Next | 25 BTC |
| Next | 12.5 BTC |
| Lecture time | 6.25 BTC |
| After about 2024 | 3.125 BTC |

- Total bitcoins ever: slightly **less than 21 million**.
- The **last bitcoin** will be mined around the year **2140**. After that miners earn **only transaction fees**.

### Making a payment
1. Bob sends his **address** to Alice.
2. Alice adds Bob's address and the amount to a **transaction**.
3. Alice **signs** it with her **private key** and announces her **public key** for verification.
4. The transaction is **broadcast** to the network.

### Preventing double spending
- Every transaction and block is **validated** by many nodes.
- If both spends are in the **same block**, they are detected.
- If they go into **two different blocks (a fork)**, only one branch survives.
- Payment is released only after **several confirmations** (more blocks added on top).
- The **block reward** is released to a miner only after about **100 confirmations**.

### Anonymity
- The network is **permissionless**, so no account is needed.
- Bitcoin **addresses are hashes of public keys**, not the keys themselves (and not IP addresses).
- People use **many key pairs** (a "key ring") and give a different address for each payment, so payments cannot easily be linked to one person.
- Each address has its own balance. Coins from several addresses can be combined in one payment, with the **change** returned to yourself.
- Bitcoin uses **ECDSA** for signatures.

### What owning a bitcoin means
- Bitcoins do **not exist** as physical or electronic objects.
- Owning bitcoin = having a **private key** that matches an address that received coins.
- **If you lose your private key, you lose the bitcoins**, and many bitcoins are lost this way.
- Store the private key safely (hardware device, paper QR code). For a shop payment, scan the shop's address QR, then scan your private key.

### Bitcoin exchanges
- Legality of **using** bitcoin to pay differs by country. In many places **trading** it is allowed, and it is treated like a **commodity**.
- **Centralized exchanges** (several Indian ones were named in the lecture) work like demat accounts: you complete **KYC**, they hold your balance, and you buy and sell for profit.
- Trading on an exchange is **not the same** as running a node or mining.
- Some countries let users cash out to **anonymous prepaid cards**.
- **Decentralized exchanges** are technically possible, but there is no one to turn to if something goes wrong (recovery is a challenge). Centralized exchanges give you someone responsible.

---

## Lecture 18: Consensus in the Permissionless Model

### Why classical consensus does not work here
- Classical consensus needs a **closed network** (everyone knows everyone) and **message passing**.
- An open blockchain network is **asynchronous**, so the **FLP impossibility** applies.

### Permissionless (open) model
- **Anyone can join, leave and initiate transactions.** No KYC or pre-authorization. Identity is just a **digital signature**.
- Examples: **Bitcoin** and **Ethereum** (supports DApps, e.g., CryptoKitties).
- **Key assumption**: **more than 50%** of participants are **honest**.
- So the network must be **very large**. In a small network (e.g., 10 nodes) an attacker can easily control 6 of them.

### Challenges for consensus in an open network
1. **Participants do not know each other**, so message passing is not possible.
2. **Anyone can propose a block.** Different participants should win in different rounds. If one person adds many blocks, they control part of the network (**true decentralization** is needed).
3. The network is **asynchronous**: messages can be lost or arrive out of order.
   - TCP is end to end, but the application layer (a peer) may drop messages or crash.
   - Messages spread through a **gossip protocol** (each node tells its neighbors, who tell theirs).
   - There is **no global clock** (clock drift; NTP is not perfect).
4. **Blocks may arrive in a different order** at different nodes.
5. **Prevent monopoly**: no single user or colluding group should gain control.

### Synchronous vs asynchronous network
- **Synchronous**: messages arrive in real time with little or no delay, with no loss or reordering.
- **Asynchronous**: no guarantee **if or when** a message arrives (could be lost or hours late).

### Types of faults
1. **Crash fault**: a node stops responding (hardware or software problem).
2. **Link (network) fault**: a link stops delivering messages.
3. **Byzantine fault**: a node behaves **maliciously** (e.g., tells one peer "next block is B2" and another "next block is B4"). This is the hardest to handle.

### FLP impossibility
- Consensus is impossible in an asynchronous system even with one crash fault, so **safety and liveness cannot both be guaranteed**.
- **Nakamoto consensus (PoW) gives priority to liveness.**

### Setup of the consensus problem
- Each miner keeps an **unconfirmed transaction list**.
- Because the network is asynchronous, **different miners have seen different transactions**.
- Question: **who adds the next block?**

---

## Lecture 19: Nakamoto Consensus (Proof of Work) in Detail

### Safety and liveness for blockchain

**Safety** has two parts:
- **Safety 1**: the next block is **correct**. Transactions are valid (checked using scripts), and the block has the correct hash and nonce.
- **Safety 2**: all miners agree on a **single block** (**consensus finality**). This is hard in an open network.

**Liveness**: **add a block as long as it is correct.** Do not wait to confirm that it is unique.

> **PoW ensures Safety 1 and Liveness. Safety 2 (finality) is compromised immediately but achieved eventually.**

### Miner's process
1. Pick transactions from the **unconfirmed transaction list** and build a block.
2. Every miner works **independently**, with no coordination.
3. Block size has an upper limit (Bitcoin is 1 MB). There is **no fixed number or ordering** of transactions (at least one is needed).

### The puzzle (challenge-response)
- Find a **nonce n** so that **y = H(x ‖ n)** and **y ≤ target (yt)**.
- **x** = Merkle root + timestamp + **previous block hash**.
- **No shortcut**: miners must try nonces repeatedly (brute force). Solving is **hard**, verifying is **easy**.

**What is common and what differs between miners**

| Common to all miners | Different for each miner |
|---|---|
| Previous block hash (yp) | Merkle root (different transactions) |
| Target (yt), based on the current blockchain | Timestamp |
| | The nonce found |

### The hash function does two jobs
1. Links the block to the **previous block** (because x contains the previous block hash). This forms the chain.
2. The nonce gives a **proof of work** for consensus.

### After one miner solves it
1. The winner **signs** the block and **broadcasts** it with the gossip protocol.
2. Others **verify** it (they have the Merkle root, timestamp, nonce and previous hash) and add it.
3. Other miners stop, **remove committed transactions** from their unconfirmed list and start the next round.
4. The number of miners can change every round.
- No guarantee that **your** transaction gets into the latest block (the miner may not have heard it yet).

### Open question
- What if **two miners solve it almost simultaneously**? (Next lecture.)

---

## Lecture 20: Forks, Attacks on PoW and the 51% Attack

### Handling simultaneous blocks
- Both blocks are **valid** (Safety 1 holds). The blockchain becomes a **tree** for a while.
- Goal: **eventual consensus** (eventual finality).
- One branch becomes the **main chain**. The other becomes a **fork** and is abandoned.

### Rule to choose the branch
- **Majority rule**: a node accepts the block that it hears from the **majority of its peers**.
- If it is a tie, **choose randomly**.
- Eventually one branch grows longer and is accepted as the **longest chain**.
- Transactions that were only in the fork block (not in the main chain) go **back to the unconfirmed transaction list**, and are included in a later block.

### Confirmations
- A node cannot immediately know whether a block will be forked.
- **Bitcoin rule**: do not use or trust a transaction until **6 blocks** have been added after its block (**6 confirmations**). This gives **eventual consensus finality**.

### Attacks on proof of work

**1. Sybil attack**
- The attacker fills the network with **many fake identities** (many public keys or addresses).
- These fake nodes can refuse to relay valid blocks or relay bad ones.
- **Bitcoin's defense**: allows only **one outbound connection per /16 block of IP addresses**, so many identities in one subnet cannot all become your peers.

**2. Denial of Service (DoS) attack**
- An attacker floods a node with lots of (invalid) transactions to block its processing.
- **Defense**: limit forwarding, and **disconnect peers** that send too many transactions.

**3. 51% attack**
- PoW security assumes the attacker **cannot control more than 50% of the hash power**.
- To change an old block, the attacker must redo the nonce for that block **and every later block**. This is normally too slow, because new blocks keep arriving.
- If the attacker's hash power (**Pa**) is **greater than** the honest network's (**Pb**), the attacker can rewrite the chain faster than it grows.
- It is **hard but not impossible**. In a small network it is easy.
- Real cases:
  - **Nov 2013**: GHash.io mining pool, repeated double spending against **BitcoinDice** (a gambling site).
  - **Aug 2016**: **Krypton**, an Ethereum-based network, suffered a 51% attack (the network was small).

### Monopoly problem
- PoW depends on **computing resources**, so miners with more resources win more often.
- Rewards decrease over time, so small miners lose interest and leave.
- A **few large miners** then control the network, which makes a **51% attack** possible.
- Game-theory explanation: the **tragedy of the commons**.
- Bitcoin is large enough for this to be unlikely for now.

### Conclusion
- PoW may create **forks**, so finality is **not immediate**. It is achieved eventually (6 confirmations).
- Security holds only if attackers cannot get **more than 50%** of the hash power, so the network must be **large**.
- Next lecture: other limitations of PoW and its **variants**.

---

## Quick Revision (Week 4)

- **Join network**: seed node → address list → connect to neighbors → download the latest blockchain.
- **Flooding**: validate → relay → ignore duplicates. Each node has its **own transaction pool**.
- **Miner winner** floods the block. Others verify, add, and drop the included transactions.
- **Miner income** = block reward + transaction fees.
- **Fork**: two simultaneous blocks. **Longest chain** becomes the main chain. **Hard fork** and **soft fork** are intentional upgrades.
- **Block time** about 10 min. **Difficulty** changes every **2016 blocks** (about 2 weeks).
- **Halving** every **210,000 blocks** (about 4 years): 50 → 25 → 12.5 → 6.25 → 3.125. **Max supply** is under **21 million**, and the last coin is mined around **2140**.
- **Double spending** is prevented by validation, forks and **confirmations** (6 for transactions, about 100 for block rewards).
- **Addresses** = hash of public key. Use many key pairs for anonymity. **Lose private key = lose coins.**
- **Exchanges** trade bitcoin as a commodity and are usually centralized (KYC).
- **Permissionless assumption**: more than **50% honest** and a **very large network**.
- **Open-network challenges**: unknown participants, anyone can propose, asynchronous, ordering, monopoly.
- **Faults**: crash, link, **Byzantine**.
- **Safety 1** (correct block) and **liveness** hold in PoW. **Safety 2** (single block, finality) is only eventual.
- **PoW puzzle**: y = H(x ‖ n) ≤ target, with x = Merkle root + timestamp + previous hash.
- **Majority rule** picks the branch, with a random pick on a tie.
- **Attacks**: **Sybil** (fake identities), **DoS**, **51%** (more than half the hash power). **Monopoly** is the tragedy of the commons.

---

# Week 5

## Lecture 21: Limitations of PoW and Alternatives (PoS, PoB, PoET)

### Good things about PoW
- Fully **decentralized** consensus for a **permissionless** network.
- Gives **safety** and **liveness** (finality only eventually).
- Works well for **cryptocurrency**: a free, open marketplace with no bank or government control.

### Limitations of PoW
1. **Needs a very large network.** It is "trustless" about individuals, but you must trust that the **society as a whole** is honest. The network must be large enough that nobody can get **51% of the hash power**.
   - Bitcoin grew big before attackers understood the 51% attack. A **new** application (or an enterprise network with few stakeholders) cannot easily guarantee a large network at the start (**bootstrapping problem**).
2. **Very low transaction throughput.**
   - Bitcoin: about **3.3 transactions per second**. Ethereum: about **15 per second**.
   - Visa/Mastercard handle thousands per second (5,000 to 10,000+).
3. **Wasted computing power.**
   - Only the **winning miner** gets the reward. All others (thousands) wasted their effort.
   - A block that becomes a **fork** loses its reward: its **coinbase transaction** (the first transaction, which is the mining reward) becomes invalid.
4. **Huge energy use** (figures from the Digiconomist index):
   - About **157.74 TWh per year** (30 Aug 2021).
   - About **825 kg of carbon footprint per transaction**.
   - About **1738 kWh per transaction** (like a US household for about 60 days).

### Proof of Stake (PoS)
> In **Proof of Stake**, the chance of creating the next block depends on the **amount of coins (stake) the miner holds**, not on computing work.

- Proposed in **2011** by a member of the Bitcoin forum (no formal paper).
- Idea: start with PoW, then **switch to PoS once coins are widely distributed**.
- PoW: chance depends on **work done**. PoS: chance depends on **coins held** (1% of coins → about 1% of blocks), like shareholding.
- **Why it is more protected**: an attack is **expensive** (you need a majority of coins), and the attacker would **lose value** by attacking.
- **Ways to define stake**:
  - **Randomized selection** using stake (used in NXT and BlackCoin).
  - **Coin age** = number of coins × number of days held (used in Peercoin). Holding coins longer counts more, so a quick buyer cannot attack.

### Proof of Burn (PoB)
> In **Proof of Burn**, a miner shows proof that they **burned (destroyed) some coins** by sending them to a **verifiably unspendable address**.

- It is "expensive" like PoW, but wastes **digital currency**, not real computing power, so it is claimed to be more **energy efficient**.
- It burns coins that were **mined using PoW**.

### Problem with PoS and PoB
- Both depend on **coins mined by PoW**. So they **cannot be used to bootstrap** a new network. You must start with PoW and move later.

### Proof of Elapsed Time (PoET)
> In **Proof of Elapsed Time**, every participant **waits for a random amount of time**, and the **first one whose timer finishes becomes the leader** and proposes the block.

- Proposed by **Intel**, used in **Hyperledger Sawtooth**.
- Problem: how do we know the participant **really waited** and did not cheat?
- Solution: use hardware, **Intel SGX (Software Guard Extensions)**, a **Trusted Execution Environment (TEE)**.
  - The system is split into an **untrusted world** (normal apps) and a **trusted world** (hardware-protected).
  - The trusted code cannot be changed by the rest of the system, and the hardware gives an **attestation** (a signed proof) that it ran correctly (e.g., that the full wait time passed).
  - Other TEEs: **ARM TrustZone**.
- PoET **can bootstrap** a network, but works **only on special hardware** (Intel SGX).

### Summary and trade-offs
- PoW is costly. PoS and PoB are cheaper but **cannot bootstrap**. PoET can bootstrap but **needs special hardware**.
- "No free lunch": choose by your application's needs.
- All of these are for **open (permissionless)** networks. Enterprise (closed) networks need other mechanisms, which come next. Even then some assumption such as "enough honest participants" (about **33%** for classical BFT, to be covered later) is needed.

---

## Lecture 22: Introduction to Ethereum and Go Ethereum (geth)

### Ethereum
- A **permissionless blockchain platform** like Bitcoin, but it lets users send cryptocurrency for a small fee **and** run **smart contracts** (applications "that everyone can use and no one can take down").
- Development started around **2013**, launched **July 2015**.
- It is the most popular cryptocurrency after Bitcoin. The cryptocurrency is **ether**.
- It is **decentralized**: there is no central Ethereum server.

### Ethereum node and client
- **Node** = any computing device running an **Ethereum client** (a program that connects to the network and makes transactions).

**Components of an Ethereum client:**
| Component | Role |
|---|---|
| **Consensus module** | Handles consensus. Mainnet uses **Proof of Work**; others like **Proof of Authority** are supported |
| **Ethereum state** | Maintains the state of the ledger |
| **EVM (Ethereum Virtual Machine)** | Executes smart contracts |
| **Transaction pool (txpool)** | Caches transactions in memory for validation and execution |
| **P2P module** | Communicates with other nodes (peer-to-peer) |

- The **Ethereum mainnet** is one instance of the network. Anyone can create their **own Ethereum network** by connecting their own nodes.

### Go Ethereum (geth)
- The **official Go implementation** of the Ethereum client. It is a **command-line** client.
- Used to connect to the mainnet, test networks, or your own network.
- **End users do not use geth directly.** Developers build apps on top of it using SDKs like **web3.js** or **ethers.js**.
- geth exposes **JSON-RPC endpoints** over **HTTP, WebSocket, or IPC**.

### Installing geth (Ubuntu)
1. `sudo add-apt-repository -y ppa:ethereum/ethereum`
2. `sudo apt-get update`
3. `sudo apt-get install ethereum`
4. `geth version` to check.

### Accounts
- `geth account list`, `geth account new`, `geth account update`, `geth account import`.
- Each account has a **public key (address)** and **private key**.
- The **private key is not stored in plain text**; it is **encrypted with your password** and kept in the **keystore** folder (`~/.ethereum/keystore`).

### Test networks
- Mainnet transactions need real ether (gas), so use **test networks** for practice.

| Test network | Consensus | Note |
|---|---|---|
| **Ropsten** | Proof of Work | Slower, same as mainnet |
| **Rinkeby** | Proof of Authority | Faster |
| **Goerli** | Proof of Authority | Faster (used in the lectures) |

### Sync modes

| Mode | What it does |
|---|---|
| **Full** | Downloads **all blocks** (headers, transactions, receipts) and **executes every block** to build the state. Most resource-heavy |
| **Fast / Snap** | Downloads headers and receipts and verifies them. **Snap is the default** |
| **Light** | Downloads headers, **verifies only some data randomly**, and relies on other full nodes. **Fastest and lightest** |

- Connect to Goerli in light mode: `geth --goerli --syncmode light`
- Add `--http` to enable **RPC over HTTP** (default `127.0.0.1:8545`).

### Two ways to use geth's API
- **IPC / JavaScript console**: more functions, but needs **direct access** to the machine running geth.
- **RPC over HTTP**: remote apps can connect, but has **security considerations** (you expose your node).

### Querying a balance (RPC over HTTP)
- Send an HTTP **POST** (e.g., with `curl`) with a **JSON payload**: `jsonrpc: "2.0"`, `method: "eth_getBalance"`, `params: [address, "latest"]`, `id`.
- The result is in **hexadecimal** (e.g., `0x0` means 0).
- Balance unit is **wei**: **1 ether = 10^18 wei**. Divide by 10^18 to get ether.

---

## Lecture 23: Ethereum Transactions, Gas, and Faucets

### Transactions
- **Queries only read** the ledger. A **transaction** **writes** to it.
- An **Ethereum transaction** is a **cryptographically signed instruction from an existing account** that updates the state of the network.
- Simplest example: transfer ether from one account to another.
- You need two things:
  1. **Access to the account** (private key) to sign.
  2. **Gas** to pay the fee.

### Gas
> **Gas** is the **fee paid in ether** for the computational resources needed to execute a transaction.

- Miners/verifiers must validate and execute your transaction, so every transaction costs gas.
- On the **mainnet**, buy ether from an exchange (with real money) or earn it by mining.

### Faucet (for test networks)
- A **faucet** gives **free test ether** so you can pay gas on test networks.
- It is **rate limited** to stop abuse (a DoS attack through unlimited free ether).
- **Goerli faucet**: post a **tweet containing your account address**, paste the tweet URL into the faucet, and choose:
  - 6 ether for 1 day, or 15 ether for 3 days, or 37.5 ether for 9 days.
  - You cannot request again for that period. You would need a new social media account.

### Using accounts on a test network
- Create an account on Goerli: `geth --goerli account new`.
- To reuse a mainnet account, **copy its keystore file** from `~/.ethereum/keystore` to `~/.ethereum/goerli/keystore`.
- Save the password in a file (e.g., `pw.txt`).
- **Unlock the account** when running geth:
  `geth --goerli --syncmode light --http --allow-insecure-unlock --unlock <address> --password pw.txt`

### Sending ether with RPC
- Method: **`eth_sendTransaction`** (a POST request).
- Parameters: **`from`**, **`to`**, **`value`** (amount in **hexadecimal wei**; 0.1 ether = 0.1 × 10^18 wei, converted to hex).
- The response is the **transaction hash**.
- The same method can also **deploy smart contracts**.

### Monitoring a transaction
- Use **Etherscan** (e.g., the Goerli Etherscan site). The status goes from **Pending** to **Success** once it is mined into a block.
- **`eth_getTransactionByHash`**: gets the transaction details (block hash, block number, transaction index).
- **`eth_getBlockByNumber`**: gets the block details. The block number must be given in **hexadecimal**. The output includes difficulty, gas limit, gas used, hash, nonce, miner, and the list of transactions.

---

## Lecture 24: Decentralized Applications (DApps) and web3.js

### DApp
> A **DApp (decentralized application)** is an application that runs on a decentralized network, with no central server or authority.

**Two components of an Ethereum DApp:**
1. **Smart contract**: deployed on the Ethereum network. Its code is executed independently by the participants, and the output is decided by **consensus**.
2. **DApp UI (user interface)**: lets users run transactions and queries on the contract.

- The **DApp UI sits between the end user and the Ethereum node** (geth, or services like Infura).

### web3.js
> **web3.js** is the **Ethereum JavaScript API**: a collection of libraries to interact with a geth node easily (instead of writing manual POST requests).

- It connects to geth through **RPC over HTTP, WebSocket, or IPC**.
- It needs **Node.js** and **npm**. Install: `npm install web3`.
- Check: `var Web3 = require('web3'); console.log(Web3.version)`.

### Connecting
```javascript
var Web3 = require('web3');
var web3 = new Web3('http://localhost:8545');
```
- Port **8545** is where geth opened the RPC endpoint (started with `--http`).

### Querying a balance
```javascript
web3.eth.getBalance(address).then(console.log);
```
- Returns a **promise** (asynchronous). The result prints when the query finishes.
- The balance is shown in **decimal wei** (web3 converts it from hexadecimal automatically).

### Sending a transaction
```javascript
var transaction = {
  from: "<sender address>",
  to: "<receiver address>",
  value: web3.utils.numberToHex(100000000000000000)  // 0.1 ether in wei
};
web3.eth.sendTransaction(transaction).then(console.log);
```
- **`web3.utils.numberToHex`** converts a decimal number to hexadecimal.
- Requirements: geth is running with the sender account **unlocked**, and the account has **ether for gas**.
- The program **waits until the transaction is mined**, then prints the **block number, block hash and transaction hash**. Verify on Etherscan.
- The same `sendTransaction` can also be used to deploy smart contracts.

---

## Lecture 25: Ethereum Smart Contracts, Solidity and Remix

### Smart contracts in Ethereum
> **Smart contracts** are programs executed in a **decentralized setting**. They read data from the ledger, process it, and **write results back** to the ledger. The result depends on the **consensus** of the independent participants executing it.

**Properties:**
- A deployed contract gets **its own address** (it acts like an **account**). It can **hold a balance** and **send transactions**.
- It is **not controlled by any single user**; it runs by its own logic.
- Users interact by **sending transactions that call a function** defined in the contract.

### Execution model
- Ethereum is a **replicated (distributed) state machine**. A transaction moves the ledger from one **state** to another. Contracts can have their own **state variables**.
- Execution must be **deterministic**. Every participant executes the contract independently, and if results differed they could not reach consensus.

### Development flow
1. Write the contract in a high-level language: **Solidity** (most popular) or **Vyper**.
2. **Compile** with a smart contract compiler (e.g., **solc**) → **bytecode** + **ABI**.
3. **Deploy** the bytecode to a network (mainnet or test network). The contract gets an **address**.
4. **Execute** via **web3.js** using the **ABI** and the **contract address**.

- **EVM (Ethereum Virtual Machine)** executes the bytecode.
- **ABI (Application Binary Interface)** describes the contract's functions and parameters. Without the ABI you cannot call its functions from web3.js.

### Solidity
- High-level, **statically typed**, supports **inheritance**, **libraries** and complex user-defined types.
- Syntax influenced by **JavaScript and C++**.

### Example: Storage contract
```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract Storage {
    uint256 positiveNumber;

    function store(uint256 num) public {
        positiveNumber = num;
    }

    function readData() public view returns (uint256) {
        return positiveNumber;
    }
}
```
- **License comment** at the top.
- **`pragma solidity`** sets the compiler version range.
- **`contract`** keyword starts the contract.
- **`uint256`** is an unsigned 256-bit integer (the state variable).
- **`public`** means the function can be called from **outside** the contract (by users via transactions).
- **`view`** means the function **only reads** and does not write to the ledger.
- **Queries (view functions) are free. Transactions that change data cost gas.**

### Tools
- **Remix editor**: browser-based IDE to write, compile, test and deploy Solidity (has the compiler built in; shows ABI and bytecode).
- **MetaMask**: a browser extension **wallet** that lets Remix connect to the Ethereum network. It holds accounts and works across mainnet and test networks.
- **JavaScript VM** (in Remix): an emulator in the browser for testing without a real network.
- **Injected web3**: deploys to a real network through MetaMask (MetaMask shows the gas fee estimate and asks you to confirm).

### Using a deployed contract with web3.js
```javascript
var Web3 = require('web3');
var Contract = require('web3-eth-contract');
Contract.setProvider('http://localhost:8545');

var myContract = new Contract(abi, contractAddress, {
  from: "<your account>",
  gasPrice: "20000000000"   // 20 gwei
});

// READ (view function): no gas
myContract.methods.readData().call().then(console.log);

// WRITE (transaction): needs gas
myContract.methods.store(11).send().then(console.log);
```
- You need the **ABI**, the **contract address**, the **from account**, and a **gas price**.
- **`.call()`**: for **view** functions. It just reads the latest ledger state and sends no transaction.
- **`.send()`**: for functions that **change the ledger**. It sends a **signed transaction** and costs gas. The account must be unlocked in geth.

### Summary
- A **DApp = smart contract (Solidity, deployed on the network) + application code (web3.js UI)**.
- Tools involved: **geth**, **web3.js**, **Remix**, **MetaMask**.

---

## Quick Revision (Week 5)

- **PoW limits**: needs a huge network, throughput is low (Bitcoin about 3.3 tps, Ethereum about 15 tps), wasted effort, high energy use.
- **PoS**: chance proportional to **coins held**. Variants: randomization, **coin age** (coins × days). Attack is costly.
- **PoB**: **burn coins** to an unspendable address. Both PoS and PoB **need PoW-mined coins**, so they **cannot bootstrap**.
- **PoET**: random wait timer, first to finish leads. Uses **Intel SGX** (trusted execution environment) for attestation. Used in **Hyperledger Sawtooth**.
- **Ethereum**: launched **2015**, permissionless, runs **smart contracts**. Client parts: consensus, state, **EVM**, txpool, P2P.
- **geth**: Go implementation. Sync modes **full, fast/snap (default), light**. API: **JSON-RPC over HTTP, WebSocket, IPC**.
- **Units**: **1 ether = 10^18 wei**. RPC values are in **hex**.
- **Test networks**: Ropsten (PoW), Rinkeby and Goerli (PoA). **Faucet** gives free test ether.
- **Gas** = fee in ether for executing a transaction. **Queries are free, transactions cost gas.**
- **RPC methods**: `eth_getBalance`, `eth_sendTransaction`, `eth_getTransactionByHash`, `eth_getBlockByNumber`.
- **DApp** = smart contract + UI. **web3.js** talks to geth. `getBalance`, `sendTransaction`, `utils.numberToHex`.
- **Smart contract**: has its own address, must be **deterministic**, runs on the **EVM**.
- **Flow**: Solidity → compile → **bytecode + ABI** → deploy → call from web3.js.
- **`view`** functions use `.call()` (free). **State-changing** functions use `.send()` (gas).
- **Tools**: **Remix** (IDE), **MetaMask** (wallet).

> **Note (not from the lectures):** these lectures were recorded around 2021. Since then, Ethereum's mainnet moved from **Proof of Work to Proof of Stake** (the 2022 "Merge"), and Ropsten, Rinkeby and Goerli have been retired in favor of newer test networks. For the exam, follow the lecture version (mainnet = PoW).

---

# Week 6

## Lecture 26: Consensus in Permissioned Blockchain and State Machine Replication

### Permissioned (closed) blockchain model
- Users are **authenticated beforehand**. An authentication mechanism controls who joins and leaves.
- **Membership Service Provider (MSP)**: gives a node or person the authentication key so it can prove it is a valid member and join the network.
- **Everyone knows who the other participants are**, so message passing is possible (unlike an open network).
- But participants are often **competitors**, so they **do not trust each other** and may behave maliciously. That is why we **still need consensus and security**.
- Typical use: **business applications / contracts among a closed set of participants**.

**Example: provenance tracking in a supply chain (grocery)**
- Farmers → wholesalers → distributors → cold storage → market. Many middlemen, many players.
- A blockchain gives a **common coordination platform** where all players can share reliable information (demand, supply, planning).

### Smart contract (definition)
> A **smart contract** is a **self-executing contract** in which the **terms of agreement between buyer and seller are written directly into lines of code**.

### Executing a smart contract on a closed network
1. **Store the contract on the blockchain.**
2. When an **event is triggered** (e.g., goods delivered or money transferred), **execute the code locally** at a peer.
3. The output is turned into a **transaction** (e.g., "20 tons of potatoes transferred from seller A to buyer B").
4. Other **peers validate** the transaction (they have the contract code too).
5. If valid, it is **committed to the blockchain**. This commit can **trigger the next event** (e.g., payment).

**Do all peers need to execute the code?** No. Execute it on a **subset of nodes** and make sure the **same resulting state is propagated** to all nodes.
- A **majority of peers must agree on the state**.
- Peers act as **witnesses** by **digitally signing** the proposal. A proof that a majority signed shows the information is valid, so it can be committed.

### State Machine Replication (SMR)
- Any **deterministically executed code** can be represented as a **state machine**. So the smart contract is represented as a state machine.
- Example: states such as "more goods?" → deliver goods → "all orders complete?" → go back, or move to the final state "goods transfer complete".

**How SMR works:**
1. The **state machine is replicated** on every server (replica).
2. Clients submit transactions (e.g., T1: delivered 100 kg potatoes, T2: delivered 50 kg tomatoes).
3. The replicas reach **consensus on the order** of the transactions (T1 then T2).
4. Every replica **executes the transactions in that order** on its own copy.
5. All replicas should reach the **same final state** (say S2), and they agree on it.
6. If one replica is **faulty** and reports S3, **majority voting** (the others say S2) gives the correct final state S2.

- This needs a **message-passing** protocol for the voting.

---

## Lecture 27: Crash Fault Tolerance and Introduction to Paxos

### Why SMR works as consensus for permissioned blockchain
1. The network is **closed**, so nodes know each other. Each node can be a **replica**. If replicas agree on the state, nodes agree on the value.
2. **No mining overhead.** Nodes just **pass messages** (no proof of work, stake, burn or elapsed time needed). Everyone is already a member of the consensus group.
- Consensus is still needed because **machines can be faulty or malicious**.
- **Cryptography helps**: digital signatures and hashes can be combined with classical algorithms to **relax some assumptions**.
- Classical algorithms used: **Paxos, Raft, Byzantine agreement protocols (e.g., PBFT)**. All are based on state machine replication.

### Types of faults (recap)
1. **Crash fault**: a node stops operating (hardware or software failure).
   - In an **asynchronous** system you cannot tell whether a silent node **crashed** or its message is **delayed**.
   - You only **do not receive** a message. You never receive a **wrong** one.
2. **Byzantine fault**: a node behaves maliciously (e.g., sends different information to different peers).
   - Harder to handle, and more relevant to blockchain.
   - **BFT algorithms are built on CFT algorithms**, so we learn CFT first.

### FLP and priority
- In asynchronous systems, safety and liveness cannot both be guaranteed, even with one crash fault.
- CFT algorithms like **Paxos**, and some BFT algorithms like PBFT, **give priority to safety over liveness**. That means they reach **consensus finality** (unlike PoW).

### Properties of consensus (CFT)
| Property | Meaning |
|---|---|
| **Validity** | If all correct processes propose the same value v, then any correct process decides v |
| **Agreement** | No two correct processes decide differently |
| **Termination** | Every correct process eventually decides |

**Compared with PoW:** validity is unlikely (miners propose different blocks). Agreement (safety) is not guaranteed immediately. Termination (liveness) is what PoW prioritizes.

### CFT algorithms
- **Paxos**: the most fundamental CFT consensus algorithm, by **Leslie Lamport**.
- **Raft**: simpler than Paxos. Used in **Hyperledger Fabric for transaction ordering** (when there are no Byzantine nodes).

### Dinner example (5 friends, asynchronous)
- A friend asleep (crashed) does not break consensus if the **majority** (3 of 5) agrees. With 5 nodes, at most **2** can be faulty.
- **If there are f crash faults, you need at least 2f + 1 nodes** in an asynchronous CFT system.

### About Paxos
- A **family of algorithms** for consensus in asynchronous systems (we study the basic one).
- Proposed by **Lamport in 1989**, accepted (ACM Transactions on Computer Systems) in **1998**. Paper title: **"The Part-Time Parliament"**. Lamport received the **Turing Award in 2013**.

---

## Lecture 28: The Paxos Algorithm

### Roles
- **Proposer**: proposes a value.
- **Acceptor**: accepts a proposal.
- **Learner**: learns the value at consensus.
- One node can have **more than one role**.

### Majority
- The **number of acceptors is known** in advance, so the majority is known.
- **Any two majorities always overlap in at least one node.** Example: 5 acceptors → majority 3. With **6 acceptors**, 3 is **not** a majority (two groups of 3 do not overlap), so you need **4**.
- Only **crash faults** exist here: you either get the correct message or none.

### ID and state
- Each proposal has a **unique id** (epoch number). Can be a timestamp or a hash of timestamp and proposer id.
- The id acts as the **state**. It helps ignore old or delayed messages.
- **A single Paxos run reaches one consensus.** For many consensus decisions, use **Multi-Paxos**.
- **Consensus is on the value, not on the id.**

### Paxos steps
1. **Prepare**: the proposer sends **prepare(id)** to a majority (or all) of the acceptors.
2. **Promise**: an acceptor checks if it already promised to ignore this id.
   - If yes → ignore.
   - Otherwise → **promise to ignore any request with a lower id** and reply **promise(id)**.
   - **If the acceptor has already accepted a value**, the promise also carries that **accepted id and value**.
3. **Accept request**: when the proposer gets **promises from a majority** for its id, it sends **accept-request(id, value)**.
   - **Which value?** If any promise contained an already accepted value, the proposer must **use that value (the one with the highest id)**. If none, it uses **its own value**.
4. **Accept**: an acceptor that has not promised to ignore this id replies **accept(id, value)** to the proposer and to the **learners**.
5. **Consensus**: when a **majority of acceptors accept** the value, **consensus is reached** on that value.

**Why this works**
- Round 1 (prepare/promise) **agrees on the state (id)** and ignores old delayed messages.
- Round 2 (accept request/accept) **agrees on the value**.
- Because of the overlapping majority, a later proposer always learns about an **already accepted value** and keeps it. So the value never changes after consensus.

---

## Lecture 29: Safety and Liveness of Paxos, Leader Election, Multi-Paxos

### Safety (why Paxos is safe)
- With f faults, you need **2f + 1** acceptors. Example: 3 acceptors tolerate 1 crash.
- In an asynchronous network, messages can arrive **out of order** (e.g., a proposer closer to an acceptor).

**Case 1:** Acceptor 3 gets **prepare 50** first and promises 50, then gets **prepare 100** and promises 100. Acceptors 1 and 2 promised 100 first and **ignore prepare 50**. Prepare 50 does **not get a majority**, so proposer 1 (id 100) goes ahead.

**Case 2:** Acceptors 2 and 3 get **prepare 50** first (promise 50), so proposer 2 gets a majority and sends **accept request 50**. But before it arrives, they have **already promised 100**, so they **ignore** accept request 50. Proposer 1 (id 100) succeeds.

> **Majority voting + ids ensure safety**, even with delays, reordering and crash faults.

### Liveness (not guaranteed)
- Proposers can keep **competing with higher ids** (prepare 100, then 150, then 200 ...). Each time the earlier proposer's accept request is ignored, so progress may **never finish**.
- So Paxos has **no termination guarantee**: **safety is ensured, liveness is compromised**. This agrees with the **FLP impossibility**.
- A lower-id accept request will not be accepted by a majority. A higher-id request with a different value is handled because the common node tells the earlier accepted value.

### Applications and extensions
- **Leader election**: use standard Paxos where the value is "I will be the leader". Once elected, a leader makes later consensus easier. **Raft** works on this idea.
- **Multi-Paxos**: runs **many Paxos instances**, each with a **round number**. Value agreed in round n is fixed; then start round n + 1 from scratch.
  - Uses: **blockchain** (agree on each block) and **replicated databases** (commit each transaction).

### Limitation
- Paxos works only for **crash faults**. A **malicious node** can break it (next lecture).

---

## Lecture 30: Byzantine Faults and the Byzantine Generals Problem

### Agreement vs consensus
- **Agreement** is a temporary or partial step. **Consensus** may need multiple rounds of agreement. Example: Paxos has two agreement rounds (id, then value).

### Why Paxos fails with a malicious node
- Acceptor 2 already promised 100, but then **also sends promise 50** (it should have ignored 50).
- Now both proposers think they got a majority, and both send accept requests (dinner and movie).
- The malicious acceptor **accepts both**: it tells proposer 1 "dinner" and proposer 2 "movie".
- The two proposers believe different values were agreed, so **safety is violated**.

### Byzantine Generals Problem (Lamport)
- A fort with two doors. Two lieutenants must **attack at the same time** or they lose. They follow the **commander**.
- The commander (or a lieutenant) may be a **traitor** (e.g., bribed), sending "attack" to one and "retreat" to the other.
- Solving this in an asynchronous setting is much harder than in a synchronous one.

**Case: 1 commander + 2 lieutenants**
- Lieutenants share what they received. They **see a conflict** (one has attack, the other retreat).
- But they **cannot tell who is faulty**: the commander, or a lieutenant who is lying about what he heard.
- So you can **detect** a Byzantine fault but **cannot tolerate** it (no consensus).

**Case: 1 commander + 3 lieutenants**
- If the commander is faulty (attack to two, retreat to one): after sharing, every lieutenant sees **2 attack, 1 retreat**, so all agree on the **majority value (attack)**.
- If a lieutenant is faulty: the others still see a majority of the commander's value. All loyal lieutenants **agree on the same value**.
- The agreed value can be attack or retreat. What matters is that **all correct nodes agree on the same value**.

### Byzantine Fault Detection vs Tolerance
| | Detection (BFD) | Tolerance (BFT) |
|---|---|---|
| Goal | Notice that some Byzantine behavior happened | **Reach consensus anyway**, and ideally know who is faulty |

### Key result
> **To tolerate f Byzantine (faulty) nodes, you need at least 3f + 1 nodes in total.**

- 1 faulty node → **4 nodes** needed. (3 nodes: detection only. 4 nodes: consensus.)

**Intuitive proof**
- Take 3f nodes split into three groups: **PL** (f correct), **PF** (f faulty), **PR** (f correct).
- The faulty group tells PL "0" and PR "1", creating a **partition**. PL and PR cannot communicate directly, so each side sees an **equal split**, with no clear majority.
- **Adding one extra correct node** to one side **breaks the tie**. So the total needed is **3f + 1**.

**Compare:** crash faults need **2f + 1** nodes. Byzantine faults need **3f + 1** nodes.

### Next
- **PBFT (Practical Byzantine Fault Tolerance)**, used in **Hyperledger Fabric**.

---

## Quick Revision (Week 6)

- **Permissioned blockchain**: pre-authenticated participants via **MSP**, known to each other but not trusted.
- **Smart contract** = self-executing contract with terms written in code. Steps: store → event triggers local execution → transaction → peers validate → commit (may trigger the next event).
- **SMR**: replicate a deterministic state machine, agree on **order of transactions**, execute, agree on the **final state** by majority.
- **Why SMR for permissioned**: nodes known, **no mining cost**, only message passing. Classical algorithms: **Paxos, Raft, PBFT**.
- **Crash fault**: silent node, never a wrong message. **Byzantine fault**: wrong or inconsistent messages.
- **Consensus properties**: **validity, agreement, termination**.
- **CFT needs 2f + 1 nodes. BFT needs 3f + 1 nodes.**
- **Raft** is used for ordering in **Hyperledger Fabric** (no Byzantine nodes).
- **Paxos** (Lamport 1989, accepted 1998, "The Part-Time Parliament", Turing Award 2013).
- **Paxos roles**: proposer, acceptor, learner. Any two majorities overlap in at least one node.
- **Paxos messages**: **prepare → promise → accept request → accept**. Round 1 agrees on the **id (state)**, round 2 on the **value**. A proposer must reuse an **already accepted value**.
- **Consensus is on the value, not the id.**
- **Paxos**: **safe** (majority + ids handle delays and reordering) but **not live** (dueling proposers). It cannot handle **Byzantine** nodes.
- **Leader election** and **Multi-Paxos** (round numbers, repeated for many values, e.g., blocks).
- **Byzantine Generals**: 1 commander + 2 lieutenants = detect only. 1 commander + 3 lieutenants = consensus by majority.
- **BFD** (detect) vs **BFT** (tolerate and agree).
- **Proof idea for 3f + 1**: faulty nodes partition the network. One extra node breaks the tie.

---
