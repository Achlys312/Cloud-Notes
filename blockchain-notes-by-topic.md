---
tags: [blockchain, notes, iit-kharagpur, nptel]
course: Blockchain and its Applications
organization: by topic (regrouped from the week-wise notes)
---

# Blockchain and its Applications: Notes by Topic

These are the week-wise lecture notes regrouped by topic. Each lecture keeps its full original text, and a small line under each lecture heading says which week it came from. The original weekly quick revisions are kept at the end.

## Contents

1. [1. Blockchain Basics: What and Why](#1-blockchain-basics-what-and-why)
2. [2. Cryptography Foundations](#2-cryptography-foundations)
3. [3. Distributed Consensus Background](#3-distributed-consensus-background)
4. [4. Cryptocurrency History](#4-cryptocurrency-history)
5. [5. Bitcoin: Mining, Blocks, Scripts and the Network](#5-bitcoin-mining-blocks-scripts-and-the-network)
6. [6. Consensus in Permissionless Blockchains](#6-consensus-in-permissionless-blockchains)
7. [7. Smart Contracts and Permissioned Blockchains](#7-smart-contracts-and-permissioned-blockchains)
8. [8. Classical Consensus: Paxos, Byzantine Faults and PBFT](#8-classical-consensus-paxos-byzantine-faults-and-pbft)
9. [9. Ethereum](#9-ethereum)
10. [10. Enterprise Blockchain and Hyperledger Fabric](#10-enterprise-blockchain-and-hyperledger-fabric)
11. [11. Scalable Consensus: Bitcoin-NG, CoSi, ByzCoin, Algorand](#11-scalable-consensus-bitcoin-ng-cosi-byzcoin-algorand)
12. [12. Identity Management: DIDs, Verifiable Credentials, Indy and Aries](#12-identity-management-dids-verifiable-credentials-indy-and-aries)
13. [13. Blockchain Interoperability](#13-blockchain-interoperability)
14. [14. Blockchain Security and Attacks](#14-blockchain-security-and-attacks)
15. [15. Use Cases and Application Design](#15-use-cases-and-application-design)
16. [Quick Revision by Week](#quick-revision-by-week)

## Topic to Lecture Map

| Topic | Lectures |
|---|---|
| 1. Blockchain Basics: What and Why | L1, L2 |
| 2. Cryptography Foundations | L3, L4, L5, L6, L7 |
| 3. Distributed Consensus Background | L8 |
| 4. Cryptocurrency History | L9 |
| 5. Bitcoin: Mining, Blocks, Scripts and the Network | L10, L11, L13, L14, L15, L16, L17 |
| 6. Consensus in Permissionless Blockchains | L18, L19, L20, L21 |
| 7. Smart Contracts and Permissioned Blockchains | L12, L26 |
| 8. Classical Consensus: Paxos, Byzantine Faults and PBFT | L27, L28, L29, L30, L31, L32 |
| 9. Ethereum | L22, L23, L24, L25 |
| 10. Enterprise Blockchain and Hyperledger Fabric | L33, L34, L35, L36, L37 |
| 11. Scalable Consensus: Bitcoin-NG, CoSi, ByzCoin, Algorand | L38, L39, L40, L41, L42 |
| 12. Identity Management: DIDs, Verifiable Credentials, Indy and Aries | L43, L44, L45, L49, L50, L51 |
| 13. Blockchain Interoperability | L46, L47, L48 |
| 14. Blockchain Security and Attacks | L52, L53, L54 |
| 15. Use Cases and Application Design | L55, L56, L57, L58, L59 |

---

## 1. Blockchain Basics: What and Why

*Myths, decentralization, the blackboard idea, formal definition.*

### Lecture 1: Introduction, Myths, Decentralization

*(Week 1)*

#### Myths about blockchain

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

#### Decentralization

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

### Lecture 2: Blockchain Idea and Formal Definition

*(Week 1)*

#### The "Blackboard" idea
Imagine a blackboard where all stakeholders write down everything that happens in the supply chain.

**Properties of this blackboard:**
1. **Infinite space**: nothing is ever erased, so all historical data stays.
2. **Everyone can see it**: this gives transparency and verification.
3. **Changes are visible to everyone**: if you made a mistake, you cannot erase it. You add a correction, and everyone can see it.
4. **Not erasable**: once written, it stays. Nobody can later **deny** what they wrote, because each entry carries their signature.

**Advantages:**
- **One-step auditing**: a simple computer program can check for discrepancies (e.g., 100 barrels produced, only 60 transported, so 40 are missing).
- **Matchmaking**: a company can easily find who has extra petrol or who sells cheaper.

#### Problem: who maintains the board?
- One central entity (government, a cloud provider like Amazon, or one company) is a bad option:
  - If it fails or is attacked, everything is lost (single point of failure).
  - Competitors cannot trust one of their own to maintain it.
- **Decentralization improves security.** If 100 sources hold the same data and we go by majority, an attacker must compromise at least **51** of them instead of just one.
- "No free lunch": decentralization also has overhead, which is covered later.

#### Solution: everyone keeps their own copy
- Every organization keeps its **own copy** of the board.
- New problem: how do we make sure every copy has the **same** information? This is the **distributed consensus problem** (covered later).

#### Blockchain definition
> **Blockchain** is an **immutable, append-only, ever-growing chain of data**. Data once added cannot be deleted or modified later.

- **Immutable**: no one can change it.
- **Append-only**: you can only add new data, not erase.
- **Ever-growing**: new blocks keep getting added.
- New information is added as a **block**, and the same block is appended to **every** local copy. A chain of blocks gives the name **blockchain**.

#### Formal definition (important for the exam)
> **Blockchain is a decentralized, immutable, append-only, public ledger.**

| Keyword       | Meaning                                              |
| ------------- | ---------------------------------------------------- |
| Decentralized | Everyone keeps their own copy, with no central owner |
| Immutable     | Existing data cannot be changed                      |
| Append-only   | You can only add new data                            |
| Public        | Everyone can see and verify the information          |

---

## 2. Cryptography Foundations

*Hash functions, SHA-256, hash pointers, Merkle trees, public key cryptography, RSA, digital signatures.*

### Lecture 3: Cryptographic Hash Functions (Part 1)

*(Week 1)*

#### Why study this?
Hash functions are used to connect blocks in a chain in a **tamper-proof** way. Digital signatures (covered later) are also a core building block.

#### Definition
> A **cryptographic hash function** takes an input of **any size** (message *M*) and produces a **fixed-size output** called the **message digest**, written H(M).

- In blockchain the digest is usually **256 bits**.
- It must be **very fast** to compute.

#### Properties of cryptographic hash functions

1. **Deterministic**: the same message always gives the same digest. There is no randomness.
2. **Collision-free**: two different messages should not give the same digest. If M1 ≠ M2, then H(M1) ≠ H(M2).
3. **Hiding (information hiding)**: even a tiny change in the message gives a completely different digest. From a digest you cannot work out the message, and knowing H(M1) does not help you predict H(M2).
4. **Puzzle friendliness**: see below.

Also: hash functions are **one-way**. Given x, finding H(x) is easy. Given H(x), finding x is practically impossible.

#### Collision resistance and the Birthday Paradox
- "Difficult to find" a collision means it is not strictly impossible, but it would take far too long.
- **Birthday paradox**: with only 23 people the chance that two share a birthday is 0.5, and with 70 people it is 0.999. Collisions happen sooner than you expect.
- For a hash with **n-bit output**, an attacker needs about **2^(n/2)** hash operations to find a collision.
- For n = 256 that is **2^128** operations. Even at 1 microsecond per hash, it takes about **10^25 years**.
- So with a long enough digest (256 bits), finding two messages with the same hash is practically impossible.

#### Hash as a message digest
- If H(x) = H(y), we safely assume x = y.
- So instead of storing or comparing long documents, we store or compare only their **short, fixed-length digests**. This is efficient.

#### Hiding and commitment
- You can **commit** to a value by storing its hash.
- Later, if someone claims the original value was y, hash y and compare it with the stored hash. If it matches, the claim is verified. If not, it is false.

#### Puzzle friendliness
> Given a message **x** and a desired output property **y**, it is hard to find a value **k** such that **H(x ‖ k) = y** (‖ means concatenation).

- y is usually not one exact value but a **set of acceptable values** (for example, a hash with certain properties).
- **Random searching** is the best strategy to solve the puzzle.
- Used in **mining** and **Proof of Work** (Bitcoin).

#### Demo (from the lecture)
- Hash of "hello world" and hash of "hello world 1" are **completely different**, even though the input changed by only a tiny bit.
- SHA-256 output = **64 hexadecimal digits** = 256 bits (each hex digit = 4 bits).
- Other hash functions: MD5, SHA-1, SHA-512 (different output lengths).

---

### Lecture 4: SHA-256 and Patterns of Hashing

*(Week 1)*

#### SHA-256
- SHA = **Secure Hash Algorithm**. SHA-256 gives a **256-bit** message digest.
- It is used in **Bitcoin mining** and is central to Bitcoin's blockchain.
- It is part of a family of hash functions designed by the **US National Security Agency (NSA)**.
- The output is always 256 bits, no matter the input length.

#### Steps of SHA-256

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

#### Patterns of hashing data (two inputs: "Hello" and "World!")

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

### Lecture 5: Hash Pointers, Hash Chain and Merkle Tree

*(Week 1)*

#### Recap of hash properties used here
- **One-way**: from H(M) = D you cannot get back M.
- **Collision-free**: if M1 ≠ M2 then D1 ≠ D2. So if D1 = D2, the messages are the same.

#### Hash pointer
> A **cryptographic hash pointer** (also called a **hash reference**) is a **pointer to the location where information is stored**, together with a **hash of that information**.

**Uses:**
1. **Retrieve** the information (like any pointer).
2. **Check that the information has not been modified.** Go to the location, **recompute the hash** of the data and **match it with the stored hash**. If they match, the data was not tampered with.

- A hash pointer is like a **linked list**, but each pointer also carries a hash of the data it points to.
- Useful when data is stored once and **not modified later**, but you want to **detect any modification**. Blockchain is such an application.

#### Tampering example
- Data "Hello World!" has a hash pointer storing H("Hello World!").
- If the data changes to "Hello World?", the new hash does not match the stored hash, so the pointer **breaks** and the tampering is **detected**.
- **Smart attacker**: changes the data **and also updates the stored hash** in the pointer. Then the mismatch is not detected.
- So we must make it **computationally hard** for the attacker to recompute the hashes.

#### Analogy (locker token)
- You leave a bag in locker 5 and get a token saying "locker 5". A normal pointer only says where it is, so someone could swap your bag.
- If the token also says "red backpack", you can prove what you left. This is like **storing the hash along with the pointer**.

#### Making tampering harder: nonce and restrictions
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

#### Hash chain
> A **hash chain** is a set of blocks connected by hash pointers. Each block stores the **hash of the previous block**.

- If an attacker changes data in one block, its hash changes, so the **next block's pointer breaks**.
- To hide the change, the attacker must **recompute the hash of every later block**, and each hash needs a valid nonce (leading zeros).
- The more blocks in the chain, the **more work** is needed. So tampering becomes **computationally very difficult**.

#### Merkle tree
> A **Merkle tree** is a **binary tree of hash pointers**. Leaf nodes hold the hashes of data (transactions), and each parent holds the hash of its two children joined together.

**Example with 4 transactions T1, T2, T3, T4:**
1. Leaves: H(T1), H(T2), H(T3), H(T4).
2. Next level: H0 = H( H(T1) ‖ H(T2) ) and H1 = H( H(T3) ‖ H(T4) ).
3. Top: **Root hash = H( H0 ‖ H1 )**. This is the **Merkle root**.

- This is **hierarchical hashing** (from Lecture 4).
- If any transaction changes, every hash on the path up to the root changes.
- In blockchain, a Merkle tree is used to **store the transactions of a block**.

#### Block and blockchain structure (preview)
- Each block has a **block header** containing:
  - the **hash of the previous block** (the hash pointer)
  - the **Merkle root**
  - a **nonce**
  - the hash of the block itself
- The block also holds the **transactions**.
- Blocks are linked by hash pointers.
> **A blockchain is a hash chain of blocks**, connected in a tamper-proof way.

---

### Lecture 6: Public Key Cryptography

*(Week 2)*

#### Basic terms
- **Cryptography**: sending a message securely from A to B over a channel that may not be secure (an intruder may read or change it).
- **Plain text**: the original message.
- **Cipher text**: the scrambled message that is actually sent.
- **Encryption**: converting plain text into cipher text.
- **Decryption**: converting cipher text back into plain text.
- **Key**: a parameter that decides the output of a cryptographic algorithm.
- Hash functions cannot be used for this, because even the receiver could not get the message back.

#### Two types of cryptography

| | Symmetric key | Asymmetric key (Public key) |
|---|---|---|
| Keys | **Same key** for encryption and decryption | **Different keys**: one for encryption, another for decryption |
| Problem | How to share the key securely | Solves this problem |

#### Properties of a good cryptographic key
1. **Random**: generated truly randomly so an attacker cannot guess it.
2. **Sufficient length**: otherwise brute force (trying every possibility) works.
3. **Sufficient entropy**: every bit of the key should be equally random.

#### Public key and private key
- Every user has a **key pair**.
- **Private key**: known **only to the owner**.
- **Public key**: known to **everyone**.

#### Sending a secret message (confidentiality)
Alice wants to send message M to Bob:
1. Alice encrypts M with **Bob's public key** → cipher text M'.
2. M' is sent over the unsecured link.
3. Bob decrypts M' with **his own private key** → gets M.

An adversary who sees M' cannot read it, because only Bob has the private key. Anyone (Alice, Tom) can send to Bob using Bob's public key.

#### RSA algorithm
- Named after **Rivest, Shamir, Adleman**. It is one of the first public key algorithms.
- Four steps: **key generation → key distribution → encryption → decryption**.

**RSA key generation**
1. Choose two distinct large **random prime numbers** p and q.
2. Compute **n = p × q**. The length of n is the **key length**.
3. Compute **φ(n) = (p − 1) × (q − 1)** (Euler's totient function).
4. Choose e such that **1 < e < φ(n)** and **gcd(e, φ(n)) = 1** (e and φ(n) are co-prime).
5. Find d such that **d × e ≡ 1 (mod φ(n))** (d is the modular multiplicative inverse of e).

**Public key = (e, n). Private key = (d, n).**

#### Important property
- Encrypt with the public key → decrypt with the private key. This gives confidentiality.
- Encrypt with the private key → decrypt with the public key. **This is used for digital signatures** (next lecture).

#### Digital signature (intro)
> A **digital signature** is a digital code attached to an electronically sent document, used to **verify the content**, **authenticate the sender's identity** and **prevent non-repudiation** (the sender cannot deny sending it).

- Only the signer can sign, but **everyone can verify**.
- A signature is tied to **one document** and cannot be reused on another.

---

### Lecture 7: RSA Encryption/Decryption and Digital Signature

*(Week 2)*

#### RSA encryption and decryption
- Plain text M is converted to an integer m.
- **Encryption**: **C = m^e mod n** (using the public key (e, n)).
- **Decryption**: **m = C^d mod n** (using the private key (d, n)).
- Why it works: (m^e)^d ≡ m (mod n).

#### Worked example (from Stallings)
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

#### Digital signature using public key cryptography

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

#### Use of digital signatures in blockchain
- They **validate the origin of a transaction**.
- They give **non-repudiation**: Alice cannot deny her own transactions.
- No one else (e.g., Carol) can claim Alice's transaction, because the signature can only be verified with Alice's public key.
- Example: Alice creates 10 coins and signs the transaction. Then Alice sends 5 coins to Bob and signs that transaction too.
- **Bitcoin uses ECDSA**, which is based on **elliptic curve cryptography**.

#### Summary of the two main cryptographic tools
1. **Cryptographic hash functions**
2. **Digital signatures**

---

## 3. Distributed Consensus Background

*Consensus problem, faults, synchrony, safety and liveness, FLP.*

### Lecture 8: History of Blockchain and Distributed Consensus

*(Week 2)*

#### Background
- Blockchain became popular around 2014-15, but its ideas are old (**1970s-80s**, from distributed systems research).
- **Three pillars of blockchain**:
  1. Distributed systems
  2. Cryptographic techniques
  3. Economic models (mainly useful for cryptocurrencies)

#### Distributed consensus problem
> When one node proposes something (e.g., a new block), **all other nodes must collectively agree** on it. This is the **distributed consensus problem**.

- In blockchain, the peers are the participating organizations (refinery, distributor, retailer, and so on).
- Once consensus is done, everyone holds the **same copy** of the data.

#### Example: burger or pizza
- **Centralized way**: one friend acts as leader, collects choices and announces the result. You must **trust** the leader.
- **Distributed way**: everyone calls everyone else and shares their choice. Each person counts the majority. **No leader is needed.**
- **Trade-off**: centralized needs about 6 calls, while distributed needs 4 × 3 = **12 calls**. Distributed costs more messages but needs no trust.

#### Byzantine behavior
- A node that tells **different information to different people** (e.g., "pizza" to one friend, "burger" to another) shows **Byzantine behavior**.

#### Types of communication
- **Synchronous**: messages arrive in real time (like a phone call).
- **Asynchronous**: there is **no bound on message delay** (like an SMS). The internet is mostly asynchronous.

#### Types of faults
- **Crash fault**: a node stops responding because of a hardware or software failure. It is easier to handle.
- **Byzantine fault**: a node responds but gives **wrong or inconsistent information**. It is harder to handle.

#### Safety and liveness
- **Safety**: correct processes produce the **correct output**.
- **Liveness**: the output is produced in a **finite amount of time** (the algorithm eventually terminates).

#### FLP Impossibility Theorem (1985)
> By **Fischer, Lynch and Patterson**: consensus is **impossible in a fully asynchronous system, even with a single crash fault**.

- It means **safety and liveness cannot both be guaranteed together**.
- Classical systems give **priority to safety over liveness**.

#### Timeline

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

## 4. Cryptocurrency History

*eCash, b-money, Bit Gold, double spending.*

### Lecture 9: Cryptocurrency History

*(Week 2)*

#### Problems with physical currency
1. **Management**: notes can get torn, and exchanging them is a hassle.
2. **Theft**: notes can be stolen (pickpocketing).

This led to the idea of **digital money**.

#### Three requirements for a cryptocurrency
1. **Third parties cannot determine the payee, the time or the amount** of payments (privacy).
2. **Proof of payment**: you can prove you paid (like a cash memo).
3. **Ability to stop the use of payment media reported stolen.**

#### eCash (1983)
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

#### Move to full decentralization
- New idea: **remove the bank and government completely**. People transact directly, with no third party watching.
- Attraction: it is untraceable and free from government control (but this raises legal and tax debates).

#### b-money and Bit Gold (1998)
- **b-money**: by **Wei Dai**, an anonymous distributed electronic cash system.
- **Bit Gold**: by **Nick Szabo**. It used **cryptographic puzzles**, but puzzle verification still needed **some central involvement**, so it was not fully decentralized.
- Open question: can puzzle solving be verified in a **fully distributed** way?

#### Double spending
> **Double spending** means using the same money more than once.

- Example: you have ₹100, and you send ₹60 to A and ₹80 to B. Both cannot be valid.
- A **consensus mechanism** is needed so the community can detect this by checking transaction history.
- Next question: can classical consensus algorithms be used here?

---

## 5. Bitcoin: Mining, Blocks, Scripts and the Network

*Proof of Work idea, mining, block structure, transactions, scripts, P2P network, rewards, wallets and exchanges.*

### Lecture 10: Bitcoin and Proof of Work

*(Week 2)*

#### Open network
- In an **open network**, **anyone can join** and no central authority exists.
- This is a problem for classical consensus, because it uses **message passing** and needs the **identity of all participants**.
- So classical algorithms work **only in closed systems**.

#### Bitcoin paper (2008)
- Title: **"Bitcoin: A Peer-to-Peer Electronic Cash System"**.
- Author: **Satoshi Nakamoto**.
- It showed how to reach consensus in an open network **without message passing**.

#### Idea: elect a leader by puzzle solving
- The network gives everyone a **hard puzzle**.
- **The first person to solve it becomes the leader** for that round, and the leader's decision (the next set of valid transactions) is accepted.
- Different people win in different rounds.

#### Properties of a good puzzle
1. **Difficult to solve**, so that only one person (usually) solves it first.
2. **Easy to verify**, so everyone can quickly check the answer.

#### Puzzle using hash functions
- Puzzle: given **x** and **y**, find a **nonce N** such that **y = H(x ‖ N)**.
- There is no shortcut, so you must try different nonces (**random search**). This is hard.
- Verification is easy: compute H(x ‖ N) once and compare.

#### Proof of Work (PoW)
> **Proof of Work** is the consensus algorithm where a participant does hard computational work to solve a puzzle, and the solution acts as **proof** that the work was done.

- Also called **Nakamoto consensus**.
- The idea of puzzle solving as proof first came from **Bit Gold**. Bitcoin formalized it and added **coin mining** in an open peer-to-peer network.

#### Safety vs Liveness in Bitcoin
- Classical algorithms: priority to **safety**.
- **PoW (Nakamoto consensus): priority to liveness.**
- Result: **no immediate finality**. A transaction may be accepted now but is not final until later.
- Reason: more than one person may solve the puzzle at the same time, so the network cannot decide immediately which transaction to keep (for example, the ₹60 vs ₹80 double spend). This gets resolved over later rounds.

#### Timeline
| Year | Event |
|---|---|
| 2008 | Bitcoin white paper (the term "blockchain" was **not** used; it said "block" and "chain" separately) |
| 2011 | **Litecoin** |
| 2015 | **Ethereum** goes live (supports decentralized applications, or **DApps**) |
| 2016 | Term **"blockchain"** becomes popular |

#### Open question for next lecture
- Why would anyone spend computing power to solve the puzzle? (Incentives.)

---

### Lecture 11: Bitcoin Mining and Incentives

*(Week 3)*

#### Bitcoin mining
- The open consensus method used in Bitcoin (puzzle solving) is called **mining**.
- **Miners** are special nodes in the Bitcoin network. Anyone can be a miner, with no registration (just run the miner software).
- **Task of a miner**: collect the transactions floating in the network, combine them into a **block** and propose it for the blockchain.

#### How the winning block is chosen
- Many miners build **different blocks**, but only **one** block can be added.
- The network gives a **hard puzzle**: find a nonce so that the hash meets the target (y = H(x ‖ n), where x and y are given and n must be found).
- There is no shortcut, so miners keep **retrying randomly** and spend computing power.
- The **first miner to solve it** gets their block added. The nonce they found is the **proof** attached to the block.
- Other nodes **easily verify** the proof, so the block is valid.
- Different miners win in different rounds, so **no single miner controls the blockchain**.
- This is called **Proof of Work**: the solution is proof that real work was done.

#### Incentive: why would anyone mine?
- Solving the puzzle costs a lot of computing power, so there must be a reward.
- **A miner who successfully adds a block gets new bitcoins as a reward.**
- This is also how **new bitcoins enter the system**. It is like a government minting new money, which is why it is called **mining**.
- The Bitcoin network acts like a **reserve bank without any explicit governance**: it controls the flow of money and creates new currency over time.

#### Three pillars of blockchain
1. **Distributed systems** (distributed consensus)
2. **Cryptographic techniques** (hash chain, puzzles, signatures)
3. **Economic model** (mining reward, controlled coin supply)

Satoshi Nakamoto did not invent entirely new things. He or she **combined existing ideas** from different domains. The identity of Satoshi Nakamoto is unknown.

#### Legal debate
- Bitcoin transactions cannot be easily tracked, so some governments do not allow it.

#### Blockchain 1.0: Distributed Ledger Technology (DLT)
> A **ledger** is where transactions are logged. Bitcoin's is a **distributed public ledger**: anyone can see and verify it.

#### Bitcoin facts and timeline

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

#### Beyond financial transactions
- Idea: instead of logging only financial transactions, **submit executable code as a transaction**.
- Because the platform is distributed and runs consensus, the **code execution itself is agreed upon by everyone**.
- This gives rise to **smart contracts** (next lecture).

---

### Lecture 13: Blockchain Elements 1 (Block Structure and Header)

*(Week 3)*

#### Blockchain
- A platform for executing **transactional services** (e.g., Alice sends 5 bitcoins to Bob, or a vehicle title is transferred).
- An **append-only shared ledger of digitally signed and encrypted transactions**, **replicated across a network of peer nodes**.
- It can span organizations and individuals who **need not trust each other**.
- Peers verify transactions. Security comes from the cryptographic techniques studied earlier.

#### Block structure
> A **block** is a container data structure with two parts: **block header** and **list of transactions**.

- Blocks are linked using **hash pointers**: each block's header holds the hash of the previous block.
- **Size**: a Bitcoin block is about **1 MB** (set by Satoshi Nakamoto), holding roughly 500 to 1000+ transactions.
- **Larger blocks (e.g., 8 MB)**: more transactions per block, but longer verification and propagation time, so higher latency.

#### Block header contains
1. **Previous block hash**
2. **Merkle root** (of the block's transactions)
3. **Timestamp**
4. **Difficulty bits** (the target)
5. **Nonce**
6. **Version**

The **block hash** is the hash of this header. It is the block's identifier.

#### Why it is tamper-proof
- Changing one transaction in an old block (say block 600,000) changes the **Merkle root** → changes that **block's hash** → the next block's "previous hash" no longer matches.
- The attacker must **recompute the hash of every later block** (e.g., all blocks up to 700,000), and each one needs a nonce with the required leading zeros.
- This is computationally very hard unless the attacker has huge computing power.

#### Mining a block
> **Mining** is generating the hash of a block (using the previous hash, timestamp, Merkle root, difficulty bits, version, and a nonce) so that the hash satisfies the required **number of leading zeros**.

- The **block generation puzzle** is to find the **nonce**.

#### Difficulty bits (target)
- "bits" is an 8-hex-digit value, e.g. `0x170e2632`.
  - **First byte** = **index** (0x17 = 23).
  - **Next three bytes** = **coefficient** (0e2632).
- **Target = coefficient × 2^(8 × (index − 3))**
- Written as a 64-hex-digit (256-bit) number, the target decides how many **leading zeros** the block hash needs.
- A block's hash must meet or beat this requirement. In the lecture's example the real block hash had more leading zeros than the minimum required.
- The difficulty **changes over time** (explained later).

#### Verification demo
- Using a block hash verification tool, enter **version, Merkle root, bits, timestamp, nonce, previous block hash** → it computes the block hash, which matches the real block.
- **Verifying is easy; finding the nonce is the hard part.**
- Block explorers: **btc.com** and **blockchain.com**.

---

### Lecture 14: Block Generation Cost, Transactions, Scripts (Intro)

*(Week 3)*

#### Cost of block generation
- Finding the nonce is **computationally expensive** (many leading zeros needed).
- It needs special hardware called **ASICs** (application-specific integrated circuits), which are expensive.
- Only the **first miner** to solve the puzzle gets the **block reward**, so the work of all others is **wasted**.
- The total **hash rate** of the Bitcoin network is huge (about 150 million tera-hashes per second in the lecture).
- It uses a very large amount of electricity (the lecture compared it to powering around 20,000 households; figures vary because no one knows the exact value).
- Individuals cannot compete, so miners form **mining pools** (e.g., F2Pool, AntPool, Binance Pool) that combine their resources.
- **Security assumption**: the **majority of computing power** must be in the hands of **honest nodes**.

#### Peer nodes
- Each node keeps a **full local copy** of the blockchain (about 350 GB at the time).
- All copies must stay **consistent** with the latest mined block.

#### Transactions in a block
- Transactions are organized as a **Merkle tree**. The Merkle root goes into the block header.
- Each transaction has its own **hash**.

#### Inputs and outputs
- A transaction has **inputs** and **outputs**.
- Example: Alice has 100 BTC (the input) and pays Bob 40 BTC. Alice keeps the remaining 60 as **change** in the same transaction.
- Each recipient can later spend their coins in the same way (Bob spends 30 of his 40, and so on).

#### Proving ownership
- Alice **signs** the transaction with her **private key** and sends her **public key**. Bob verifies it using Alice's public key (digital signature).
- Bob must prove later that he truly owns the 40 bitcoins before spending them.
- In Bitcoin this is done with **scripts**.

#### Scripts
- **scriptPubKey**: used by the sender (Alice) to **lock** the payment to Bob (the **output**).
- **scriptSig**: used by the receiver (Bob) to **unlock and claim** it (the **input** of his next transaction).
- Bob can spend the coins **only if both scripts together execute to TRUE**.

**Bitcoin script language:**
- Simple, compact, **stack-based**, processed **left to right** (similar to the Forth language).
- **Not Turing complete**: **no loops**, so the script always terminates. This avoids coins getting stuck because a script never ends.

#### Pay to Public Key Hash (P2PKH)
- Bob gives Alice the **hash of his public key**, not the public key itself.
- Alice pays to that **public key hash**.
- Later Bob provides his **public key** (which must hash to that address) and a **signature** proving he owns the matching private key.

#### Summary
- Block generation is very costly, with a lot of wasted energy. This is the cost of **proof of work**.
- Transactions are included in blocks, and scripts are used to make and claim payments.

---

### Lecture 15: Bitcoin Scripts in Detail

*(Week 3)*

#### Input vs output
- **Transaction output** (Alice → Bob, 40 BTC): uses **scriptPubKey**.
- **Transaction input** (Bob claims and spends, e.g., pays 30 BTC to Carol): uses **scriptSig**.
- Alice also had to claim her own 100 BTC the same way earlier.

#### Why a public key hash?
- A public key can be linked to a person, so paying to the **hash of the public key** keeps the payment more **anonymous**.

#### Script P2PKH
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

#### What each check proves
- **OP_EQUALVERIFY**: the public key Bob gave hashes to the **same hash Alice paid to**, so the payment was meant for Bob.
- **OP_CHECKSIG**: Bob really holds the **private key** for that public key (he signed with it). So he is not an impersonator.
- Together: Alice paid Bob's key hash, and Bob proved ownership, so **Bob is the right person to claim the coins**.
- This uses **hash functions** and **digital signatures** from the earlier lectures.

#### Real example
- A transaction in a real block (viewed on btc.com) showed **P2PKH** inputs and two outputs with the same script pattern (OP_DUP, OP_HASH160, pubKeyHash, OP_EQUALVERIFY, OP_CHECKSIG).

#### Types of operations (op codes)
- Arithmetic
- If/then conditions
- Logical operators
- Data handling (e.g., OP_DUP)
- Cryptographic (hash functions, signature verification)
- **Multi-signature** verification (more than one party must sign, e.g., Alice and Bob together)

#### Other interesting scripts
- **Anyone can spend**: the unlocking script is simply `OP_TRUE`, so anyone can claim the funds.
- **OP_RETURN**: stops further processing of the script.
- **Time lock (freezing funds)**: uses **OP_CHECKLOCKTIMEVERIFY**. The funds cannot be claimed until a set future time (e.g., 15 Nov 2021). If the current time is before that, the script returns **false**.
- A good online resource lists many such scripts.

#### Next lecture
- How blocks are tied together, how nodes receive blocks, how blocks propagate, and how miners generate blocks.

---

### Lecture 16: Joining the Network, Transaction Flooding, Block Propagation, Forks

*(Week 4)*

#### Bitcoin peer-to-peer network
- **Ad hoc** network with a **random topology**, running over **TCP**.
- **All nodes are equal**: no client-server and no master-slave structure.
- New nodes can join **at any time**.
- Nodes that stop responding are **removed after about 3 hours** of inactivity.

#### How a new node joins
1. Install and run the Bitcoin software on your machine.
2. Ask a **seed node** for an address list.
3. The seed node sends the **addresses of some peers (neighbors)**. The new node connects only to a few neighbors, not to all nodes.
4. Ask the neighbors for the **latest blockchain** and download it.
5. Now the node is at par with all other nodes and is a **valid node**.

- You do **not** have to make transactions or mine. You can just watch the network (new blocks, transactions).

#### Transaction flooding
Example: Alice makes a transaction A → B of 10 BTC.
1. Alice sends it to her **neighbors**.
2. Each neighbor **validates** it, then **relays it to its own neighbors**, and so on. This spreads across the whole network (**flooding**).
3. If a node receives the **same transaction again**, it ignores it, so duplicates do not loop forever.

**What a node checks before relaying a transaction:**
- It is valid in the current blockchain (no conflict).
- **No double spending.**
- The **script** matches the allowed (whitelisted) script types, with no risk of infinite loops.

- Because everything is asynchronous, **different nodes have different transaction pools** (cache) at any moment, and in different orders.

#### Mining and block propagation
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

#### Fork
- If **two miners mine a block at almost the same time**, different parts of the network receive different blocks (say block 2 and block 3 after block 1).
- Nodes add whichever they received first (usually based on what the majority of neighbors send), so the chain splits temporarily.
- As more blocks are added, one branch becomes the **longest chain**. The majority accepts it as the **main chain**, and the other branch **dies out**.
- **Only the longest chain prevails.**
- **Accidental forks** are rare.
- **Intentional forks** (**hard fork** and **soft fork**) are used to upgrade the software version or create new versions of the network (e.g., Bitcoin Cash).

---

### Lecture 17: Block Reward, Double Spending, Anonymity, Exchanges

*(Week 4)*

#### Generating coins
- Like any currency, supply must be **controlled**, otherwise there is **inflation**.
- **Counterfeit** (invalid) bitcoins are rejected because nodes validate every transaction using the scripts.
- New bitcoins are created **only through mining**, as the **block reward**.

#### Block reward and fees
- The miner gets a **block reward** (6.25 BTC in the lecture) **plus transaction fees** (small amounts paid by users, measured in **satoshis per virtual byte**).
- **Block 0** (the first block) had a reward of **50 BTC**.

#### Difficulty adjustment
- Target time to mine a block is about **10 minutes**.
- Hardware keeps getting faster, so the **difficulty (leading zeros) is increased** to keep this 10 minutes.
- Difficulty is adjusted **every 2016 blocks** (about **2 weeks**).

#### Reward halving
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

#### Making a payment
1. Bob sends his **address** to Alice.
2. Alice adds Bob's address and the amount to a **transaction**.
3. Alice **signs** it with her **private key** and announces her **public key** for verification.
4. The transaction is **broadcast** to the network.

#### Preventing double spending
- Every transaction and block is **validated** by many nodes.
- If both spends are in the **same block**, they are detected.
- If they go into **two different blocks (a fork)**, only one branch survives.
- Payment is released only after **several confirmations** (more blocks added on top).
- The **block reward** is released to a miner only after about **100 confirmations**.

#### Anonymity
- The network is **permissionless**, so no account is needed.
- Bitcoin **addresses are hashes of public keys**, not the keys themselves (and not IP addresses).
- People use **many key pairs** (a "key ring") and give a different address for each payment, so payments cannot easily be linked to one person.
- Each address has its own balance. Coins from several addresses can be combined in one payment, with the **change** returned to yourself.
- Bitcoin uses **ECDSA** for signatures.

#### What owning a bitcoin means
- Bitcoins do **not exist** as physical or electronic objects.
- Owning bitcoin = having a **private key** that matches an address that received coins.
- **If you lose your private key, you lose the bitcoins**, and many bitcoins are lost this way.
- Store the private key safely (hardware device, paper QR code). For a shop payment, scan the shop's address QR, then scan your private key.

#### Bitcoin exchanges
- Legality of **using** bitcoin to pay differs by country. In many places **trading** it is allowed, and it is treated like a **commodity**.
- **Centralized exchanges** (several Indian ones were named in the lecture) work like demat accounts: you complete **KYC**, they hold your balance, and you buy and sell for profit.
- Trading on an exchange is **not the same** as running a node or mining.
- Some countries let users cash out to **anonymous prepaid cards**.
- **Decentralized exchanges** are technically possible, but there is no one to turn to if something goes wrong (recovery is a challenge). Centralized exchanges give you someone responsible.

---

## 6. Consensus in Permissionless Blockchains

*Nakamoto consensus, forks, attacks on PoW, limits of PoW, PoS, PoB, PoET.*

### Lecture 18: Consensus in the Permissionless Model

*(Week 4)*

#### Why classical consensus does not work here
- Classical consensus needs a **closed network** (everyone knows everyone) and **message passing**.
- An open blockchain network is **asynchronous**, so the **FLP impossibility** applies.

#### Permissionless (open) model
- **Anyone can join, leave and initiate transactions.** No KYC or pre-authorization. Identity is just a **digital signature**.
- Examples: **Bitcoin** and **Ethereum** (supports DApps, e.g., CryptoKitties).
- **Key assumption**: **more than 50%** of participants are **honest**.
- So the network must be **very large**. In a small network (e.g., 10 nodes) an attacker can easily control 6 of them.

#### Challenges for consensus in an open network
1. **Participants do not know each other**, so message passing is not possible.
2. **Anyone can propose a block.** Different participants should win in different rounds. If one person adds many blocks, they control part of the network (**true decentralization** is needed).
3. The network is **asynchronous**: messages can be lost or arrive out of order.
   - TCP is end to end, but the application layer (a peer) may drop messages or crash.
   - Messages spread through a **gossip protocol** (each node tells its neighbors, who tell theirs).
   - There is **no global clock** (clock drift; NTP is not perfect).
4. **Blocks may arrive in a different order** at different nodes.
5. **Prevent monopoly**: no single user or colluding group should gain control.

#### Synchronous vs asynchronous network
- **Synchronous**: messages arrive in real time with little or no delay, with no loss or reordering.
- **Asynchronous**: no guarantee **if or when** a message arrives (could be lost or hours late).

#### Types of faults
1. **Crash fault**: a node stops responding (hardware or software problem).
2. **Link (network) fault**: a link stops delivering messages.
3. **Byzantine fault**: a node behaves **maliciously** (e.g., tells one peer "next block is B2" and another "next block is B4"). This is the hardest to handle.

#### FLP impossibility
- Consensus is impossible in an asynchronous system even with one crash fault, so **safety and liveness cannot both be guaranteed**.
- **Nakamoto consensus (PoW) gives priority to liveness.**

#### Setup of the consensus problem
- Each miner keeps an **unconfirmed transaction list**.
- Because the network is asynchronous, **different miners have seen different transactions**.
- Question: **who adds the next block?**

---

### Lecture 19: Nakamoto Consensus (Proof of Work) in Detail

*(Week 4)*

#### Safety and liveness for blockchain

**Safety** has two parts:
- **Safety 1**: the next block is **correct**. Transactions are valid (checked using scripts), and the block has the correct hash and nonce.
- **Safety 2**: all miners agree on a **single block** (**consensus finality**). This is hard in an open network.

**Liveness**: **add a block as long as it is correct.** Do not wait to confirm that it is unique.

> **PoW ensures Safety 1 and Liveness. Safety 2 (finality) is compromised immediately but achieved eventually.**

#### Miner's process
1. Pick transactions from the **unconfirmed transaction list** and build a block.
2. Every miner works **independently**, with no coordination.
3. Block size has an upper limit (Bitcoin is 1 MB). There is **no fixed number or ordering** of transactions (at least one is needed).

#### The puzzle (challenge-response)
- Find a **nonce n** so that **y = H(x ‖ n)** and **y ≤ target (yt)**.
- **x** = Merkle root + timestamp + **previous block hash**.
- **No shortcut**: miners must try nonces repeatedly (brute force). Solving is **hard**, verifying is **easy**.

**What is common and what differs between miners**

| Common to all miners | Different for each miner |
|---|---|
| Previous block hash (yp) | Merkle root (different transactions) |
| Target (yt), based on the current blockchain | Timestamp |
| | The nonce found |

#### The hash function does two jobs
1. Links the block to the **previous block** (because x contains the previous block hash). This forms the chain.
2. The nonce gives a **proof of work** for consensus.

#### After one miner solves it
1. The winner **signs** the block and **broadcasts** it with the gossip protocol.
2. Others **verify** it (they have the Merkle root, timestamp, nonce and previous hash) and add it.
3. Other miners stop, **remove committed transactions** from their unconfirmed list and start the next round.
4. The number of miners can change every round.
- No guarantee that **your** transaction gets into the latest block (the miner may not have heard it yet).

#### Open question
- What if **two miners solve it almost simultaneously**? (Next lecture.)

---

### Lecture 20: Forks, Attacks on PoW and the 51% Attack

*(Week 4)*

#### Handling simultaneous blocks
- Both blocks are **valid** (Safety 1 holds). The blockchain becomes a **tree** for a while.
- Goal: **eventual consensus** (eventual finality).
- One branch becomes the **main chain**. The other becomes a **fork** and is abandoned.

#### Rule to choose the branch
- **Majority rule**: a node accepts the block that it hears from the **majority of its peers**.
- If it is a tie, **choose randomly**.
- Eventually one branch grows longer and is accepted as the **longest chain**.
- Transactions that were only in the fork block (not in the main chain) go **back to the unconfirmed transaction list**, and are included in a later block.

#### Confirmations
- A node cannot immediately know whether a block will be forked.
- **Bitcoin rule**: do not use or trust a transaction until **6 blocks** have been added after its block (**6 confirmations**). This gives **eventual consensus finality**.

#### Attacks on proof of work

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

#### Monopoly problem
- PoW depends on **computing resources**, so miners with more resources win more often.
- Rewards decrease over time, so small miners lose interest and leave.
- A **few large miners** then control the network, which makes a **51% attack** possible.
- Game-theory explanation: the **tragedy of the commons**.
- Bitcoin is large enough for this to be unlikely for now.

#### Conclusion
- PoW may create **forks**, so finality is **not immediate**. It is achieved eventually (6 confirmations).
- Security holds only if attackers cannot get **more than 50%** of the hash power, so the network must be **large**.
- Next lecture: other limitations of PoW and its **variants**.

---

### Lecture 21: Limitations of PoW and Alternatives (PoS, PoB, PoET)

*(Week 5)*

#### Good things about PoW
- Fully **decentralized** consensus for a **permissionless** network.
- Gives **safety** and **liveness** (finality only eventually).
- Works well for **cryptocurrency**: a free, open marketplace with no bank or government control.

#### Limitations of PoW
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

#### Proof of Stake (PoS)
> In **Proof of Stake**, the chance of creating the next block depends on the **amount of coins (stake) the miner holds**, not on computing work.

- Proposed in **2011** by a member of the Bitcoin forum (no formal paper).
- Idea: start with PoW, then **switch to PoS once coins are widely distributed**.
- PoW: chance depends on **work done**. PoS: chance depends on **coins held** (1% of coins → about 1% of blocks), like shareholding.
- **Why it is more protected**: an attack is **expensive** (you need a majority of coins), and the attacker would **lose value** by attacking.
- **Ways to define stake**:
  - **Randomized selection** using stake (used in NXT and BlackCoin).
  - **Coin age** = number of coins × number of days held (used in Peercoin). Holding coins longer counts more, so a quick buyer cannot attack.

#### Proof of Burn (PoB)
> In **Proof of Burn**, a miner shows proof that they **burned (destroyed) some coins** by sending them to a **verifiably unspendable address**.

- It is "expensive" like PoW, but wastes **digital currency**, not real computing power, so it is claimed to be more **energy efficient**.
- It burns coins that were **mined using PoW**.

#### Problem with PoS and PoB
- Both depend on **coins mined by PoW**. So they **cannot be used to bootstrap** a new network. You must start with PoW and move later.

#### Proof of Elapsed Time (PoET)
> In **Proof of Elapsed Time**, every participant **waits for a random amount of time**, and the **first one whose timer finishes becomes the leader** and proposes the block.

- Proposed by **Intel**, used in **Hyperledger Sawtooth**.
- Problem: how do we know the participant **really waited** and did not cheat?
- Solution: use hardware, **Intel SGX (Software Guard Extensions)**, a **Trusted Execution Environment (TEE)**.
  - The system is split into an **untrusted world** (normal apps) and a **trusted world** (hardware-protected).
  - The trusted code cannot be changed by the rest of the system, and the hardware gives an **attestation** (a signed proof) that it ran correctly (e.g., that the full wait time passed).
  - Other TEEs: **ARM TrustZone**.
- PoET **can bootstrap** a network, but works **only on special hardware** (Intel SGX).

#### Summary and trade-offs
- PoW is costly. PoS and PoB are cheaper but **cannot bootstrap**. PoET can bootstrap but **needs special hardware**.
- "No free lunch": choose by your application's needs.
- All of these are for **open (permissionless)** networks. Enterprise (closed) networks need other mechanisms, which come next. Even then some assumption such as "enough honest participants" (about **33%** for classical BFT, to be covered later) is needed.

---

## 7. Smart Contracts and Permissioned Blockchains

*Smart contracts, blockchain generations, permissioned model, state machine replication.*

### Lecture 12: Smart Contracts and Permissioned Blockchain

*(Week 3)*

#### Smart contract
> A **smart contract** is a contract or code that is **executed automatically** over a **decentralized platform**.

#### Problems with the traditional way (centralized cloud)
- Two parties agree on a contract and run it on a cloud platform. Problems:
  1. How do you check that the **inputs are valid**?
  2. A user can later **deny** submitting an input, or claim someone **impersonated** them.
  3. You must **trust the third party** (the cloud). An attacker on the cloud could change the computation.

#### Example code (lecture)
- `pay(sender, receiver, amount)`: if the sender has less than the amount → return −1 (failure). Otherwise deduct from the sender, add to the receiver, return 1 (success).
- `deliverGoods(count, pricePerCount)`: calls pay. If payment succeeds, schedule the logistics and return 1. Otherwise return 0.

#### How decentralized execution works
- Any code can be seen as a **state machine**. After each step the **state** changes (e.g., sender balance, receiver balance, count).
- The **state of execution is stored on the blockchain**, so everyone knows how far the code ran and where it continues.
- The contract is submitted to the blockchain instead of a central server. Other nodes **monitor and verify** the execution.
- This solves the three problems above.
- Examples: **Ethereum DApps**, **Hyperledger Fabric**, and the game **CryptoKitties** (game state kept on blockchain, no central game server).

#### Blockchain generations

| Version | What it is |
|---|---|
| **Blockchain 1.0** | Distributed ledger technology (cryptocurrency, financial transactions) |
| **Blockchain 2.0** | **Smart contracts** (code execution on blockchain) |
| **Blockchain 3.0** | **Trustless decentralization** for enterprise (permissioned blockchain) |

#### Problem with Proof of Work for enterprises
- PoW works in an open network, but has **high transaction latency** and **low throughput**.
- Bitcoin takes about **10 minutes per block**. Ethereum takes a few seconds to a few minutes.
- Enterprise applications (like supply chain) need **real-time logging**, **high throughput** and **low latency**. Delays can allow fraud.

#### Permissioned blockchain
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

### Lecture 26: Consensus in Permissioned Blockchain and State Machine Replication

*(Week 6)*

#### Permissioned (closed) blockchain model
- Users are **authenticated beforehand**. An authentication mechanism controls who joins and leaves.
- **Membership Service Provider (MSP)**: gives a node or person the authentication key so it can prove it is a valid member and join the network.
- **Everyone knows who the other participants are**, so message passing is possible (unlike an open network).
- But participants are often **competitors**, so they **do not trust each other** and may behave maliciously. That is why we **still need consensus and security**.
- Typical use: **business applications / contracts among a closed set of participants**.

**Example: provenance tracking in a supply chain (grocery)**
- Farmers → wholesalers → distributors → cold storage → market. Many middlemen, many players.
- A blockchain gives a **common coordination platform** where all players can share reliable information (demand, supply, planning).

#### Smart contract (definition)
> A **smart contract** is a **self-executing contract** in which the **terms of agreement between buyer and seller are written directly into lines of code**.

#### Executing a smart contract on a closed network
1. **Store the contract on the blockchain.**
2. When an **event is triggered** (e.g., goods delivered or money transferred), **execute the code locally** at a peer.
3. The output is turned into a **transaction** (e.g., "20 tons of potatoes transferred from seller A to buyer B").
4. Other **peers validate** the transaction (they have the contract code too).
5. If valid, it is **committed to the blockchain**. This commit can **trigger the next event** (e.g., payment).

**Do all peers need to execute the code?** No. Execute it on a **subset of nodes** and make sure the **same resulting state is propagated** to all nodes.
- A **majority of peers must agree on the state**.
- Peers act as **witnesses** by **digitally signing** the proposal. A proof that a majority signed shows the information is valid, so it can be committed.

#### State Machine Replication (SMR)
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

## 8. Classical Consensus: Paxos, Byzantine Faults and PBFT

*CFT, Paxos, Byzantine Generals, PBFT, quorums, view change.*

### Lecture 27: Crash Fault Tolerance and Introduction to Paxos

*(Week 6)*

#### Why SMR works as consensus for permissioned blockchain
1. The network is **closed**, so nodes know each other. Each node can be a **replica**. If replicas agree on the state, nodes agree on the value.
2. **No mining overhead.** Nodes just **pass messages** (no proof of work, stake, burn or elapsed time needed). Everyone is already a member of the consensus group.
- Consensus is still needed because **machines can be faulty or malicious**.
- **Cryptography helps**: digital signatures and hashes can be combined with classical algorithms to **relax some assumptions**.
- Classical algorithms used: **Paxos, Raft, Byzantine agreement protocols (e.g., PBFT)**. All are based on state machine replication.

#### Types of faults (recap)
1. **Crash fault**: a node stops operating (hardware or software failure).
   - In an **asynchronous** system you cannot tell whether a silent node **crashed** or its message is **delayed**.
   - You only **do not receive** a message. You never receive a **wrong** one.
2. **Byzantine fault**: a node behaves maliciously (e.g., sends different information to different peers).
   - Harder to handle, and more relevant to blockchain.
   - **BFT algorithms are built on CFT algorithms**, so we learn CFT first.

#### FLP and priority
- In asynchronous systems, safety and liveness cannot both be guaranteed, even with one crash fault.
- CFT algorithms like **Paxos**, and some BFT algorithms like PBFT, **give priority to safety over liveness**. That means they reach **consensus finality** (unlike PoW).

#### Properties of consensus (CFT)
| Property | Meaning |
|---|---|
| **Validity** | If all correct processes propose the same value v, then any correct process decides v |
| **Agreement** | No two correct processes decide differently |
| **Termination** | Every correct process eventually decides |

**Compared with PoW:** validity is unlikely (miners propose different blocks). Agreement (safety) is not guaranteed immediately. Termination (liveness) is what PoW prioritizes.

#### CFT algorithms
- **Paxos**: the most fundamental CFT consensus algorithm, by **Leslie Lamport**.
- **Raft**: simpler than Paxos. Used in **Hyperledger Fabric for transaction ordering** (when there are no Byzantine nodes).

#### Dinner example (5 friends, asynchronous)
- A friend asleep (crashed) does not break consensus if the **majority** (3 of 5) agrees. With 5 nodes, at most **2** can be faulty.
- **If there are f crash faults, you need at least 2f + 1 nodes** in an asynchronous CFT system.

#### About Paxos
- A **family of algorithms** for consensus in asynchronous systems (we study the basic one).
- Proposed by **Lamport in 1989**, accepted (ACM Transactions on Computer Systems) in **1998**. Paper title: **"The Part-Time Parliament"**. Lamport received the **Turing Award in 2013**.

---

### Lecture 28: The Paxos Algorithm

*(Week 6)*

#### Roles
- **Proposer**: proposes a value.
- **Acceptor**: accepts a proposal.
- **Learner**: learns the value at consensus.
- One node can have **more than one role**.

#### Majority
- The **number of acceptors is known** in advance, so the majority is known.
- **Any two majorities always overlap in at least one node.** Example: 5 acceptors → majority 3. With **6 acceptors**, 3 is **not** a majority (two groups of 3 do not overlap), so you need **4**.
- Only **crash faults** exist here: you either get the correct message or none.

#### ID and state
- Each proposal has a **unique id** (epoch number). Can be a timestamp or a hash of timestamp and proposer id.
- The id acts as the **state**. It helps ignore old or delayed messages.
- **A single Paxos run reaches one consensus.** For many consensus decisions, use **Multi-Paxos**.
- **Consensus is on the value, not on the id.**

#### Paxos steps
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

### Lecture 29: Safety and Liveness of Paxos, Leader Election, Multi-Paxos

*(Week 6)*

#### Safety (why Paxos is safe)
- With f faults, you need **2f + 1** acceptors. Example: 3 acceptors tolerate 1 crash.
- In an asynchronous network, messages can arrive **out of order** (e.g., a proposer closer to an acceptor).

**Case 1:** Acceptor 3 gets **prepare 50** first and promises 50, then gets **prepare 100** and promises 100. Acceptors 1 and 2 promised 100 first and **ignore prepare 50**. Prepare 50 does **not get a majority**, so proposer 1 (id 100) goes ahead.

**Case 2:** Acceptors 2 and 3 get **prepare 50** first (promise 50), so proposer 2 gets a majority and sends **accept request 50**. But before it arrives, they have **already promised 100**, so they **ignore** accept request 50. Proposer 1 (id 100) succeeds.

> **Majority voting + ids ensure safety**, even with delays, reordering and crash faults.

#### Liveness (not guaranteed)
- Proposers can keep **competing with higher ids** (prepare 100, then 150, then 200 ...). Each time the earlier proposer's accept request is ignored, so progress may **never finish**.
- So Paxos has **no termination guarantee**: **safety is ensured, liveness is compromised**. This agrees with the **FLP impossibility**.
- A lower-id accept request will not be accepted by a majority. A higher-id request with a different value is handled because the common node tells the earlier accepted value.

#### Applications and extensions
- **Leader election**: use standard Paxos where the value is "I will be the leader". Once elected, a leader makes later consensus easier. **Raft** works on this idea.
- **Multi-Paxos**: runs **many Paxos instances**, each with a **round number**. Value agreed in round n is fixed; then start round n + 1 from scratch.
  - Uses: **blockchain** (agree on each block) and **replicated databases** (commit each transaction).

#### Limitation
- Paxos works only for **crash faults**. A **malicious node** can break it (next lecture).

---

### Lecture 30: Byzantine Faults and the Byzantine Generals Problem

*(Week 6)*

#### Agreement vs consensus
- **Agreement** is a temporary or partial step. **Consensus** may need multiple rounds of agreement. Example: Paxos has two agreement rounds (id, then value).

#### Why Paxos fails with a malicious node
- Acceptor 2 already promised 100, but then **also sends promise 50** (it should have ignored 50).
- Now both proposers think they got a majority, and both send accept requests (dinner and movie).
- The malicious acceptor **accepts both**: it tells proposer 1 "dinner" and proposer 2 "movie".
- The two proposers believe different values were agreed, so **safety is violated**.

#### Byzantine Generals Problem (Lamport)
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

#### Byzantine Fault Detection vs Tolerance
| | Detection (BFD) | Tolerance (BFT) |
|---|---|---|
| Goal | Notice that some Byzantine behavior happened | **Reach consensus anyway**, and ideally know who is faulty |

#### Key result
> **To tolerate f Byzantine (faulty) nodes, you need at least 3f + 1 nodes in total.**

- 1 faulty node → **4 nodes** needed. (3 nodes: detection only. 4 nodes: consensus.)

**Intuitive proof**
- Take 3f nodes split into three groups: **PL** (f correct), **PF** (f faulty), **PR** (f correct).
- The faulty group tells PL "0" and PR "1", creating a **partition**. PL and PR cannot communicate directly, so each side sees an **equal split**, with no clear majority.
- **Adding one extra correct node** to one side **breaks the tie**. So the total needed is **3f + 1**.

**Compare:** crash faults need **2f + 1** nodes. Byzantine faults need **3f + 1** nodes.

#### Next
- **PBFT (Practical Byzantine Fault Tolerance)**, used in **Hyperledger Fabric**.

---

### Lecture 31: PBFT (Practical Byzantine Fault Tolerance)

*(Week 7)*

#### Recap
- To tolerate **f faults** you need **3f + 1 nodes**. Here **f counts all faults together** (crash, link and Byzantine), not only Byzantine ones.

#### LSP algorithm (first Byzantine agreement algorithm)
- From the paper **"The Byzantine Generals Problem"** by **Lamport, Shostak and Pease**. This is the "relay the message and take a majority" method seen in Lecture 30.
- Assumptions (not realistic):
  1. **Synchronous** network.
  2. **Reliable channel** (messages never lost).
  3. **Fully connected** network.
  4. The receiver **always knows the sender's identity**.
- It formally proved the **3f + 1** requirement, but it is not used in real networks.

#### PBFT
> **PBFT** is a Byzantine agreement protocol for **asynchronous** environments that removes most of the unrealistic assumptions of LSP.

- By **Miguel Castro and Barbara Liskov**, published at **OSDI 1999**: "Practical Byzantine Fault Tolerance".
- **Practical** because:
  1. Works in an **asynchronous** network.
  2. Uses **digital signatures** to authenticate senders (so receivers need not know the sender beforehand).
  3. Uses a **hash (digest)** with each message for **integrity**.
  4. **Low overhead**, easy to implement.
- Gives **priority to safety over liveness** (liveness needs extra assumptions, next lecture).
- Used by many permissioned blockchains (the lecture names **Tendermint** and **Hyperledger Fabric**).

#### Setup
- Based on **state machine replication**, with **3f + 1 replicas**.
- The system moves through configurations called **views**, each identified by a unique integer **v**.
- In each view: **one primary** (like the leader or proposer) and the rest are **backups** (like acceptors).
  - Unlike Paxos, there is a **single primary**, not multiple proposers.
- Choosing the primary: any leader election method (e.g., Paxos), or a **predefined order** (if one fails, the next becomes primary).
- When the primary is faulty, the **view changes** (v → v + 1) with a new primary. Messages from an **old view are dropped**.
- **Clients** are outside the protocol. They send requests and wait for replies.

#### Normal operation: three phases

**Phase 1: PRE-PREPARE**
1. Client sends a request to the **primary**.
2. Primary orders the requests and assigns a **sequence number n**.
3. Primary **multicasts** `<PRE-PREPARE, v, n, d>` signed with its **private key**, together with the message **m**.
   - v = current view, n = sequence number, d = digest of m.

**A backup accepts PRE-PREPARE if:**
- The **signature** is correct and d is the digest of m.
- The backup is in the **same view v**.
- It has **not accepted a different pre-prepare with the same n** in view v.
- **n is within a threshold** (not too old). This prevents **replay attacks**.

**Phase 2: PREPARE**
1. Each backup that accepts the pre-prepare **multicasts** `<PREPARE, v, n, d, k>` (signed) to **all other replicas including the primary**.
2. This works like a **vote**: "I agree with the primary's order".
3. A replica accepts prepare messages if the **signature is correct, the view matches and n is within the threshold**.
- Messages may arrive **out of order** (a prepare may arrive before the pre-prepare), so replicas must **keep track** of everything received.
- The pre-prepare and prepare phases make the non-faulty replicas agree on a **total order** of requests.

> **Total order**: one final order everyone agrees on (like block 1, block 2, block 3 ...). A **partial order** allows several valid orders (a DAG).

**Phase 3: COMMIT**
- A request is **prepared** when a replica has the pre-prepare and **2f matching prepare messages from different backups**. Adding its own, that is **2f + 1 votes**.
- The replica then multicasts `<COMMIT, v, n, d, k>` (signed).
- The request is **committed** at a replica when it has sent its commit and received **2f commit messages from others** (again 2f + 1 total).
- Then it executes and **replies to the client**. The lecture says the client waits for **2f + 1** matching replies.
  > *Note (not from the lecture):* the original PBFT paper says the client waits for **f + 1** matching replies. Follow your slides for the exam.

#### Quorum
> A **quorum** is the **minimum number of votes** a distributed transaction needs in order to commit. (Proposed by **David Gifford, 1979**; used in commit protocols and replica management.)

PBFT uses a **Byzantine dissemination quorum** with two properties:
1. **Intersection**: any two quorums share **at least one correct replica**.
2. **Availability**: there is always a quorum with **no faulty replicas**.

**Quorum size = 2f + 1** (out of 3f + 1 replicas).

**Why 2f + 1?**
- **If all f faults are crash/network faults**: they send nothing, so you still get **2f + 1 votes from non-faulty nodes**, and you can decide.
- **If all f are Byzantine**: they may send wrong votes. Wait for **2f + 1**. At most f are faulty, so **at least f + 1 are correct**, which is a majority of those 2f + 1.
- **f + 1 votes would not be enough**, because all f of them could be faulty, leaving only one correct vote.
- In an asynchronous network you cannot wait for all 3f + 1 votes (some may be delayed), so you wait for **2f + 1 out of 3f + 1**.

---

### Lecture 32: PBFT Safety, Liveness and View Change

*(Week 7)*

#### Three rounds recap
**Pre-prepare → Prepare → Commit** (each uses the 2f + 1 quorum), then reply to the client.

#### Safety
- Unlike Paxos, PBFT has a **single leader (primary)**, so there is **no ping-pong effect** between competing proposers.
- With a **2f + 1 quorum**, even if f nodes are faulty (crash or Byzantine), at least **f + 1 correct votes** support the result.
- So **PBFT is safe in an asynchronous environment**, with up to f faults (crash plus Byzantine).

#### Liveness problem
- Safety assumes the **primary is non-faulty**. If the primary **fails**, nobody proposes, and the system **stops making progress**.
- In a **pure asynchronous** system a replica cannot tell whether the primary **failed**, is **delayed**, or just **has nothing to send**. It would wait forever. (FLP says safety and liveness cannot both be guaranteed.)

#### Weak synchrony (the assumption used for liveness)
- Pure asynchrony (infinite delay) is **not practical**. PBFT assumes **weak synchrony**:
  - The **sender and receiver are correct**, and the sender **keeps retransmitting** until delivered (like **TCP**).
  - Congestion does not last forever, so there is an **upper bound T** on message delay (T can be 3 seconds or 10 minutes, depending on the network).
- This sits **between synchronous** (no delay) **and asynchronous** (infinite delay).
- The **primary periodically sends dummy (heartbeat) messages** even if it has nothing to propose, to show it is alive.
- If backups hear nothing from the primary within **T**, they treat it as faulty.

#### View change protocol
> **View change** replaces a faulty primary with a new one, giving **eventual liveness**.

**Trigger:** a backup **starts a timer** when it receives a request (if not already running). It stops the timer when the request is executed. If the **timer expires in view v**, it starts a view change to **v + 1**.

**View-change message:** `<VIEW-CHANGE, v+1, n, C, P, k>`
| Field | Meaning |
|---|---|
| **v + 1** | The new view being proposed |
| **n** | Sequence number of the **last stable checkpoint** (messages up to n are committed) |
| **C** | **2f + 1 valid checkpoint messages** (prepare/commit proof) showing the checkpoint at n |
| **P** | For each request that was **prepared** (pre-prepare and prepare done) with a sequence number **greater than n** but **not committed** |
| **k** | The replica sending it |

- C and P let every replica agree on **which messages are committed** and **which are only prepared**.

**Steps**
1. Replicas **multicast VIEW-CHANGE** messages.
2. When the next primary receives **2f + 1 view-change messages** (quorum), it takes over as the new primary.
3. Replicas send **view-change acknowledgements** to the new primary.
4. The new primary broadcasts a **NEW-VIEW** message, which **starts view v + 1**.
5. PBFT continues in rounds in the new view.

**Choosing the next primary** (not fixed by PBFT):
- **Round robin** (predefined: if replica R fails, replica R + 1 is next), or
- A **leader election** mechanism (e.g., Paxos-style).

#### Conclusion
- PBFT is **safe with a 2f + 1 quorum in an asynchronous environment**.
- **Liveness** needs the **weak synchrony** assumption and the **view change protocol**.

---

## 9. Ethereum

*geth, transactions and gas, DApps and web3.js, Solidity and Remix.*

### Lecture 22: Introduction to Ethereum and Go Ethereum (geth)

*(Week 5)*

#### Ethereum
- A **permissionless blockchain platform** like Bitcoin, but it lets users send cryptocurrency for a small fee **and** run **smart contracts** (applications "that everyone can use and no one can take down").
- Development started around **2013**, launched **July 2015**.
- It is the most popular cryptocurrency after Bitcoin. The cryptocurrency is **ether**.
- It is **decentralized**: there is no central Ethereum server.

#### Ethereum node and client
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

#### Go Ethereum (geth)
- The **official Go implementation** of the Ethereum client. It is a **command-line** client.
- Used to connect to the mainnet, test networks, or your own network.
- **End users do not use geth directly.** Developers build apps on top of it using SDKs like **web3.js** or **ethers.js**.
- geth exposes **JSON-RPC endpoints** over **HTTP, WebSocket, or IPC**.

#### Installing geth (Ubuntu)
1. `sudo add-apt-repository -y ppa:ethereum/ethereum`
2. `sudo apt-get update`
3. `sudo apt-get install ethereum`
4. `geth version` to check.

#### Accounts
- `geth account list`, `geth account new`, `geth account update`, `geth account import`.
- Each account has a **public key (address)** and **private key**.
- The **private key is not stored in plain text**; it is **encrypted with your password** and kept in the **keystore** folder (`~/.ethereum/keystore`).

#### Test networks
- Mainnet transactions need real ether (gas), so use **test networks** for practice.

| Test network | Consensus | Note |
|---|---|---|
| **Ropsten** | Proof of Work | Slower, same as mainnet |
| **Rinkeby** | Proof of Authority | Faster |
| **Goerli** | Proof of Authority | Faster (used in the lectures) |

#### Sync modes

| Mode | What it does |
|---|---|
| **Full** | Downloads **all blocks** (headers, transactions, receipts) and **executes every block** to build the state. Most resource-heavy |
| **Fast / Snap** | Downloads headers and receipts and verifies them. **Snap is the default** |
| **Light** | Downloads headers, **verifies only some data randomly**, and relies on other full nodes. **Fastest and lightest** |

- Connect to Goerli in light mode: `geth --goerli --syncmode light`
- Add `--http` to enable **RPC over HTTP** (default `127.0.0.1:8545`).

#### Two ways to use geth's API
- **IPC / JavaScript console**: more functions, but needs **direct access** to the machine running geth.
- **RPC over HTTP**: remote apps can connect, but has **security considerations** (you expose your node).

#### Querying a balance (RPC over HTTP)
- Send an HTTP **POST** (e.g., with `curl`) with a **JSON payload**: `jsonrpc: "2.0"`, `method: "eth_getBalance"`, `params: [address, "latest"]`, `id`.
- The result is in **hexadecimal** (e.g., `0x0` means 0).
- Balance unit is **wei**: **1 ether = 10^18 wei**. Divide by 10^18 to get ether.

---

### Lecture 23: Ethereum Transactions, Gas, and Faucets

*(Week 5)*

#### Transactions
- **Queries only read** the ledger. A **transaction** **writes** to it.
- An **Ethereum transaction** is a **cryptographically signed instruction from an existing account** that updates the state of the network.
- Simplest example: transfer ether from one account to another.
- You need two things:
  1. **Access to the account** (private key) to sign.
  2. **Gas** to pay the fee.

#### Gas
> **Gas** is the **fee paid in ether** for the computational resources needed to execute a transaction.

- Miners/verifiers must validate and execute your transaction, so every transaction costs gas.
- On the **mainnet**, buy ether from an exchange (with real money) or earn it by mining.

#### Faucet (for test networks)
- A **faucet** gives **free test ether** so you can pay gas on test networks.
- It is **rate limited** to stop abuse (a DoS attack through unlimited free ether).
- **Goerli faucet**: post a **tweet containing your account address**, paste the tweet URL into the faucet, and choose:
  - 6 ether for 1 day, or 15 ether for 3 days, or 37.5 ether for 9 days.
  - You cannot request again for that period. You would need a new social media account.

#### Using accounts on a test network
- Create an account on Goerli: `geth --goerli account new`.
- To reuse a mainnet account, **copy its keystore file** from `~/.ethereum/keystore` to `~/.ethereum/goerli/keystore`.
- Save the password in a file (e.g., `pw.txt`).
- **Unlock the account** when running geth:
  `geth --goerli --syncmode light --http --allow-insecure-unlock --unlock <address> --password pw.txt`

#### Sending ether with RPC
- Method: **`eth_sendTransaction`** (a POST request).
- Parameters: **`from`**, **`to`**, **`value`** (amount in **hexadecimal wei**; 0.1 ether = 0.1 × 10^18 wei, converted to hex).
- The response is the **transaction hash**.
- The same method can also **deploy smart contracts**.

#### Monitoring a transaction
- Use **Etherscan** (e.g., the Goerli Etherscan site). The status goes from **Pending** to **Success** once it is mined into a block.
- **`eth_getTransactionByHash`**: gets the transaction details (block hash, block number, transaction index).
- **`eth_getBlockByNumber`**: gets the block details. The block number must be given in **hexadecimal**. The output includes difficulty, gas limit, gas used, hash, nonce, miner, and the list of transactions.

---

### Lecture 24: Decentralized Applications (DApps) and web3.js

*(Week 5)*

#### DApp
> A **DApp (decentralized application)** is an application that runs on a decentralized network, with no central server or authority.

**Two components of an Ethereum DApp:**
1. **Smart contract**: deployed on the Ethereum network. Its code is executed independently by the participants, and the output is decided by **consensus**.
2. **DApp UI (user interface)**: lets users run transactions and queries on the contract.

- The **DApp UI sits between the end user and the Ethereum node** (geth, or services like Infura).

#### web3.js
> **web3.js** is the **Ethereum JavaScript API**: a collection of libraries to interact with a geth node easily (instead of writing manual POST requests).

- It connects to geth through **RPC over HTTP, WebSocket, or IPC**.
- It needs **Node.js** and **npm**. Install: `npm install web3`.
- Check: `var Web3 = require('web3'); console.log(Web3.version)`.

#### Connecting
```javascript
var Web3 = require('web3');
var web3 = new Web3('http://localhost:8545');
```
- Port **8545** is where geth opened the RPC endpoint (started with `--http`).

#### Querying a balance
```javascript
web3.eth.getBalance(address).then(console.log);
```
- Returns a **promise** (asynchronous). The result prints when the query finishes.
- The balance is shown in **decimal wei** (web3 converts it from hexadecimal automatically).

#### Sending a transaction
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

### Lecture 25: Ethereum Smart Contracts, Solidity and Remix

*(Week 5)*

#### Smart contracts in Ethereum
> **Smart contracts** are programs executed in a **decentralized setting**. They read data from the ledger, process it, and **write results back** to the ledger. The result depends on the **consensus** of the independent participants executing it.

**Properties:**
- A deployed contract gets **its own address** (it acts like an **account**). It can **hold a balance** and **send transactions**.
- It is **not controlled by any single user**; it runs by its own logic.
- Users interact by **sending transactions that call a function** defined in the contract.

#### Execution model
- Ethereum is a **replicated (distributed) state machine**. A transaction moves the ledger from one **state** to another. Contracts can have their own **state variables**.
- Execution must be **deterministic**. Every participant executes the contract independently, and if results differed they could not reach consensus.

#### Development flow
1. Write the contract in a high-level language: **Solidity** (most popular) or **Vyper**.
2. **Compile** with a smart contract compiler (e.g., **solc**) → **bytecode** + **ABI**.
3. **Deploy** the bytecode to a network (mainnet or test network). The contract gets an **address**.
4. **Execute** via **web3.js** using the **ABI** and the **contract address**.

- **EVM (Ethereum Virtual Machine)** executes the bytecode.
- **ABI (Application Binary Interface)** describes the contract's functions and parameters. Without the ABI you cannot call its functions from web3.js.

#### Solidity
- High-level, **statically typed**, supports **inheritance**, **libraries** and complex user-defined types.
- Syntax influenced by **JavaScript and C++**.

#### Example: Storage contract
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

#### Tools
- **Remix editor**: browser-based IDE to write, compile, test and deploy Solidity (has the compiler built in; shows ABI and bytecode).
- **MetaMask**: a browser extension **wallet** that lets Remix connect to the Ethereum network. It holds accounts and works across mainnet and test networks.
- **JavaScript VM** (in Remix): an emulator in the browser for testing without a real network.
- **Injected web3**: deploys to a real network through MetaMask (MetaMask shows the gas fee estimate and asks you to confirm).

#### Using a deployed contract with web3.js
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

#### Summary
- A **DApp = smart contract (Solidity, deployed on the network) + application code (web3.js UI)**.
- Tools involved: **geth**, **web3.js**, **Remix**, **MetaMask**.

---

## 10. Enterprise Blockchain and Hyperledger Fabric

*Enterprise value, Hyperledger projects, Fabric installation, architecture, chaincode, applications.*

### Lecture 33: Enterprise Blockchain and the Hyperledger Project

*(Week 7)*

#### Recap and goal
- So far: consensus for **permissionless** blockchains (PoW and alternatives) and **permissioned** ones (Byzantine agreement, PBFT). Now: how these apply to **enterprise blockchain**, leading to **Hyperledger Fabric**.

#### Beyond Bitcoin
- Blockchain was made famous by **Bitcoin**, but the application space is **much bigger** and includes **non-financial** uses that do not need cryptocurrency. **Smart contracts** let code run automatically in a decentralized way, which suits enterprises.

#### Why enterprises need blockchain (trusted third party problem)
- Traditional model: enterprises share data through a **trusted third party**. But trust is not really built in, and there is a **cost**.
- **Example: e-commerce marketplace** (Amazon, Flipkart, eBay). The platform validates sellers, but takes a **share of profit**, which **raises prices** compared to a local market.
- A **decentralized marketplace** raises the question: **who validates a seller's authenticity** and removes a fraudulent seller? Blockchain lets participants share information and do this without a central party.

#### Example: auditing and asset transfer in a business network
- Parties A, B, C, D each keep their own financial records (usually held with banks). **Auditors** must collect records from each party and from the banks and **cross-check manually** (e.g., A says it bought goods from B for ₹1 lakh with tax paid, so B's record must match).
- This is **inefficient, expensive and vulnerable**.
- With blockchain, **all parties, banks and auditors are on one platform** and all transactions are logged. The auditor can **verify automatically**, with **provenance, immutability and finality**. You get a **verifiable, immutable log** with no trusted third party.

#### Four pillars of blockchain for business
| Pillar | Meaning |
|---|---|
| **Shared (distributed) ledger** | An **append-only** record shared across the business network. Everyone keeps and shares it, so no one has to ask "who holds the information?" |
| **Smart contracts** | Business terms embedded in transactions and **executed automatically** on events (e.g., uploading an invoice triggers delivery of goods). Less manual effort and risk, more transparency |
| **Security / privacy** | Right **visibility** for each stakeholder. Transactions are **secure, authenticated and verifiable** |
| **Consensus** | All parties **agree** on the network-verified transactions, so everyone sees the same information |

#### Benefits for business
- **Time**: transaction time falls from **days to near instantaneous**.
- **Cost**: removes **intermediaries**.
- **Risk**: less **tampering, fraud and cybercrime** (tamper-proof platform).
- **New business models**: e.g., **IoT in a supply chain** logs product state on the blockchain, and a smart contract can react (e.g., if onions spoil in transit, **redirect the vehicle** to a nearby place).

#### Degrees of decentralization
- Today's systems: **100% centralized** ledgers. **Bitcoin**: **permissionless public**, 100% decentralized. **Enterprise** use cases sit in between:
  - **Permissioned public shared**: anyone can participate but must be **pre-authenticated** (e.g., e-commerce **sellers**).
  - **Permissioned private shared**: a **fixed consortium** (e.g., **supply chain**, the **petroleum** example).

#### Permissionless vs permissioned
| | Permissionless | Permissioned |
|---|---|---|
| Access | **Open** read and write | **Permissioned** write; participants pre-authenticated |
| Scaling | Many nodes, **not** transaction throughput | **Throughput**, **not** many nodes |
| Consensus | **PoW / PoS** | **Closed membership**: Byzantine agreement protocols |
| Identity | **Anonymous / pseudonymous** | **Node identities known**; transaction identities can be private, anonymous or pseudonymous |
| Assets | **Native assets** (coins) | **Any asset or data/state** |

#### Hyperledger
> **Hyperledger** is a **Linux Foundation** collaborative project to advance blockchain technology by building a **cross-industry open standard for distributed ledgers**. Its umbrella is called the **Hyperledger Greenhouse**.

- Projects include **Fabric, Grid, Indy, Aries, Sawtooth, Besu, Burrow** and others, each with different decentralization models and uses (e.g., **Indy** for **identity management**).
- Community: **300+ members**, including tech giants (Microsoft, Intel and others) and financial institutions.

#### Hyperledger Fabric
- An **enterprise-grade permissioned distributed ledger platform** that is **modular**: **plug-and-play** components for **consensus, privacy and membership services**.
- Supports a **"network of networks"**: members keep **private transactions and confidential contracts** with agreed parties **without a central authority**. If a member is not a party to a transaction, it does not appear on their ledger.
- Emphasis: **ledger, smart contracts, consensus, confidentiality, resiliency, scalability**.
- **Version 1.0 released in July 2017**. At the time of the lecture, about **159 developers from 27 organizations** (open source, anyone can contribute).
- Next lectures: a hands-on demo of building an application on Fabric.

---

### Lecture 34: Hyperledger Foundation and Installing Fabric

*(Week 7)*

#### Hyperledger Foundation
> An **open-source community** (umbrella organization) hosting many **permissioned blockchain** frameworks and tools for **enterprise-grade** blockchain deployments.

- Enterprise use case: **companies collaborate in a closed group** (a **consortium**). Members **know each other** but **do not fully trust each other**, and there is **no central trusted authority**. The platform provides a **distributed shared ledger** using permissioned consensus.

| Project | Purpose |
|---|---|
| **Fabric** | Building **consortium** blockchain networks |
| **Sawtooth** | A DLT platform (uses PoET, from Lecture 21) |
| **Indy** | **Identity management** (decentralized identifiers, verifiable credentials and presentations) |
| **Burrow** | Permissioned platform that runs **EVM smart contracts** with a **BFT consensus** |
| **Cello** | Tool: **operational dashboard** for blockchains |
| **Explorer** | Tool: view, invoke and **query blocks** |

- Cello and Explorer work on top of **more than one** blockchain platform.

#### Hyperledger Fabric
- **Open-source, enterprise-grade, permissioned DLT platform.**
- **Modular**: you can **plug in your own consensus protocol or membership service**.
- For building blockchain-based products and applications with **smart contracts**.
- Smart contracts (**chaincode**) can be written in **general-purpose languages: Java, Go, Node.js**. (Ethereum needs Solidity.)

#### Installation (Ubuntu) prerequisites
1. **git** (version control)
2. **curl** (HTTP client)
3. **Docker**: containers isolate each organization's processes, so a whole multi-organization network can run on one machine.
4. **Docker Compose**: manages the containers of a Fabric network.
5. **Go** (the lectures write chaincode in Go).

**Install steps**
- git and curl: `sudo apt install git curl` (check with `--version`).
- **Go**: download the tarball, extract to `/usr/local/go` (`sudo tar -C /usr/local -xzvf <file>`), then add it to `PATH` (also in `~/.bashrc`).
- **Docker**: install `ca-certificates`, `gnupg`, `lsb-release`; add Docker's GPG key and repository; `sudo apt update`; install **docker-ce, docker-ce-cli, containerd.io**.
- **Post-install** (needed for Fabric): create the **docker group** (`sudo groupadd docker`) and **add your user** to it (`sudo usermod -aG docker $USER`), so Docker works **without sudo**.
- **Docker Compose**: download the binary and make it executable (`chmod +x`).
- Check that the **versions match** the Fabric documentation.

#### Installing Fabric itself
Fabric is a collection of **samples, binaries and Docker images**.
- **Fabric samples**: sample programs and scripts (test networks, chaincode, apps).
- **Fabric binaries**: executables, e.g. **cryptogen** (generate keys for participants), **configtxgen** (generate the **genesis block**), **peer** (execute and query transactions), plus monitoring tools.
- **Docker images**: each Fabric component runs **containerized** (isolated per organization).

**One command** (inside a new folder): `curl -sSL <install-script-url> | bash -s <fabric version> <fabric-ca version>` (e.g., 2.2.4 and 1.5.2).
- It **clones fabric-samples**, **downloads the binaries** and **pulls the Docker images**.
- Then add the `bin` folder to `PATH` (also in `~/.bashrc`).
- Test: `cryptogen`, `configtxgen`, `peer version`.

---

### Lecture 35: Fabric Architecture, Test Network and Chaincode

*(Week 7)*

#### Key components of a Fabric network

**Ledger**
- A **blockchain** (blocks linked by the previous block's hash) plus the **world state**.
- **World state** = the **current state** of the ledger (the latest values of the data).

**Channels**
- One Fabric network can have **multiple ledgers**, each called a **channel**.
- A **subset of organizations** can form a channel and share a **private ledger**. Other organizations cannot see it.
- **Each channel has its own ledger and world state.**

**Peer**
- The component **each organization uses to interact with the ledger**.
- **Executes transactions**, **queries the ledger**, **runs chaincode**.
- Gives the **interface for client applications** (through the **Fabric SDK**).
- Sends **events** (new committed transactions or chaincode events) back to the client application.

**Chaincode**
- Fabric's name for **smart contracts**, deployed on peers.

**MSP (Membership Service Provider)**
- Issues **identities** to the different components or participants **within an organization**, so each can transact with its own identity.
- **CA (Certificate Authority)**: one implementation of an MSP. It issues certificates and credentials.

**Orderer**
- Takes transactions from peers, **orders them, compiles them into blocks**, and commits them through the **consensus** process.
- The **default** implementation is **Raft**.

#### The test network
- Fabric ships a **test network** for development and testing.
- Default setup: **2 organizations**, **1 peer each** (optionally 1 CA each), and **1 orderer**. All run as **Docker containers** on one machine.
- Control it with the script **`network.sh`** in `fabric-samples/test-network`.

| Command | What it does |
|---|---|
| `./network.sh up` | Generates configuration and crypto material, starts the containers |
| `./network.sh down` | Stops containers and cleans up |
| `./network.sh createChannel` | Creates a channel (default **mychannel**; use `-c <name>` for another) |
| `./network.sh deployCC ...` | Deploys chaincode |

- **`docker ps`**: lists running containers (Org1 peer, Org2 peer, the orderer, a fabric-tools container).
- **`docker logs <container id>`** (add `-f` to follow): see logs. At first the peer log says "no active channels".
- You **must create a channel first**. The ledger exists per channel, and transactions are made in a channel.

#### Assets
- Fabric has **no built-in cryptocurrency**. It works with **assets**: any data stored on the ledger, usually something of value (land records, cars, etc.), with properties like owner and value.

#### Deploying chaincode
`./network.sh deployCC -ccn <name> -ccp <path to chaincode source> -ccl go`
- **-ccn** = chaincode name, **-ccp** = source path, **-ccl** = language.
- Example: **asset-transfer-basic** (from fabric-samples). It stores sample assets with an owner and value.
- The chaincode is **installed on each peer** (two instances) and runs in **separate containers** (shown as `dev-peer...` in `docker ps`).

#### Invoking and querying chaincode
**Choose the organization** by exporting environment variables:
- `FABRIC_CFG_PATH` (config directory)
- `CORE_PEER_TLS_ENABLED=true`
- `CORE_PEER_LOCALMSPID=Org1MSP`
- TLS root certificate file and MSP config path for that org
- `CORE_PEER_ADDRESS=localhost:7051` (Org1 peer's address)

**Invoke** (changes the ledger; goes through the orderer):
`peer chaincode invoke -o localhost:7050 ... -C mychannel -n <chaincode name> -c '{"function":"InitLedger","Args":[]}'`
- You must give the **orderer address**, TLS options, and the **peer addresses of both organizations** with their TLS certificates.
- Shows "chaincode invoke successful".

**Query** (read only):
`peer chaincode query -C mychannel -n <name> -c '{"Args":["GetAllAssets"]}'`
- `ReadAsset asset6` shows one asset (owner Michael).

**Change the ledger:** invoke `TransferAsset asset6 Christopher`. A new query shows the owner is now **Christopher**. This changes the **world state**.

- Function names (InitLedger, GetAllAssets, ReadAsset, TransferAsset) are **specific to the chaincode**.
- If chaincode errors occur, check the chaincode container's `docker logs`.

**Next lecture:** writing your own chaincode and client applications.

---

### Lecture 36: Writing Fabric Chaincode and the Transaction Flow

*(Week 8)*

#### Fabric smart contracts = chaincode
- To make transactions, you must first define the **data types, rules and processes**. This business logic is written as a **smart contract**, which Fabric **packages as chaincode**.
- Example: a **car contract** with functions **query car** (return details), **transfer** (change the owner from seller to buyer) and **update** (change other properties).

#### Fabric transaction flow
Players: a **client**, several **endorsing peers**, the **ordering service** (Raft or another protocol), and other (committing) peers.
1. A **client** (belonging to some organization) creates a transaction containing: **client id, chaincode id, payload (arguments), timestamp, client signature**.
2. The client sends it to the **endorsing peers**.
3. Each endorsing peer **simulates (emulates) the transaction on its own copy of the ledger**. If the result is correct as per the business logic, it **endorses** it and sends the endorsement back to the client.
4. The client collects the endorsements and sends the transaction (with endorsements) to the **ordering service**.
5. The orderer **collects transactions, puts them in a block** and sends the block to **all peers** (endorsing and non-endorsing, called committing peers).
6. The peers **commit** the block.

#### Chaincode languages and execution
- Fabric provides SDKs (the **fabric contract API**) for **Go, Node.js and Java**. These are general-purpose languages (unlike Solidity in Ethereum).
- Chaincode is installed on **each peer** and runs as a **separate process (container)** from the peer. Each peer has its own copy.

#### Writing a Go chaincode (key-value store)
- `package main`, import `fmt` and the **fabric-contract-api-go/contractapi** package.
- Define the contract type: `type SmartContract struct { contractapi.Contract }`.
- **InitLedger**: `func (s *SmartContract) InitLedger(ctx contractapi.TransactionContextInterface) error` stores a dummy key-value pair with **`ctx.GetStub().PutState(key, []byte(value))`**. Returns an error if `PutState` fails, else `nil`.
- **CreateKey(ctx, key string, val string) error**: stores a key-value pair using **PutState**.
- **QueryKey(ctx, key string) (string, error)**: reads using **`ctx.GetStub().GetState(key)`** and returns the value (empty string if the key does not exist).
- **main()**: `chaincode, err := contractapi.NewChaincode(new(SmartContract))`, then `chaincode.Start()`, checking errors.
- **Stub functions**: **PutState** writes to the **world state**, **GetState** reads from it.
- You can store any data (JSON, XML) by **serializing it into a string**.

**Build steps**
1. `go mod init <module name>`
2. `go get` (fetches required packages)
3. `go build`

**Deploy and test**
1. `./network.sh up`, then `./network.sh createChannel` (mychannel).
2. `./network.sh deployCC -ccn keyvaluechaincode -ccp ../test-chaincode -ccl go`.
3. Set the environment variables (as in Lecture 35) and **invoke** `InitLedger` (no arguments).
4. **Query** `QueryKey` with `testkey` → returns `testvalue`. Querying `nptel` (not stored) gives an **empty string**.
5. **Invoke** `CreateKey` with `nptel` and `blockchain`, then query `nptel` → `blockchain`.

- In recent Fabric versions, **InitLedger is not mandatory**. You can define your own functions directly.

---

### Lecture 37: Fabric Applications, Fabric CA and DApps

*(Week 8)*

#### Fabric application architecture
- Until now we ran chaincode from the **command line** using the `peer` binary. Real applications must access chaincode **programmatically**.
- A **Fabric application** uses the **Fabric SDK** to send transactions through the **peer**, receive the results, and optionally **listen to ledger events**.
- It runs with the **identity of the application developer or the organization**.
- Languages: **Node.js and Java** are best supported. SDKs also exist for **Go and Python**. The lecture uses **Node.js**.

#### Fabric CA
- A **Fabric CA (Certificate Authority)** issues **certificates and credentials (identities)** to components and applications of an organization.
- Start the test network with CAs: `./network.sh up createChannel -ca`. This starts **CA for orderer, CA for Org1, CA for Org2** (check with `docker ps`).
- Without `-ca`, the network uses the **cryptogen** tool, which creates identities once and cannot issue new ones later.
- Then deploy the chaincode (`deployCC`) as before.

#### Setting up the Node.js application
1. Create a folder (e.g., `test-app` inside `test-network`).
2. `npm init` (creates `package.json`).
3. `npm install fabric-ca-client fabric-network`.
4. Import: **FabricCAServices** (from fabric-ca-client), **Wallets** and **Gateway** (from fabric-network), plus `fs` and `path`.
5. Write an **async main()** function and call it at the end.

#### Steps in the application

**1. Read the connection profile**
- JSON file for Org1 (found under `organizations/peerOrganizations/org1.example.com`).
- Read with `fs.readFileSync` and `JSON.parse` into an object (`ccp`). It holds peer addresses (e.g., localhost:7051), CA address, MSP details.

**2. Get the CA information**
- `ccp.certificateAuthorities['ca.org1.example.com']`, and its TLS CA certificate (`tlsCACerts.pem`).
- Create the CA client: `new FabricCAServices(caInfo.url, { trustedRoots: caTLSCACerts, verify: false }, caInfo.caName)`.

**3. Create the wallet**
- `Wallets.newFileSystemWallet(path)` using a `wallet` folder in the current directory. Identities are stored here.

**4. Enroll the CA admin**
- `ca.enroll({ enrollmentID: 'admin', enrollmentSecret: 'adminpw' })`. These values come from the CA's docker compose file used at startup.
- Build an **X.509 identity** (certificate, private key, MSP id `Org1MSP`, type X.509).
- Save it: `wallet.put('admin', x509Identity)`.

**5. Register and enroll the application user**
- The app needs **its own identity** from the CA, obtained using the CA admin.
- Get the admin user context from the wallet (provider registry).
- `ca.register({ affiliation: 'org1.department1', enrollmentID: 'appUser', role: 'client' }, adminUser)` returns a **secret**.
- `ca.enroll({ enrollmentID: 'appUser', enrollmentSecret: secret })`, then build the X.509 identity and `wallet.put('appUser', ...)`.
- If the identity already exists in the wallet, it says so and skips this step.

**6. Connect to the network through a Gateway**
- `const gateway = new Gateway()`
- `gateway.connect(ccp, { wallet, identity: 'appUser', discovery: { enabled: true, asLocalhost: true } })` (asLocalhost because it is a test network).
- `const network = await gateway.getNetwork('mychannel')`
- `const contract = network.getContract('keyvaluechaincode')`

**7. Run chaincode**
- **Query**: `contract.evaluateTransaction('QueryKey', 'nptel')`. Convert the result to a string and print it.
- **Transaction** (changes the world state): `contract.submitTransaction('CreateKey', 'nptel', 'awesome')`.
- Query again to see the value.
- `await gateway.disconnect()`.

> **evaluateTransaction** is for **queries** (read only). **submitTransaction** is for **transactions** that change the **world state** (goes through endorsement, ordering, commit).

#### Summary
- Steps: import SDK packages → connection profile → CA info and CA client → wallet → enroll CA admin → register and enroll app user → gateway → network and contract → query and submit.
- Chaincode (business logic) + client application = a **DApp** on a permissioned network.

---

## 11. Scalable Consensus: Bitcoin-NG, CoSi, ByzCoin, Algorand

*PoW vs PBFT scalability, Bitcoin-NG, collective signing, ByzCoin, Algorand.*

### Lecture 38: Consensus Scalability (PoW vs PBFT)

*(Week 8)*

#### Recap of consensus protocols
- **Permissionless**: PoW (needs many miners, heavy computation), PoS and PoB (cannot bootstrap, depend on PoW), PoET (needs trusted hardware like Intel SGX).
- **Permissioned**: **PBFT** and other Byzantine agreement protocols (e.g., RBFT, hybrid BFT), using message passing, signatures and other cryptography.

#### PoW vs PBFT
| | **PoW** | **PBFT** |
|---|---|---|
| Environment | **Open**: anyone can join | **Closed**: identities known (message passing) |
| Number of nodes | **Scalable** (millions) | **Not scalable** (about 20 to 30) |
| Transaction throughput | **Low** | **High** |
| Computation | Heavy hashing | Only message passing |

#### Scalability of PoW: the two "magic numbers"
- **Block frequency**: about **10 minutes** per block.
- **Block size**: **1 MB** originally, later raised (the lecture says up to **8 MB**).
- Block size is limited by the **time peers need to download** a new block. If it is too big, the next block may be mined before peers finish, causing inconsistency.

#### Throughput calculation (1 MB block)
- Block size = 1 MB = **1,048,576 bytes**.
- Average Bitcoin transaction size ≈ **380.04 bytes**.
- Transactions per block ≈ 1,048,576 / 380.04 ≈ **2,759**.
- Per 10 minutes (600 s) → 2,759 / 600 ≈ **4.6 transactions per second (tps)**.
- **Visa** handles about **1,736 tps**.

#### Can tuning the parameters reach Visa's level?
| Option | Result |
|---|---|
| Keep **10 min** block time, increase block size | Needs about **377.5 MB** blocks. Impractical: peers on slow networks cannot download that fast |
| Keep **1 MB** block, reduce block time | Needs about **1.6 s** per block. The puzzle must become too easy, which **hurts security** |
| 1 MB block, **14 s** block time | About **197 tps** (still far below Visa) |
| **2 MB** block, **28 s** block time (download time doubles too) | About **196.6 tps** (no gain) |

- So PoW throughput **cannot be raised much** just by tuning the two parameters.

#### Performance vs scalability chart (Vukolić paper)
- x-axis: **node scalability** (number of nodes). y-axis: **throughput** (under 100 tps up to more than 10,000 tps).
- **BFT protocols**: **high throughput**, but only about **under 20 to 30 nodes**.
- **PoW**: supports **many nodes**, but **low throughput**.
- Goal: a protocol with **both** many nodes and high throughput.

#### Consensus finality (Vukolić's definition)
> If a correct node p appends block **B** to its blockchain **before** appending block **B'**, then **no correct node q appends B' before B**.

- **PoW**: does **not** ensure finality (forks can exist).
- **BFT**: **does** ensure finality.

#### Full comparison (PoW vs BFT consensus)
| Property | PoW | BFT |
|---|---|---|
| Node identity management | **Open**, decentralized | **Permissioned**, nodes know each other's IDs |
| Consensus finality | **No** | **Yes** |
| Scalability (number of nodes) | **Excellent** | **Limited** |
| Scalability (number of clients) | Excellent | Excellent |
| Throughput | **Limited** | **Excellent** |
| Latency | **High** | **Excellent** (about network latency) |
| Power consumption | **Very poor** | **Good** |
| Adversary power tolerated | **Under 25%** of computing power (as given in the lecture) | **Under 33%** of voting power |
| Network synchrony | Uses physical clock timestamps | No synchrony needed for safety (but **liveness (view change)** needs weak synchrony) |
| Correctness proof | **None** (no formal proof) | **Formal proof** |

#### Conclusion
- Permissionless consensus has **limited throughput**. BFT-based permissioned consensus is **limited in number of nodes**.
- We need a consensus that **balances both**. Next lectures cover protocols that do this.

---

### Lecture 39: Bitcoin-NG

*(Week 8)*

#### Paper
- **"Bitcoin-NG: A Scalable Blockchain Protocol"**, **NSDI 2016** (Eyal, Gencer, Sirer, van Renesse). An enhancement of **Nakamoto consensus (PoW)**.
- On the performance vs scalability chart, Bitcoin-NG has **node scalability like PoW** but **better performance**.

#### Problems with Nakamoto consensus
1. **Low transaction scalability**: a block every ~10 minutes (the difficulty must stay high for security) and a limited block size. Individual blocks can arrive earlier, but the **difficulty is fixed** so that blocks come at most every ~10 minutes on average.
2. **Forks** prevent **consensus finality**.
3. **Unfairness**: a miner on a **slow network** has its block propagated late, another miner's block wins, and its block becomes a **fork** (wasted).

#### Key idea
> **Bitcoin-NG decouples leader election from transaction serialization.**

- Two tasks: (1) **elect a leader** (via PoW mining), (2) **serialize transactions** into blocks.
- In **PoW**: both are tied together. **Every block** needs a new leader election, and the winner only proposes **one block**.
- In **Bitcoin-NG**: leader election is **infrequent**. Once elected, the leader can propose **many blocks** until the next leader is elected.

#### Two types of blocks
| | **Key block** | **Micro block** |
|---|---|---|
| Purpose | **Leader election** | **Carry transactions** (serialization) |
| Created by | A new miner who wins **PoW** | The **current leader** (no PoW) |
| Contents | Reference to previous block (key or micro), **unix time**, **coinbase transaction** (reward), **target hash**, **nonce** | Header with reference to previous block, **unix time**, **hash (Merkle root) of ledger entries**, the **leader's signature** on the header; plus the **ledger entries** (transactions) |
| Frequency | Infrequent (**exponentially distributed**, about every 10 minutes on average) | **Much more frequent**, at a rate up to a predefined maximum, many between two key blocks |

- Key blocks are generated by **regular Bitcoin mining**.
- The leader **signs** the micro blocks so that no other node can impersonate the leader.

#### Micro block fork
- A new leader (new key block) may **not have heard the latest micro blocks** of the previous leader (e.g., heard up to m3 but not m4). The new key block then builds on m3, and the remaining micro blocks (m4) are **pruned (forked)**.
- This is common because micro blocks are frequent.
- Reduce it by letting nodes **wait for the network propagation time** before trusting a micro block, to ensure no new key block prunes it.

#### Results (from the paper's graphs)
- **Consensus latency**: Bitcoin about **200 s** vs Bitcoin-NG about **10 s** (much lower).
- **Fairness** (0 to 1; closer to 1 is fairer): Bitcoin's fairness **drops** as the fork rate rises, while Bitcoin-NG stays **close to 1**.

#### Conclusion
- Bitcoin-NG improves **transaction throughput, latency and fairness**, and keeps PoW-like **node scalability**.
- It is still far below BFT in performance, so more improvement is possible.

---

### Lecture 40: Collective Signing (CoSi)

*(Week 8)*

#### Collective signing
- **CoSi (collective signing)** is a scalable way for **many parties to sign a message together**.
- From the paper **"Keeping Authorities Honest or Bust with Decentralized Witness Cosigning"** (IEEE S&P 2016).
- It protects authorities and their clients from **undetected misuse**.

**Analogy:** a nomination letter is signed by the **department head**, then the **dean**, then the **director**. Many people vouch for it, so even if one authority is faulty, the statement as a whole is still trustworthy. Another analogy: **witnesses in a marriage registry**.

> **Witness cosigning**: every authoritative statement is **validated and publicly logged by a diverse group of witnesses** before clients accept it. A statement signed by **w witnesses** assures the client that it has been **seen and not immediately found erroneous** by those w observers.

#### Scalability problem and the tree
- Normal repeated signing (P1 signs, then P2 signs the result, ...) is slow, and verification must be done in **reverse order**. **Not scalable.**
- **Solution**: the leader organizes the witnesses in a **tree**. Signatures from children are **aggregated upward** to the root. This is scalable.
- CoSi uses **Schnorr multi-signatures**.
- Another multi-signature option: **BLS** (Boneh–Lynn–Shacham), based on **bilinear pairing**, even more scalable.

#### Schnorr multi-signature

**Key generation**
- A group **G of prime order r** with generator **g**. The **discrete logarithm problem is hard** in G (given g^x, you cannot find x).
- **Private key** x (random integer between 0 and r − 1). **Public key** g^x.
- n signers with private keys x1, x2, ... xn and public keys g^x1, g^x2, ... g^xn.

**Signing**
1. Each signer picks a random secret **v_i** and computes **V_i = g^(v_i)**.
2. The leader aggregates: **V = ∏ V_i** (product).
3. The leader computes the **collective challenge c = H(V ‖ S)**, where S is the message to sign, and sends c to the signers.
4. Each signer computes the response **r_i = v_i − c · x_i**.
5. The leader aggregates: **r = Σ r_i** (sum).
6. The **signature is (c, r)**.

**Verification**
1. Compute the **combined public key Y = ∏ g^(x_i)**.
2. Compute **V' = g^r · Y^c**.
3. Check that **H(V' ‖ S) = c**. If yes, the signature is valid.

**Why it works:** g^r · Y^c = g^(Σ(v_i − c·x_i)) · g^(c·Σx_i) = g^(Σ v_i) = ∏ V_i = V, so the hash matches c. Verification needs just one check using the combined public key, with no repeated verification.

#### CoSi protocol on the tree
1. **Leader announces** the message to all witnesses (down the tree).
2. **Commitment**: each node sends its V_i up, and parents **multiply** the V values of their subtree.
3. The leader computes **c = H(V ‖ S)** and sends it down.
4. **Response**: each node computes r_i and sends it up, and parents **add** the values.
5. The leader gets **(c, r)**.

#### CoSi and PBFT
- **One CoSi round** emulates PBFT's **pre-prepare and prepare** phases.
- A **second CoSi round** emulates the **commit** phase.
- So **two CoSi rounds emulate the three PBFT rounds**.
- Advantages: no need for **full connectivity** (a tree is enough); the quorum is based on a **majority signing** the message; verification uses only the collective public key. Easier to scale while still giving **Byzantine fault tolerance**.

#### Next lecture
- **ByzCoin**, which uses CoSi to improve consensus scalability further.

---

### Lecture 41: ByzCoin

*(Week 9)*

#### Requirements of blockchain consensus
1. **Byzantine fault tolerant** (malicious participants across administrative domains).
2. **Strong consistency** across all replicas (same copy at the same time).
3. **Scales with workload** (high transaction throughput).
4. **Scales with network size** (many nodes).
- **PoW** is good at requirement 4 but weak at 3. **PBFT** is good at 3 but weak at 4. We need a protocol that balances both.

#### Problem with Bitcoin-NG
- A **faulty key block or micro block is only detected at the end of the round**, when the next leader is elected.
- A malicious leader can add a key block, some correct micro blocks, then **one faulty micro block**. The **whole chain of that leader (key block and all micro blocks) must be discarded**.
- With forks, this makes it even worse. A malicious miner can repeatedly cause this and create a **denial of service**.
- Reason: **micro blocks are not explicitly validated** before being added (only key blocks are validated by mining).

#### First attempt: PBFT verifiers
- Use a small group of **PBFT verifiers** that validate each micro block before it is added. PBFT works fast in a small group.
- But PBFT has problems here:
  1. It needs a **static consensus group**. If that group is **colluded**, **safety is violated**.
  2. **O(n²) communication** and **O(n) verification** (does not scale with nodes).
  3. **No third-party verification proof**: it uses **MACs** and shared keys, so you must know who the other miners are (hard in an open network).
  4. **Sybil attack**: a malicious node creates many pseudonyms to break the 3f + 1 requirement.

#### ByzCoin idea: an open consensus group
> **ByzCoin** combines **Proof of Work with PBFT (using CoSi)**. PoW is used to **select the members of the consensus group**, and CoSi collectively signs each micro block.

- Paper: **"Enhancing Bitcoin Security and Performance with Strong Consistency via Collective Signing"** (USENIX Security 2016).

**How the group is chosen**
1. Look at a **sliding window** of the **last w key blocks** (e.g., 7).
2. Every miner who mined a key block in the window becomes a **member of the trustee (witness cosigner) group**.
3. A miner's **share** = number of blocks it mined in the window / w (e.g., yellow 2/7, red 2/7, blue 3/7).
4. The window **slides** with each new key block, so the **group keeps changing** (not static). Membership is public information, so members can run the protocol among themselves.

**Validation of micro blocks**
- The group forms a **CoSi tree** and **collectively signs** each micro block (it can use Schnorr or BLS signatures).
- **2 CoSi rounds = 3 PBFT rounds**, so this gives BFT-style validation.
- A micro block is added only after the group's collective signature, so a faulty micro block cannot be slipped in.

#### Efficiency gains
| | Plain PBFT | ByzCoin (CoSi) |
|---|---|---|
| Communication | **O(n²)** | **O(log n)** (tree-based multicast) |
| Verification | **O(n)** | **O(1)** (one check using the collective public key) |

#### Performance
- With larger blocks (the lecture mentions 8, 16 and 32 MB), ByzCoin's throughput gets close to payment networks, but a **gap from Visa remains**.
- **Node scalability** equals Bitcoin (the group is built from Bitcoin miners).

#### Limitations of Bitcoin (recap)
- Heavy **resource and electricity waste**.
- **Concentration of power**: a handful of mining pools mine most blocks (visible on a block explorer, where the same pools repeat).
- Unclear scalability limit, **high latency** (about 10 min per block), and **forks** (no finality).

#### Blockchain performance triangle
> **Scalability, security and decentralization**: the protocols so far can satisfy at most two at the same cost to the third.

- Full decentralization costs security. Focus on scalability costs decentralization, and so on.
- Question for next lecture: **can all three be achieved together?** (Algorand.)

---

### Lecture 42: Algorand

*(Week 9)*

#### Motivation
- ByzCoin reaches high throughput, but PayPal-level rates (about 4,000 tps) and internet scale still need more. Algorand aims for **scalability, security and decentralization together** (the performance triangle).
- Paper: **"Algorand: Scaling Byzantine Agreements for Cryptocurrencies"**, **SOSP 2017** (Gilad, Hemo, Micali, Vlachos, Zeldovich, MIT). **Silvio Micali** is a core developer.

#### Overview
- Consensus through a **Byzantine agreement protocol**, so **transaction throughput scales** like BFT, but with **a very large number of nodes**.
- Communication: **gossip protocol** (like Bitcoin).
- Key assumption: **honest majority of money** (users hold Algorand coins, and weight comes from the coins held).

**Advantages**
1. **Trivial computation**: only simple operations, **no PoW** puzzles.
2. **True decentralization**: no mining pools, all users are equal.
3. **Finality of payment**: a **fork can happen but with very low probability**, so a block is final.
4. **Scalability**: millions of users, about **1 minute** per block (network latency).
5. **Security**: safe against a bad adversary because it builds on Byzantine agreement.

#### Architecture
1. Select a **random user** to **propose a block** and gossip it.
2. Select a **random committee** (small, about 10K users out of millions) to **validate** it.
3. The committee runs **Byzantine agreement (BA\*)** on the block, **digitally signs** the result (can use collective signing), and gossips it.
- Because both the proposer and the committee are **random**, an attacker (a tiny fraction of users) has a very low chance of controlling them. Majority of the committee is honest with high probability, assuming most users are honest.

#### Cryptographic sortition
> **Who selects the committee?** Each user **selects itself**, privately and verifiably, using **cryptographic sortition**.

- Every user runs the sortition algorithm. It gives **0 (not selected) or non-zero (selected)** plus a **proof**.
- Selected users **gossip** their result with the proof, so everyone can check it.
- Selection is **weighted by the money (weight) of the user**.

**Verifiable Random Function (VRF)**
- Input: the user's **private key SK** and a string **x**.
- Output: a **hash** (a fixed-length value uniquely decided by SK and x) and a **proof π** that the hash is correct.
- The **public key** is used to verify the proof.

**Sortition inputs**: **SK**, a public **seed** (random value from the previous round, itself made with a VRF), a **threshold τ** (expected number of users selected for that role; e.g., 1 for a proposer, 100 for a 100-member committee), the **role** (block proposer or committee member), the user's weight **w**, and total weight **W** (all Algorand in the system).
- **Output**: (hash, proof, **j**). If **j > 0**, the user is selected. If **j = 0**, not selected.

#### BA\* (binary Byzantine agreement)
- A **repeated Byzantine agreement** run on the sortition committee, deciding **accept or reject** of the block (binary).

**Two types of consensus**
| | **Final consensus** | **Tentative consensus** |
|---|---|---|
| Meaning | If one user reaches **final** consensus, every other user that reaches final **or tentative** consensus in that round has agreed on the **same block** | One user may have reached consensus on a **different block** than others (fork-like) |
| Result | Safe to **confirm the block** | Not final yet |

#### Synchrony assumptions
- **Strong synchrony**: most honest users (e.g., **95%**) can send messages that most other honest users receive **within a known time bound**. The adversary cannot partition the network for long. This ensures **liveness**.
- **Weak synchrony**: the network can be **asynchronous (controlled by the adversary) but only for a bounded time**. After that, a strong synchrony period returns.
- Algorand is **safe under weak synchrony**.
- (This connects to FLP: the system is not in a pure asynchronous mode forever.)

**When is consensus only tentative?**
- Under **weak synchrony** the adversary may partition users, so two groups reach tentative consensus on **different blocks**.
- Under **strong synchrony**, BA\* may still be unable to confirm that the network was strongly synchronous, so consensus stays tentative.

#### Recovering from tentative consensus
- If a committee is bad (e.g., majority malicious), consensus stays tentative and a **timeout** occurs. Move to the **next round of BA\***.
- **Sortition selects a different committee each round**, so it is unlikely that the next committee is also malicious. Eventually an honest-majority committee gives **final consensus**.
- The lecture says only a **few repetitions (2 to 3)** are needed in most cases.

**Algorithm summary:** reduce the network using **sortition** → run **binary BA\*** → **count votes**; if the votes match the BA\* result, it is **final**, else **tentative** → next round with a new committee.

#### Conclusion and trade-offs
- Algorand gives **Bitcoin-like scalability**, **BFT-like throughput**, and (almost) **no forks**.
- **Trade-offs:**
  1. Needs a **very large network** (in a small network, sortition picks a very small committee that an attacker could capture).
  2. Assumes the **adversary cannot hold the network for long**. If an application cannot guarantee this, Algorand may not be the best choice.
- This ends the **consensus** topic. The next topics (identity management) are taught by Prof. Sural.

---

## 12. Identity Management: DIDs, Verifiable Credentials, Indy and Aries

*Digital identity, SSI, DIDs, VCs, Hyperledger Indy and Aries tutorials.*

### Lecture 43: Identity Management (Part 1)

*(Week 9)*

#### Identity
- **Physical identity**: a **collection of attributes**: name, roll or employee number, ID card, date of birth, address, validity date, and sometimes financial or social history.
- Name alone is not unique, so we use unique attributes like roll number.
- **Digital identity**: email accounts, social media accounts (profile name, photo, history). These are often **not verified**.
- **Identity fraud**: someone can create a fake account in your name. Related actions:
  - **Authentication**: prove who you are (e.g., password).
  - **Authorization**: what you are allowed to do.
  - **Verification**: check an identity presented to a service.

#### Centralized identity management and its problems
- Identities are kept in **one central repository**.
- An **attacker in between** can copy or **change** an identity (e.g., swap the photo) and present it as theirs. The holder has **no control** over who presents the identity.
- A central store is a **single attractive target**: one breach exposes many identities (e.g., stolen credit card data).

#### Single Sign-On (SSO)
- One login lets you access **multiple services** (e.g., a Google account for Gmail, Drive, YouTube).
- **Identity Provider (IdP)** keeps the identity. **Identity consumers** (other services) use the IdP to **authenticate the holder**.
- The service **does not see your password**; the IdP just says the user is authenticated.
- SSO is still **centralized**.
- **KYC** (know your customer): an extra step that **ties the digital identity to the real physical person**. Needed for financial or sensitive services.

#### Decentralized digital identity
- **No central trusted identity provider or registry.**
- Two challenges:
  1. **Verify the identity issuer** (was it issued by a proper authority?).
  2. **Verify the identity holder** (is the person presenting it the one it was issued to?).
- Without this, an attacker can **copy an identity** presented on Monday and present it as their own on Tuesday.

#### Self-Sovereign Identity (SSI)
> The **individual has full control and ownership of their identity** and decides **when, to whom and which attributes** are presented.

- Example: a student has a **degree certificate** and a **transcript**. A company may need only the certificate. A university may need the transcript too.
- Gives **privacy control**. But it puts **burden on the user**.

#### Decentralized Identifiers (DIDs)
- A **W3C recommendation**.
- A DID provides a **verifiable, decentralized digital identity**, **decoupled from centralized registries**, with **no central certificate authority**.
- The **holder can prove ownership of the DID without help from any third party**.

**Architecture**
- A **DID** is a unique **URI** that identifies a **DID subject** (a person, organization or thing).
- The DID **resolves to a DID document**.
- DID documents are stored in a **verifiable data registry** (decentralized).
- A **DID controller** can create and update the DID document. The controller **can be the subject itself**.
- A verifier takes the presented DID, fetches the DID document from the registry, and verifies.

#### Why blockchain?
- The **verifiable data registry** must be **decentralized and verifiable by anyone**. A **blockchain** provides exactly this, so it can implement the registry.

---

### Lecture 44: Identity Management (Part 2): DIDs and Verifiable Credentials

*(Week 9)*

#### DID syntax
`did : method : method-specific-identifier`
- **Scheme** = `did`.
- **DID method** (e.g., `example`, or `ethereum`) = the system that defines how the DID is created and resolved.
- **Method-specific identifier** = unique within that method.
- Together they form a **globally unique** identifier. A DID is a **URI** (see RFC 2396 for URI, URL, URN).

#### DID document
- Describes the DID subject: its **attributes**, and **cryptographic public keys** the subject or its delegates can use to **authenticate** and prove association with the DID.
- Two parts:
  1. **Properties**: **id**, **alsoKnownAs**, **controller**, **authentication** and **verification methods**, **service (service endpoints)**, and extensions (e.g., an Ethereum address).
  2. **Representation-specific entries**: the format it is written in (**JSON, XML**, etc.), so it is read correctly.
- **Service endpoint**: where the verifier can go to access the service after authentication.
- Example (JSON): `id`, `authentication` (public key in multibase, type such as Ed25519 verification key), `controller` (same as id when the subject is its own controller), and `service` (e.g., a service endpoint URL).
- **Authentication method** says which public key technique to use (RSA, Ed25519 etc.), so the verifier knows how to verify.

#### Relationships
- The **DID controller** controls the DID document and can update it.
- The **DID identifies** the **DID subject**.
- The **DID resolves to the DID document**, which **describes the subject**.
- The DID document resides in the **verifiable data registry**.
- The **controller can equal the subject** (**self-certification**). Fine for non-critical attributes (hobbies, address). Critical attributes (a degree) must be certified by an authority.

#### DID registration and verification flow
1. **Step 0**: generate a **public key PK and secret key SK**.
2. **Step 1**: create the DID document: `id = did:registry1:alice`, authentication method = public key, controller = same.
3. **Step 2**: **register**: the DID document is **signed with the controller's secret key** and stored in the **verifiable data registry**.
4. **Authentication**: Bob wants to authenticate Alice. Alice gives her DID. Bob **fetches the DID document** from the registry, checks it was **signed by the controller** (using the controller's public key), and **authenticates Alice** using her public key.

#### Why a decentralized (blockchain) registry
**Risks of a centralized registry**: documents or authentication methods can be **manipulated**, **denial of service**, **censorship** (refusing to resolve some DIDs), and **no transparency**.

**Blockchain advantages**: **transparent**, **immutable**, **tamper-evident**, and **verifiable by anyone**. **DID methods are implemented as smart contracts** that enforce authorization and signature checks.

**Platforms**
- **Sidetree**: a protocol for **scalable DID networks** that runs on top of **existing permissionless blockchains** (Bitcoin, Ethereum).
- **Hyperledger Indy**: a **public permissioned ledger**. **Anyone can read and verify**, only **selected registered parties can write**.

#### Gap: binding digital identity to physical identity
- A DID only lets the controller prove control over its DID document. Any **physical details are only self-attested** (not verified).
- For critical uses (finance, voting) we need the DID **bound to verified physical attributes**. This is done with **Verifiable Credentials**.

#### Verifiable Credentials (VCs)
- A **W3C data model** for **digital credentials** (e.g., a driving license, degree certificate, income certificate).
- **Machine verifiable**, as acceptable as the physical document, **cryptographically secure** and **privacy respecting** (the holder shows only the needed part, matching self-sovereign principles).
- Decouples three parties: **issuer → holder → verifier**.
- Example: a university (issuer) gives a degree VC to a student (holder) in 2020. In 2022 the student shows it to another university or an employer (verifier).

---

### Lecture 45: Identity Management (Part 3): VC Workflow and Trust Model

*(Week 9)*

#### VC data model: components
| Component | Role |
|---|---|
| **Issuer** | Asserts claims about subjects, **creates the VC and gives it to the holder** (university, government). **Does not store the VC in the registry.** |
| **Holder** | Possesses one or more VCs (student, employee, customer). Can hold VCs from many issuers |
| **Subject** | The entity the claims are about (human, animal, thing). **Can differ from the holder** (a parent holds a child's credential; an owner holds a pet's) |
| **Verifier** | Receives and verifies the credential presented by the holder (employer, security personnel, another university) |
| **Verifiable data registry** | A **non-entity system** that holds **DIDs and public keys**, **VC schemas** and **revocation information**. It does **not** store the VCs themselves |

- **Verifiable Presentation (VP)**: what the holder presents to the verifier. It can be the **whole VC or only part**, or data combined from several VCs.
- **VC schema**: defines how a VC looks (fields like roll number, marks, CGPA), so a **machine** can read it.
- **Revocation**: the registry also says whether a VC has been **revoked** (e.g., a cancelled driving license), since the holder may still have a copy.

#### Claims, credentials and proofs
- **Claim**: a statement about a subject (e.g., "Pat is an alumnus of Example University").
- **Credential**: a set of one or more claims by an entity.
- **Proof**: usually a **digital signature by the issuer**, signed with the issuer's **private key** and verifiable with its public key.

**Structure of a VC:** **credential metadata + claims + proof.**
- Shown as a **credential graph** (nodes and edges: credential, subject Pat, type alumni credential, issuer Example University) and a **proof graph** (signature type such as RSA Signature 2018, **nonce**, signature value, creator = issuer's public key).

#### Verifiable presentation
- The holder creates a **presentation graph** containing the VC (with its credential proof) and a **presentation proof**: the whole thing is **signed by the holder's private key**.
- The verifier checks the holder's signature using the holder's **public key from the registry**.
- The presentation can be made **years later**, with different timestamps for the VC and the VP.

**Overall flow:** the **issuer issues** (and can **revoke**) → the **holder presents** (many times) to the **verifier** → the verifier **consults the registry** (and checks revocation status) each time.

#### Trust model
- Acting as issuer, holder or verifier needs **no registration or approval** by anyone. It is **decentralized**.
- Trust is **bilateral**: the **verifier trusts the issuer** not to issue false credentials. If the verifier does not trust an issuer, it does not accept its VCs.
- The VC includes a **proof** (signature) or is transmitted so it cannot be tampered with.
- **All entities trust the verifiable data registry**, so it must be **tamper-evident and correct** (this is where **blockchain** helps).
- **Holder and verifier trust the issuer** to issue **true** credentials and **revoke quickly** when needed.

#### Combining DIDs and VCs (example: Alice, a university and an industry)
1. **Create and register DIDs**: `did:registry1:alice` and `did:registry1:university` are created and stored in the verifiable data registry (e.g., Hyperledger Indy).
2. **Issue the VC**: Alice requests a transcript VC for her DID. The university fetches Alice's DID document, then issues the **transcript VC**: holder = Alice's DID, issuer = the university's DID, **signed by the university**. Alice keeps it.
3. **Present the VC**: an industry asks for the transcript. Alice prepares a **VP signed with her private key**. The industry:
   - fetches **Alice's public key** from the registry and checks she is the holder,
   - checks the **university's signature** on the VC (issuer correct),
   - consults the **revocation list** (VCs are held only by the holder, so check it was not revoked in between).
4. If all is fine, the VC is currently valid, and the industry can continue by going to the **service endpoint** in Alice's DID document.

#### Hyperledger Aries
- A Hyperledger project for **creating, transmitting and storing verifiable digital credentials**.
- A tutorial on it follows. Hands-on work with Fabric, Indy, Aries, Bitcoin and Ethereum is recommended beyond the lectures.

---

### Lecture 49: Hyperledger Indy Tutorial (Part 1): Setup and DID Registration

*(Week 10)*

#### Hyperledger Indy
- A Hyperledger project giving **tools, libraries and components** for **digital identities rooted on blockchains**, interoperable across administrative domains, applications and blockchain silos.
- Key characteristics:
  1. A **DLT purpose-built for decentralized identity** (its **own ledger**).
  2. **Byzantine fault tolerant** by design, using the **Indy Plenum** consensus (based on **RBFT**, redundant BFT).
  3. DIDs are **globally unique and resolvable from the ledger** without a central authority.
  4. Supports **verifiable credentials** and **zero-knowledge proofs** (e.g., validate a claim without knowing the actual value).
- It is a **public permissioned** ledger: **anyone can read**, only **permitted members (stewards)** can write.

#### Architecture and sub-projects
- An **Indy network = Indy pool** of independent **Indy nodes**. DIDs are stored on the distributed Indy ledger.
- Applications access it through the **Indy SDK**. You can run your own node or connect to existing nodes, depending on whom you trust.

| Sub-project | Role |
|---|---|
| **Indy Plenum** | Implements the **BFT consensus** (RBFT) |
| **Indy Node** | Blockchain functions and **identity-specific transactions** |
| **Indy SDK** | **APIs** for applications (wrappers for Python, JavaScript etc.) |

#### Installation (test setup)
- **Indy pool**: clone the indy-sdk repository, `docker build` an image (e.g., `indy_pool`) and `docker run` it, mapping ports **9701 to 9708**. It runs **4 Indy nodes in one container**. (A prebuilt image also exists.)
- **Indy SDK** (`libindy`) on Ubuntu, then `pip install python3-indy` for the Python wrapper.
- This is a **test pool**. Production pools need different steps.

#### Scenario
- **University** (issues a transcript), **Alice** (a student applying for a job), **Company** (verifier), plus a **Government** (registers schemas).
- The Indy ledger stores **DIDs, credential schemas, credential definitions and revocation lists**.

#### Roles in Indy
| Role | Meaning |
|---|---|
| **Steward** | Pre-approved participant who can **register new DIDs** (verinyms) on the ledger |
| **Trust Anchor** | Issues verifiable credentials (e.g., university). Role value **101**. Approved by stewards |

#### Steps in the code (Python, `asyncio`)
1. **Connect to the pool**:
   - Copy the **genesis transactions file** (from `/var/lib/indy/sandbox/pool_transactions_genesis` in the container) into a file such as `pool1.txn`. It holds 4 entries (one per node, with keys and IP addresses and ports).
   - `pool.set_protocol_version(2)`, `pool.create_pool_ledger_config(name, config)`, `pool.open_pool_ledger(...)`.
2. **Get control of a Steward**: the 4 nodes' stewards are generated from a **predefined seed** (e.g., "…Steward1"). The seed lets the SDK **deterministically derive the private key**. Create a wallet (`wallet.create_wallet`) and `did.create_and_store_my_did`.
3. **Register DIDs** for **Government, University and Company** as **Trust Anchors**, using a **NYM transaction** (`ledger.build_nym_request`, then `ledger.sign_and_submit_request`) signed by the steward. Output shows the DID and role **101**.
- **Alice's DID is not registered** on the ledger, since she does not issue credentials.
- For the demo, one script plays all participants. In reality each runs its own application.

---

### Lecture 50: Hyperledger Indy Tutorial (Part 2): Issuing and Verifying Credentials

*(Week 10)*

#### Steps
4. **Register a credential schema** (Government)
5. **Create a credential definition** (University)
6. **Issue the credential** (University → Alice)
7. **Present the credential** (Alice → Company)
8. **Validate the presentation** (Company)

#### Step 4: credential schema
- A schema fixes the **format and fields** of a credential, e.g., **Transcript**, version **1.2**, attributes: **first name, last name, degree, status, year, average, SSN**.
- **Schemas cannot be deleted**. To change one, register a **new version** (e.g., 1.3).
- Create with `anoncreds.issuer_create_schema(government DID, name, version, attrs)`. Register by `ledger.build_schema_request` and `sign_and_submit_request`.

#### Step 5: credential definition
- Each **issuer** needs its own **credential definition** for a schema. It contains the **signing algorithm and public keys**.
- The university **fetches the schema** from the ledger (`build_get_schema_request`, `parse_get_schema_response`), then `anoncreds.issuer_create_and_store_credential_def` with a **tag**, **type "CL"** (the only type supported) and `support_revocation = false`. Register with `build_cred_def_request` and `sign_and_submit_request`.
- Indy can also store **revocation lists** to revoke issued credentials (not used here).

#### Step 6: issuing (a request and response flow)
1. **Alice** sets up her wallet and DID.
2. The **university creates a credential offer** (`issuer_create_credential_offer`) and sends it to Alice.
3. Alice creates a **master secret** (ensures the credential is issued **uniquely to her** and only she can present it), fetches the credential definition, and creates a **credential request** (`prover_create_credential_req`).
4. The university **issues the credential** (`issuer_create_credential`). Each attribute has a **raw value and an encoded value** (Indy does not fix an encoding scheme).
5. Alice **stores the credential** in her wallet (`prover_store_credential`).
- In real life these messages travel over a network. Here they are just copied between variables.

#### Step 7: presentation
- The **company creates a proof request** (job application) listing:
  - **requested attributes**: some **self-attested** (no restriction), some **restricted** to credentials from the university's credential definition;
  - **requested predicates** (e.g., average above a value). A predicate uses a **zero-knowledge proof**: the condition is checked **without revealing the value**.
- Alice **searches her wallet** for credentials that satisfy the proof request (`prover_search_credentials_for_proof_req`), builds the **requested credentials** (marking restricted attributes as **revealed**), fetches the needed **schemas and credential definitions** from the ledger, and creates the proof (`prover_create_proof`).

#### Step 8: validation
- The company loads the proof, fetches schemas, credential definitions and revocation info from the ledger, checks the claims, and calls `anoncreds.verifier_verify_proof`.
- It passes if all claims are correct. If a claim is changed (e.g., the degree), it raises an **assertion error** ("claim did not match").

#### Gap and next step
- The tutorial copies values between variables. Real participants need a way to **exchange credentials and presentations**, which **Hyperledger Aries** handles.

---

### Lecture 51: Hyperledger Aries (Tutorial)

*(Week 11)*

#### Why Aries?
- **Hyperledger Indy** stores DIDs and verifiable credentials, but does **not** say how two participants **communicate** and **transfer credentials and presentations**. In the Indy tutorial we just copied values between variables.
> **Hyperledger Aries** provides **shared, reusable, interoperable tools** for **creating, transmitting and storing digital credentials**. It is the infrastructure for **blockchain-rooted peer-to-peer interactions** (issuer, holder and verifier talk directly, with no central server).

#### Aries agents
- An **Aries agent** is an **instance of an application** a participant uses to **interact with Indy** and **communicate with other Aries-enabled participants**.
- Main implementations:
  1. **ACA-Py (Aries Cloud Agent – Python)**: most popular, for **non-mobile** apps, used in production.
  2. **Aries Framework .NET**.
  3. **Aries Static Agent Python**.

#### ACA-Py architecture
Three kinds of modules: **core capabilities**, **protocols**, **REST API**.
- The **core** talks to a **distributed ledger** (the **verifiable data registry**: Indy, or another such as Sidetree) for **DIDs, credential schemas, credential definitions and revocation lists**. Currently **Indy is fully supported**.
- The agent also talks to **other Aries agents peer to peer** using the **DIDComm protocol** (Aries' standard for agent-to-agent communication). DIDComm is **independent of the transport**, so HTTP, TCP etc. can be plugged in.
- **Controller**: you write a **controller** with your **business logic** (you do **not** modify the agent). The controller sends **HTTP (REST) requests** to the agent. The agent sends **events** back to the controller as **webhooks**. So a controller needs an **HTTP client** (send requests) and an **HTTP server** (receive webhooks).
  - Example: another agent sends you a credential offer, and the agent informs the controller by webhook.
- The agent is a **single executable** configured by **command-line parameters**. It manages **storage, ledgers and wallets** (Indy wallet or your own implementation). It is **stateful**: it keeps connection and protocol state.

#### Installation (Ubuntu)
1. Add the key server and repository, `apt update`, install **libindy** (Indy SDK).
2. `pip install python3-indy`.
3. `pip install aries-cloudagent` (installs **ACA-Py**).
4. Check with `which aca-py` and `aca-py --version` (e.g., 0.5.1).
- Main commands: **`provision`** (set up wallets) and **`start`** (run the agent). Use `--help` for options.

#### Starting an agent (key options)
| Option | Meaning |
|---|---|
| `--inbound-transport http 0.0.0.0 8000` and `--outbound-transport http` | **At least one inbound and one outbound transport are mandatory** |
| `--wallet-type indy` | Use the Indy wallet (Indy as the ledger) |
| `--seed` (e.g., zeros + `Steward1`) with `--replace-public-did` | Take control of a **steward** and use its DID by default |
| `--genesis-file` | Path to the Indy pool's genesis file |
| `--admin 0.0.0.0 8001` and `--admin-insecure-mode` | Enable the **admin API** (no authentication, **for testing only**, not production) |
| `--webhook-url` | Where the controller listens for **webhooks** |
| `--wallet-name`, `--label`, `--log-level debug`, `--log-file` | Names, logging |

#### Admin API demo (Swagger / OpenAPI page)
- Opens in the browser on the admin port. It acts like a test controller and shows the exact HTTP requests (and `curl` commands). Example: `GET /status` returns the agent's version and task information.
- Two agents are run: **agent 1 = steward** (started with the seed), **agent 2 = not a steward**.
- `GET /wallet/did` shows an agent's DID. `GET /ledger/did-verkey?did=...` fetches a DID's verification key from the ledger.
- `POST /wallet/did/create` creates a DID **only in the local wallet**, so it is **not on the ledger** (the ledger lookup fails).
- To register it on the ledger, the **steward** uses the **register NYM** API (`/ledger/register-nym`) with the DID and verkey. After that, the DID **can be found** on the ledger.
- Other API groups: **connections** (create connections between agents), **credentials**, **schemas and credential definitions**, **revocation**, **issue-credential**, **present-proof**.
- You use these HTTP endpoints to write your controller and build your application.

#### Conclusion
- **Aries** gives communication between participants and manages decentralized identities and digital credentials. **Indy + Aries** together make it easy to build identity and credential applications.

---

## 13. Blockchain Interoperability

*Asset transfer, atomic swaps, HTLC, multi-party swaps, permissioned interoperability.*

### Lecture 46: Blockchain Interoperability (Part 1): Asset Transfer and Exchange

*(Week 10)*

#### What is interoperability?
- Blockchains work as **isolated silos**: Bitcoin and Ethereum (**permissionless**), Hyperledger and Corda (**permissioned**).
- **Interoperability** = making different blockchains **work together by exchanging assets or data**, without any of them changing its own protocol (each keeps its **autonomy**).

| | Permissionless | Permissioned |
|---|---|---|
| What is transferred | **Assets** (cryptocurrency), e.g., 1 BTC → ether | **Data** (not cryptocurrency-driven) |
| Key requirement | Transfer correctly across networks | The data must be the **consensus view** of the source network, not data that has not reached consensus |

- There are **2000+ cryptocurrencies**, each in its own network with different protocols and standards. Interoperability needs some kind of "translation" between them.

#### Cross-chain asset transfer
- Example: Alice has Bitcoin and wants to move **1 BTC** to the Ethereum network. Assumed rate: **1 BTC = 33 ETH**. Alice's bitcoin balance drops by 1 and her (or Bob's) ether balance rises by 33.

#### Method 1: Trusted Third Party (TTP)
- **Analogy**: paying a ₹16,000-plus conference fee of 200 euros through your **bank**. The bank takes rupees, converts, and pays euros abroad.
- The **TTP** holds **accounts on both networks**.
  1. Alice sends **1 BTC to the TTP** (a normal Bitcoin transaction).
  2. The TTP sends **33 ETH to Bob** on Ethereum.
- The TTP must hold **at least 33 ETH** to do this. For reverse transfers, the balances move the other way.
- In practice: **centralized cryptocurrency exchanges**. Users hand **ownership and sole control** of their funds to the exchange. It is usually **fast**.

**Problems with the TTP approach**
- **Lack of security**: exchanges hold large balances and are **attractive targets** (many thefts).
- If the exchange **shuts down** after taking the funds, they are **lost**. You are **at the mercy of the exchange**.

#### Method 2: Asset exchange (no centralized TTP)
- Alice and Bob **both have accounts on both networks**.
  - On Bitcoin, Alice sends **1 BTC to Bob**.
  - On Ethereum, Bob sends **33 ETH to Alice**.
- Different people can act as the counterparty each time (no central exchange).
- The two transfers must be **atomic**.

> **Atomicity**: either **all** operations happen or **none**. (Database analogy: A = A − 100 and B = B + 100 must both occur or neither.)

- It is harder here because the two networks are **completely independent**.
- If a party backs out in the middle, **nobody should be worse off** (each keeps their own balance).

#### Challenges of asset exchange
1. **No escrow**: funds are in the control of individuals, and one party may **abort after receiving funds**.
2. **Synchronization** between two networks (no common clock) and between the parties.
3. **Exchange rate fluctuation**: the rate (e.g., 1 BTC = 33 ETH) can change during the transfer, so a party may no longer want to proceed.
4. **Failures**: crashes and other problems must be recovered without breaking atomicity.
- A good protocol should be **generic** (work for any pair of networks, not just Bitcoin and Ethereum).

---

### Lecture 47: Atomic Swap and Hashed Time Lock Contracts (HTLC)

*(Week 10)*

#### Setup (two parties)
- Alice sends **1 BTC to Bob (exchanger)** on Bitcoin. Bob sends **33 ETH to Alice** on Ethereum. Alice can then pay these 33 ETH to the final recipient.
- Steps 1 and 2 (the two transfers) must be **atomic**. The final step can be delayed without problem.
- Source: **"Atomic Cross-Chain Swaps"**, **PODC 2018** (Herlihy).

#### Properties of an atomic swap protocol
1. If **all parties conform**, **all swaps happen**.
2. If some parties **deviate**, **no conforming party ends up worse off**.
3. **No coalition has an incentive to deviate**.

#### Basic idea
- Contract **A** on Bitcoin (Alice → Bob, 1 BTC) and contract **B** on Ethereum (Bob → Alice, 33 ETH).
- A **common event (trigger)** makes **both execute together**.

#### Hash lock
> A **hash lock** restricts spending of funds until a **secret pre-image x** is **publicly revealed**. The contract is locked with **h = H(x)** and unlocked by revealing **x**.

- Anyone can verify that H(revealed x) = h.
- **Key property**: once x is revealed on one chain, **every other contract locked with the same h can also be opened**. This is the basis of atomic swaps.
- Example: Alice picks the secret "I love strawberries", computes its hash, and puts 1 BTC in a contract that pays Bob if the key matching the hash is revealed.

#### Time lock
> A **time lock** restricts spending until a **specified future time** (time can also be measured as **block height**).

- Example: after **2Δ** (say 2 hours) the money can be released, or **returned to the sender**.
- (Related to Bitcoin script features seen earlier.)

#### HTLC (Hashed Time Lock Contract)
> **HTLC = hash lock + time lock.** The recipient gets the funds if they present the **secret before the timeout**. If not, the funds go **back to the sender** after the timeout.

- Example: Alice funds a contract (1 BTC, hash h, timeout 2Δ). If Bob provides a service (off-chain) and Alice reveals the key, Bob claims the BTC. If Bob never provides the service, Alice does not reveal the key, and after 2Δ her 1 BTC **refunds** to her.
- Bob should act only when Alice's contract is **sufficiently deep in the chain** (many blocks on top), so it cannot be undone.

#### Two-party atomic swap using HTLC
1. **Alice generates secret x** and computes **h = H(x)**.
2. Alice creates an **HTLC on Bitcoin**: **1 BTC** to Bob if x is revealed, hash **h**, timeout **4Δ**.
3. **Bob verifies** this contract (it has the hash h and is deep in the chain).
4. Bob creates an **HTLC on Ethereum**: **33 ETH** to Alice, **same h**, timeout **2Δ** (**shorter**).
5. **Alice verifies**, then **reveals x** to claim the 33 ETH.
6. **Bob sees x** (now public) and uses it to **claim the 1 BTC** on Bitcoin.

**Timing example:** Alice's contract at 5 pm times out at 9 pm. Bob's at 6 pm times out at 8 pm.

#### If something goes wrong
- If Alice is not satisfied (e.g., she expected 35 ETH) and **does not reveal x**: **Bob's contract times out first** (he gets back 33 ETH at 8 pm), then **Alice's** (she gets back 1 BTC at 9 pm). **Nobody is worse off.**

#### Why Bob's timeout must be earlier
- If Alice's timeout were earlier, she could wait for her contract to expire (getting her 1 BTC back), **then reveal x and also claim Bob's 33 ETH**, while Bob could no longer claim the BTC. **Bob would lose.**
- The protocol is **asymmetric** because Alice knows the secret and Bob does not, so Bob must be protected.

---

### Lecture 48: Multi-party Swap and Permissioned Blockchain Interoperability

*(Week 10)*

#### Three-party atomic swap (example from the paper)
- **Carol** wants to sell her **Cadillac** only for **Bitcoin**. **Alice** wants to buy it but pays only in **altcoin**. **Bob** will trade altcoin for Bitcoin.
- Required flows: **Alice → Bob** (altcoins), **Bob → Carol** (bitcoins), **Carol → Alice** (car **title**).
- Three networks: **altcoin**, **Bitcoin**, and a **title blockchain** (vehicle registration records).
- Each pair must have accounts on the same network.

**Steps (all with the same hash H)**
1. **Alice** creates secret **S**, computes **H**, and publishes an HTLC on the **altcoin** chain (altcoins to Bob), timeout **6Δ**.
2. **Bob** confirms it, then publishes an HTLC on the **Bitcoin** chain (bitcoins to Carol), same **H**, timeout **5Δ**.
3. **Carol** confirms it, then publishes an HTLC on the **title** chain (title to Alice), same **H**, timeout **4Δ**.
4. **Alice** confirms Carol's contract, then **reveals S** to claim the **title**. This reveals S to Carol.
5. **Carol** uses S to claim the **bitcoins** from Bob's contract. This reveals S to Bob.
6. **Bob** uses S to claim the **altcoins** from Alice's contract.

- **Timeouts decrease along the chain of publishing** (6Δ, 5Δ, 4Δ), so later claimants always have time to react.

**Failures**
- If a party halts **while contracts are being deployed**, all contracts **time out and refund**.
- If a party halts **while contracts are being triggered**, **only that party is worse off**. (Example: if Carol does not claim her bitcoins after Alice took the title, Bob's contract refunds Bob, Alice's refunds Alice and she also has the car, and **only Carol loses**.)
- Deviation only **harms the deviator**, and a coalition gains nothing.

#### Interoperability in permissioned blockchains
- Networks are **private** and separate per business vertical, e.g., **TradeLens** (logistics), **WeTrade** (trade finance), **IBM Food Trust** (food supply chain). They run in isolation.
- Need: **verifiable data transfer** (not asset transfer). The data must be **consistent with the source network's state** and represent the **consensus view of its parties**.

**Example:** a buyer in India buys wool from a seller in Australia.
- **Trade finance network (SWT)**: buyer, buyer's bank, seller's bank, seller. The buyer's bank gives a **Letter of Credit (LC)** guaranteeing payment.
- **Logistics network (STL)**: carrier (shipping company), seller. The seller books shipping, the carrier loads the goods.
- The **Bill of Lading (B/L)** (proof the goods were loaded and shipped) must move from **STL → SWT**, so payment can be released. The seller is common to both networks.

#### Architecture (Hyperledger Fabric based work)
- Each network has: peer-to-peer ledgers, **consensus protocol**, **membership manager** (access rights), **configuration management**, **data acceptance policy** (when to accept foreign data), **exposure control** (how much to share), and system contracts.
- A **relay** in each network handles communication between the two networks.
- Paper: published in the **20th International Middleware Conference (Industry Track), 2019**.

**Steps**
1. The destination network (A) creates a **proof request** with a **verification policy** and sends it to its **relay**, which forwards to the **source relay** (network B).
2. The source network checks **access control and exposure control policies**.
3. It returns the **data with proofs** (endorsements/signatures from its parties), **encrypted**, through the relays.
4. The destination checks the proofs against its **verification / data acceptance policy** (e.g., how many signatures are required).
5. If valid, the destination's **chaincode (smart contract)** accepts the data and **automatically triggers next actions** (e.g., the bank releases part of the payment).

- This transfers data **without violating each network's autonomy**.

---

## 14. Blockchain Security and Attacks

*Common risks, selfish mining, eclipse attack, front-running. (Sybil, DoS and 51% attacks are in Lecture 20.)*

### Lecture 52: Blockchain Security (Part 1): Common Risks

*(Week 11)*

#### Background
- Blockchain was designed for **decentralized management**, **self-organization** (difficulty adjustment, reward halving about every 4 years) and a **distributed, immutable ledger**. It was **not designed** to give security beyond "what is written cannot be erased". Security risks come from this nature.
- Survey paper: a **security survey of blockchain systems** (Future Generation Computer Systems, 2020).

#### Two categories of risks
| | Common risks | Specific risks |
|---|---|---|
| Related to | **Blockchain operation mechanisms** | **Development, deployment and execution of smart contracts** |
| Applies to | **Blockchain 1.0 and 2.0** | **Blockchain 2.0** |

**Smart contract risks (brief, not covered in depth):** **criminal smart contracts** (malware embedded), **bugs and vulnerabilities** (contracts are written in Turing-complete languages), **under-optimized contracts** (pay more gas than needed), **underpriced operations** (an attacker repeatedly invokes cheap operations to **flood the network**, delaying genuine users).

**Common risks covered:** **51% vulnerability, private key security, criminal activities, double spending, transaction privacy leakage.**

#### 1. 51% vulnerability
- Blockchain security depends on the **difficulty of mining**. Honest miners pool their resources (ASICs are needed).
- If an attacker gets **more than 50% of the hash power** (PoW) or **stake** (PoS), it can mine a **private chain faster** than the honest network. Example: honest users mine blocks 11, 12, 13 while the attacker mines 11', 12', 13', **14'**. The longer chain **11' to 14'** attached to block 10 becomes the main chain, and **11, 12, 13 become orphans** (their work is wasted).
- The network effectively becomes **centralized**, since the attacker influences every decision.
- Historically a pool once got close to 50% and **voluntarily dropped out** to avoid this.

#### 2. Private key security
- Digital signatures depend on the **private key**. If an attacker gets **Alice's private key**, Alice **loses control** of her coins. The attacker can spend them, and everyone verifies it with Alice's public key (it looks valid).
- Keys can also be **lost or forgotten**, or the owner may **die** without sharing the key, so the coins are lost for ever.
- Protection: store keys safely, e.g., **special hardware devices** (inserted only to sign).
- The private key is a **primary target** for attackers.

#### 3. Criminal activities (abuse of anonymity)
- **Ransomware** (e.g., **WannaCry**): files are encrypted and ransom is demanded in Bitcoin, paid to anonymous addresses.
- **Darknet markets** (e.g., **Silk Road**) sell contraband and take payment in cryptocurrency.
- **Money laundering**: unaccounted money is pushed into the network and converted into valid coins.
- Anonymity and a **borderless currency** make it hard to trace people or apply one country's law.
- **Risk to blockchain itself**: if this grows, countries may **act or ban** such cryptocurrencies (e.g., in India, trading is allowed but not payments), and people may lose faith.

#### 4. Double spending (attack)
1. Attacker X sends **TXv** (payment to the vendor), which the vendor sees.
2. At the same time X sends **TXa** to a **colluding address** (X's own).
3. If X **colludes with a mining pool**, TXa is mined **first** and confirmed in a block.
4. Later TXv is detected as double spending and **rejected**.
- By then the **vendor has already given the service** (because he did not wait for several confirmations). X keeps the service and the money.
- It needs **collusion with a miner** and a vendor who **does not wait for confirmations** (e.g., a store that accepts crypto at checkout).

#### 5. Transaction privacy leakage
- Even if addresses are anonymous, every transaction **spends outputs of earlier transactions**. So a **linkage graph** can be built by tracing back, and once one person is identified, flows can be traced.
- Defense: **mixins** (**decoy or chaff coins**): extra fake inputs are added to a transaction so the real source is hard to find.
- But later research showed mixins are **not foolproof**.

---

### Lecture 53: Selfish Mining Attack

*(Week 11)*

#### Setting
- Paper: published at **Financial Cryptography 2014** (on selfish mining in Bitcoin).
- Two groups: **"others"** (honest miners) and the **attacker's mining pool** (the attacker's computing power). The attacker has **sufficient power but less than 50%**, so this is **not** a 51% attack.
- **Bold blocks = published**, **dashed blocks = mined but not published (private)**.

#### The idea
- The attacker **mines blocks but does not publish them**, keeping a **private branch**, while honest miners continue on the **public chain**. The attacker knows the public chain length, but the public does not know the private one.
- When the public chain approaches the private branch in length, the attacker **publishes several blocks together**. The attacker's chain becomes the **longest chain** and the honest blocks become **orphans**.
- (Without publishing, the attacker gets **no reward**, so the timing of publishing is the whole strategy.)

#### Why do it? (the goal)
- Honest miners lose their rewards and see the pool earning more. So they **join the pool**. The pool's computing power grows (even beyond 50%) and it earns a **larger share** of blocks. The attacker gets **more revenue**.
- Even though honest miners together mine more blocks, the attacker wins by **choosing when to reveal**.

#### The eight scenarios (state transitions)
| # | Starting situation | Event | Pool's action | Revenue |
|---|---|---|---|---|
| 1 | Pool has a private lead (e.g., 0 or more) | **Pool finds a block** | **Keep it private** | Decided later |
| 2 | Two branches of length 1 (one public, one private) | **Pool finds a block** | **Publish its branch of length 2** (longest) | **Pool gets 2** |
| 3 | Two public branches of length 1 (fork: honest 11pub and pool 11pool) | **Others find a block after the pool's head** | none | **Pool 1, others 1** |
| 4 | Same fork | **Others find a block after the public head** | none | **Others 2**, pool 0 |
| 5 | **No private branch** | Others find a block | everyone mines on the new head | **Others 1** |
| 6 | **Lead of 1** | Others find a block | **Publish its block** (two branches of length 1, a race) | Undetermined until the next block |
| 7 | **Lead of 2** | Others find a block | **Publish all its blocks** (longest chain, everyone now mines on it) | **Pool 2** |
| 8 | **Lead of more than 2** | Others find a block | **Reveal only one block** (keeps a cushion of 2) so the honest side never gets ahead | Continues according to the later state |

- The attacker **chooses its action** depending on **its lead over the public chain**. In scenario 8 it frustrates honest miners (they spend resources but keep losing) so more of them join the pool.

---

### Lecture 54: Eclipse Attack and Front-Running Attack

*(Week 11)*

#### Eclipse attack
- Based on a paper at the **USENIX Security Symposium**.
- Unlike most attacks (at the application protocol level), this attacks the **peer-to-peer network layer** of the blockchain (how peers are chosen).

**Idea:** the attacker makes **all of the victim's peers attacker-controlled**. The victim is **isolated** from the real network, and the attacker sits between them (like an eclipse), **choosing what the victim sees** and **which of the victim's transactions reach the network** (it can **selectively drop** them). The network is not fully blocked, only mediated.

**Benefit:** it enables a **"51%-like" attack with less than 50% hash power**. Example: attacker has **40%**, victim **30%**, the rest of the network **30%**. By **partitioning** miners so they **cannot build on each other's blocks**, it is a head-to-head 40% vs 30%, and the attacker can **out-compete each partition**.

**How it is done**
1. Each node picks peers from two tables: the **"new" table** (IPs heard about) and the **"tried" table** (IPs peered with before). Each IP has a **timestamp**, and IPs are stored in **buckets**.
2. A node chooses a table, picks the IP with the **newest timestamp**, and connects.
3. The attacker **fills the "tried" table with its own IPs** and the **"new" table with junk IPs**, and keeps **refreshing timestamps** so its IPs look newest. When a bucket is full, random IPs are checked and the **oldest are evicted**, so the attacker's newer IPs replace honest ones.
4. When the victim **restarts** (software update, DoS, power or network failure), it connects only to the attacker's IPs.

**Defense:** the paper's authors explain the vulnerabilities and suggest **changes to the protocol** (how buckets and IPs are updated). Developers (e.g., Bitcoin) patch it in a new release.

#### Front-running attack
> **Front running**: an attacker who **knows about a pending transaction** (e.g., in the **mempool**) acts **in front of it** to profit.

- Example: Alice is about to buy **1000 ETH** (paying gas price 5). The attacker sees it and submits its own purchase with a **higher gas price (e.g., 50)**, so **miners include it first**. The attacker buys at ₹100 and Alice then buys at ₹110 (the price rose).
- Miners themselves can be attackers, since they **choose the order of transactions** in a block.

**Three types**
| Type | Meaning | Example |
|---|---|---|
| **Displacement** | The attacker's run makes **Alice's call irrelevant** | Alice wants to buy a domain/website. The attacker buys it first. Alice's transaction then **fails** |
| **Insertion** | The attacker's run **changes the state**, and Alice's call must run on the **modified state** | The attacker buys ETH and raises the price. Alice must pay more |
| **Suppression** | The attacker **delays Alice's call**, and after the delay it does not matter | The lottery game below |

**Another classification:** **asymmetric** (e.g., Alice cancels an offer, and the attacker **fulfills the offer first**, front-running the cancel) and **bulk** (the attacker runs a large set of functions while Alice buys a limited set of shares).

**Why it is easy on blockchains:** in stock markets front running is **illegal**, but in decentralized cryptocurrencies there is **no central authority** and no single country's law, so there is **no compensation**.

**Suppression example: the Fomo3D game**
- The game closes at a deadline, and the **last ticket buyer wins**. Each ticket purchase **extends the deadline** (about 30 seconds in the lecture).
- The winner bought a ticket just before the deadline, then sent **many high-gas transactions to its own DApps**, **flooding** the network so no one else's ticket purchase got into a block. The timer expired and the attacker won. Bribing miners could also be used.

#### Summary
- Different attacks can be combined (e.g., eclipse + 51%). The research community reports vulnerabilities and fixes follow in later releases. These lectures do not give an exhaustive list of attacks.

---

## 15. Use Cases and Application Design

*Good use case criteria, land registry, finance (Stellar, Ripple, Ubin), government, decentralized marketplace.*

### Lecture 55: What Makes a Good Blockchain Use Case

*(Week 11)*

- This begins the **last six lectures**: designing use cases and applications.

#### Example use cases by industry
| Domain | Examples |
|---|---|
| **Financial services** | **Trade finance** (TradeLens, WeTrade as named in the lecture), **cross-currency payments**, **mortgages**, **KYC**, **cross-border tax** |
| **Public sector** | **Asset (land) registration**, **citizen identity management** (DIDs, self-sovereign identity), **medical records** |
| **Retail** | **Supply chains** (**IBM Food Trust**), **loyalty programs**, information sharing between suppliers and retailers |
| **Insurance** | **Claim processing, risk provenance, asset usage history** |
| **Supply chain and logistics** | Supply chain financing, maintenance tracking, provenance, compliance |

- **Medical records**: hospitals do not share sensitive data. Using **federated or distributed learning**, each hospital computes **locally** and exports only the **result**. The **blockchain logs** who accessed what data, for what purpose, so raw data does not leave.
- Common pattern: **several competing parties with a common goal** that gain by sharing information.

#### "No free lunch"
- Blockchain is **not** simply "put data on a blockchain". Compare **overhead vs benefit** (like eCash, which failed because overhead exceeded benefit).
- Many research papers ("blockchain for IoT / health records") overlook real issues and never reach real use.

#### Three requirements for a good use case
1. **A business problem** that **cannot be solved more efficiently by other technologies**.
2. **An identifiable business network** with participants, assets and transactions. (Blockchain for your own room's IoT devices is overkill, since you control everything.)
3. **A need for trust**: you **cannot trust a third party**, e.g., **competing private hospitals** (X and Y) may cheat each other. If all hospitals are under the government, **the government can run a central repository**, so **no blockchain is needed**. Trust can come from **consensus, immutability, finality, provenance**.

#### Questions to ask
**A. The business problem**
- What **specific problem** does the project address?
- What is the **current way of solving it** (even if ad hoc)?
- Which **part** of the (large) problem will you solve?

**B. Participants**
- Who are the **participants** and their **roles**? How many types (e.g., buyers and sellers)?
- **How will they access and interact** with the blockchain (web or mobile app, gateways)? Will they be **peer nodes**?
- External data sources (needs **interoperability**)?
- **Who operates, governs and regulates** the blockchain? Who ensures information is correct?
- **Is the data publicly verifiable?** Example: **sensor data** on a blockchain is a poor use case unless you can **validate** it (a sensor can be faulty or hijacked, and unlike financial data you cannot check it against history).
- What is the **incentive** for each participant to join?
- **Identities**: do you need to know your users? Bitcoin is pseudonymous, but most business uses need identity. Public chains can use an **identity oracle** (government or financial database). Private chains use a **gateway or controller**, or **decentralized identity** (Lectures 43 to 45).

**C. Assets and transactions**
- What **assets** are involved and what **key information** do they carry? (A room temperature reading is not a meaningful asset.)
- What **transactions** happen, between whom, and under what **contractual conditions**?
- Which **actions** (add, delete, change, transfer) and queries are needed, and is **access control by role** required?

**D. Others**
- Main steps of the **current workflow**; **expected benefit for each participant** (is it uneven?); **legacy systems** and degree of integration.

#### Conclusion
- Do a **trade-off analysis**. Ask: can a **central database** or **trusted third party** do the job? If yes, the **centralized solution is best**.
- "Centralized is bad, distributed is good" is a **myth**. **Single point of failure** is a weak argument because central systems use **RAID, replication, geo-replication and disaster recovery**.
- Use blockchain only if, after defining the **network, participants, assets and transactions**, it is the best solution.
- Next lecture: a **case study** analyzing a use case this way.

---

### Lecture 56: Use Case Analysis: Land Registry (Devil's Advocate)

*(Week 12)*

#### The problem
- Land records are traditionally **paper deeds**. They can be **lost, destroyed, falsified or manipulated**. Getting a duplicate from the registry office is slow and tedious.
- To **sell** land you must **prove ownership**. Without the deed you must first get a duplicate.
- **Hereditary land**: land may still be in a grandfather's name and divided among 20 to 30 heirs, so agreement is hard. Missing or unclear records invite **scams** by dishonest realtors.
- The business network is complex (**realtors, inspectors, appraisers, escrow, middlemen**) and fraud news is frequent.
- Question: can blockchain help? Split the problem into **two fronts**: (1) **maintaining land records**, (2) **land and property trading**.

#### Front 1: maintaining land records
- Stakeholders: the **government** and the **land owners (citizens)**.
- **Trade-off 1: storage.** A blockchain is a **replicated, world-readable and world-writable database**. If everyone's land record is on it, **every participant (a full node) must store everyone's records**. A citizen would store millions of records, yet use this data **maybe once in a lifetime**. High storage cost.
- **Trade-off 2: pseudo-anonymity vs government control.** The government must know who owns land (only citizens may own land, with regional restrictions). The record must be **government controlled**.
- **Conclusion: blockchain is not a good use case for land records.** Better: **digitize** and keep them in a **secure central database** run by the government, a trusted party.

#### Front 2: land and property trading
- Participants: **government, realtors, buyers, sellers, investors and startups**.
- **Crowdfunding idea**: a startup without enough money gets funds from many **investors**, buys land, builds a property (e.g., a shopping mall), sells it, and **shares the profit** with the funders. Investors need **transparency** (the real sale price and profit), which blockchain can give.
- **Assets**: land, properties (buildings, malls) and money. **Transactions**: buy and sell land or property, crowdfunding, investment and return of profit.

**Public vs private blockchain**
| | Advantage | Problem |
|---|---|---|
| **Public** | Open, no pre-authentication | You do not know **whom you invest in** (anonymity) |
| **Private** | Identities can be verified (KYC) | **Who verifies identity?** A trusted third party, and then why not just use a **centralized database**? (chicken and egg) |

**Advantages of blockchain here:** decentralized marketplace, **no intermediaries**, **liquidity** (property traded readily), **fractional ownership and crowdfunded investment** (many investors, many startups), lower transaction cost, transparency.

#### Open questions
1. **Who are the full nodes?** Must buyers and sellers store the whole chain just for one sale?
2. After selling, can I **sign out**? Claims can appear **20 to 30 years later**.
3. Must I **keep my keys forever**? **Lost keys** mean lost ownership (the lecturer lost his own Bitcoin wallet key). What if the owner **dies**: how do children claim it?
4. If I am **not a full node**, whom do I trust?
5. **Privacy**: a blockchain is world-readable, so trades and investments are visible. Use keys or blind signatures? Then **who generates the keys**, one key per transaction, and who manages them?
6. With **no trusted third party**, there is nobody to recover lost keys.
7. What **credentials** are needed to be an investor or startup, and **who validates identities**?
- **Decentralized identity management** (DIDs) may help. A mechanism for **inheritance** after loss or death is needed.
- **Digitizing** the records already solves much of the problem. Then ask what remains for blockchain.

---

### Lecture 57: Financial Services Use Cases: Stellar, Ripple and Project Ubin

*(Week 12)*

#### Cross-border payments
- The classic Bitcoin use case. Over **6000 cryptocurrencies** exist.
- **What qualifies as a currency** (economics): **medium of exchange**, **unit of account**, **store of value**.

#### Stellar
- A **decentralized hybrid blockchain** with **open membership**, launched **2014**. Native asset: **lumens**.
- Consensus: **Federated Byzantine Agreement (FBA)** (the **Stellar Consensus Protocol**, SOSP 2019 paper *"Fast and Secure Global Payments with Stellar"*).
  - **Quorums form from each participant's own trust decisions** (nodes trust nodes they know). Overlapping quorums gradually agree. This runs Byzantine agreement in an **open network**.
- **Federated voting**: nodes **vote** for a valid statement → **accept** it when a quorum votes (or neighbors accept) → **confirm** it when a quorum accepts.
  - Example (7 nodes): one group votes x, another votes y, then as nodes accept x the larger quorum's acceptance spreads, and all agree on x.
- **Safety** under asynchrony, **liveness** needs a synchronous network (FLP respected).
- **2 to 5 seconds** to clear a transaction. About **350 tps** with about **1 second** ledger update latency (higher than Bitcoin, below Visa).
- **Anchors** bridge real currencies (e.g., INR) and the Stellar network. A **distributed exchange** converts currencies at the best rate.

#### Ripple
- Built for **banks** to **clear and settle payments in real time**, intended to replace **RTGS** (real-time gross settlement) without a centralized clearinghouse.
- Consensus: **XRP Ledger Consensus Protocol**. Default currency **XRP**. **No mining**, about **5 seconds** confirmation.
- **Custom protocol, not formally validated.** A research paper (*Analysis of the XRP Ledger Consensus Protocol*) shows it **can violate safety and liveness**.
- **Gateways** convert fiat to XRP. **Market makers** convert between currencies. **Centralized governance**, and Ripple holds a large fraction of coins.

#### Project Ubin (Singapore)
- Run by the **Monetary Authority of Singapore (MAS)** with banks and industry, **Nov 2016 to end 2020**. Goal: **interbank transfers and settlement of payments and securities on distributed ledger technology** (Singapore dollar).
- **RTGS background (MEPS+)**: banks hold **reserve accounts** at the central bank. A large interbank payment is just the central bank **debiting one bank and crediting another** (no physical money moves).

| Phase | Name | Content |
|---|---|---|
| **1** | **Tokenized SGD** | Consortium of banks (e.g., DBS, HSBC, JP Morgan, UOB, OCBC, SGX, R3) does interbank payments on DLT. Linked to the legacy MEPS system |
| **2** | **Reimagining RTGS** | MAS + Association of Banks. DLT-based RTGS prototypes on **Ethereum, Fabric and Corda**. Solves **gridlock** |
| **3** | **Delivery vs Payment (DvP)** | MAS + SGX. **Atomic exchange** of cash (cash ledger) against securities (securities ledger). Three prototypes (Corda, Ethereum, Fabric, etc. in different combinations) |
| **4** | **Cross-border Payment vs Payment (PvP)** | Bank of Canada, Bank of England, MAS (from Nov 2018). Transparent payment status, faster, cheaper. Three payment models analyzed |
| **5** | **Broad ecosystem** | A **multi-currency blockchain payment network** prototype with wallets and applications (invoice financing, trade finance, supply chain, property titles, capital markets) |

**Gridlock example (phase 2):** B1 has 50k but owes 100k to B2. B2 has 100k but owes 130k to B3. B3 has 20k but owes 50k to B1. **No one can pay first**, but the **net settlement** (offsetting the payments) succeeds. The DLT computes the **net transfers** (e.g., B1 net pays 50k, B2 net pays 30k), solving the gridlock.

**Phase 5 example:** the **B2P (blockchain for procure-to-pay)** network: a buyer in Thailand and a seller in Singapore. When documents for the export are verified, **payment is settled on the Ubin network**, moving money from the buyer's wallet to the seller's. This is **interoperability** of blockchains in practice.

---

### Lecture 58: Government (Public Sector) Use Cases

*(Week 12)*

#### Government data
- Governments hold data on **assets** (land, buildings, roads), **people and organizations**, **institutions** and **business transactions**.
- Governance is a **multi-institution hierarchy** (central → state → district → panchayat/city). **Money disbursement** flows in complex ways across levels, with **poor traceability**. Citizens, whose taxes fund it, have a **right to know**. Corruption is easy to hide.
- Blockchain fits because there is **no single point of trust**, and **transparency** is needed.
- Each level has its **own ledger**, role-based access policies, and data of different **sensitivity** (e.g., Aadhaar address, phone, biometrics).

#### Design questions
- **On-chain vs off-chain**: store large data **off-chain** and only the **hash (digest)** on-chain for integrity.
- **Who maintains the ledger copies?** Citizens? Special organizations? Most articles do not answer this.

#### Data breaches in government
- About **1,001 breaches in 2020 affected about 155.8 million individuals in the USA** (Statista; the lecturer said "billion").
- **Cyberwar**: attacks to steal other nations' data. Oct 2021 news: Argentine government ID database on a dark web forum, KYC data of 4.39 crore investors exposed, fake government sites.
- **Data duplication** across organizations increases risk. Example: **passport data** is copied by the Ministry of Foreign Affairs, customs, defense, police, income tax, intelligence, audit agency and the public service ministry. Aadhaar and KYC documents are copied in many places.

#### How blockchain helps
- **Keep data in a central database**, but **access is done as transactions logged on the blockchain**. Anyone can verify **who accessed what and why**. Access cannot be denied or altered later.
- Or put the **data itself** on the blockchain (transparent, unalterable), or **both data and access control**. Size is a concern.

#### GST (Goods and Services Tax) example
- **IGST** (inter-state), **SGST** (state), **CGST** (central). Tax is paid at **each stage of production** (raw materials, parts, assembly, sale).
- **Without blockchain**: seller issues invoice, buyer pays GST, seller registers it on the GST portal, suppliers also pay and register, and **returns/refunds** are filed to recover extra tax (exemptions and double levying complicate it).
- **With blockchain (smart contracts)**: the contract **calculates the tax from the invoice and tax already paid** in earlier stages, **transfers the tax to the authority** (CGST/SGST), and **refunds directly to the customer's account**.
- Benefits: **less administrative burden**, **real-time** transactions, **no return filing**, **transparency**, less fraud and **immediate audit**.
- Still the question: who stores the ledger, and how large will it be?

#### National strategies
- **India**: MeitY **Draft National Strategy on Blockchain** (Jan 2021). Use cases include **land records transfer, digital certificates, pharma supply chain, notary service, farm insurance, identity management, power distribution, duty payments, agriculture and supply chains, e-voting, electronic health records, digital evidence management, public service delivery, IoT device management and security, vehicle life cycle, chit funds, micro-finance for self-help groups**. It proposes a **national blockchain infrastructure** supporting **Hyperledger, Ethereum, Corda**, integrated with **Aadhaar, e-Pramaan, DigiLocker**.
- **Australia**: **National Blockchain Roadmap**. **Finance and insurance** show the most blockchain activity, then professional/scientific/technical services, retail, health care, real estate, information and telecom, arts, and utilities.

#### Conclusion
- Transparency and no single point of trust are real benefits, but **who the participants are and how big the ledger gets** is the main bottleneck. A phone or PC should not need **1 TB** just to hold the ledger.

---

### Lecture 59: Designing a Decentralized Marketplace (Requirements)

*(Week 12)*

- From the lab of the lecturer. Paper: **"Blockchain Interoperability for Service Decentralization"**, **IEEE INFOCOM 2021** (Bishakh Ghosh, Tanay Bhatia, Sourav Kanti Addya, Sandip Chakraborty).

#### Centralized marketplaces today
- **E-commerce (B2C)**: Amazon, eBay. **B2B** marketplaces. **Logistics and travel**: MakeMyTrip, Trivago, Booking.com. **Cloud**: OnApp federation (small providers combine, e.g., compute from one and storage from another).
- **Limitations** of a single broker:
  - **Unfair advantage and bias** toward some sellers.
  - Sellers must **share profit** with the broker.
  - Risk of **manipulation** and **unfair dispute resolution**.

#### Objective
- A **transparent, decentralized architecture** for a service consortium that **removes the central broker**, while keeping all functions of an Amazon-like interface (**unified interface**): view catalog, query price, request resources, get access credentials, pay.
- **Out of scope (open problems)**: **dispute resolution** (e.g., you receive an empty box), **legal aspects**, and **validation of service provider identity** (assumed to be done externally).

#### Challenges
1. **Byzantine service providers**: may manipulate **pricing, scheduling, policies**, be **biased** toward users or **block** requests.
2. **Byzantine consumers**: can create **many identities** (**Sybil** attack). Every request must be agreed on by the consortium.
3. **Verifiability** of the consortium's response: there is **no single spokesperson**, so how can the end user verify that the result came from the **consortium's agreement**?
4. **Confidentiality** of consortium responses (only between consumer and providers).

#### Threat model
- **At most one third** of service providers may be Byzantine.
- Consumers may create **many accounts** (Sybil).
- **Impersonation**: a malicious provider may pose as the consortium's spokesperson.
- **Leakage** of sensitive information over the network.

#### Required components
1. **Decentralized consortium interface** (consumer ↔ providers): agreement on each request, **ordering** of requests, **verifiable** responses, **confidential** responses.
2. **Decentralized consortium collaboration** (among providers): agreement on **pricing, catalog, policies**, **scheduling**, and confidentiality of provider data.
- Simply **broadcasting** requests to providers fails because messages can be **lost or reordered** and Byzantine consumers can **partition** the consortium.

#### Guarantees
- **Interface safety**: all non-faulty providers receive **the same set of consumer requests in the same order**.
- **Interface liveness**: **all requests of non-faulty consumers are eventually received** by the consortium.

#### Design idea
- Two networks:
  - **Consumers: open network** → use a **public blockchain**. A **smart contract with a fixed logical address** is the **single point of contact**. Mining gives **consensus on each request and its order** (the order of transactions in blocks).
  - **Service providers: closed network** → a **private blockchain** among known providers (they must reveal identity so consumers can choose; external validation assumed).

#### Two open problems (answered in the next lecture)
1. **Public → private**: providers cannot simply pick requests from the public chain. Some may **not receive the mined block in time**, **malicious members** may add **invalid requests**, and **PoW forks** can partition the network.
2. **Private → public**: a **single provider cannot post** the response (it may be malicious). The **consortium's consensus has no visible form outside** the private chain, so the response must be **verifiable by the end user** and kept **confidential** (e.g., the ticket reaches only the buyer).
- This needs **blockchain interoperability** (Lectures 46 to 48).

> **Lecture 60 (the solution to this problem) is the last lecture of the course. Add it here once you have it.**

---

## Quick Revision by Week

Original end-of-week summaries, unchanged.

### Week 1

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


### Week 2

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


### Week 3

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


### Week 4

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


### Week 5

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


### Week 6

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


### Week 7

- **LSP** (Lamport, Shostak, Pease): synchronous, reliable, fully connected, known senders. Proved **3f + 1**, but unrealistic.
- **PBFT** (Castro and Liskov, 1999): **asynchronous**, uses **digital signatures** and **hashes**, low overhead, **safety over liveness**.
- **View** = configuration with **one primary** and backups. **3f + 1 replicas.**
- **PBFT phases**: **pre-prepare** (primary assigns sequence number n) → **prepare** (backups vote) → **commit**, then reply to the client.
- **Pre-prepare checks**: valid signature, correct digest, same view, no conflicting n, n within threshold (stops **replay**).
- **Prepared** = pre-prepare + **2f matching prepares**. **Committed** = **2f + 1 commits**.
- **Total order** vs **partial order**.
- **Quorum** = minimum votes to commit. **Byzantine dissemination quorum** = **intersection + availability**, size **2f + 1**.
- **Why 2f + 1**: with f Byzantine you still keep **f + 1 correct** votes. **f + 1** alone is not enough.
- **PBFT is safe** (single leader, 2f + 1 quorum, async). **Liveness** needs **weak synchrony** (bounded delay T, retransmission) and **view change**.
- **View change**: timer expires → VIEW-CHANGE (n, C, P) → **2f + 1** view-change messages → acks → **NEW-VIEW** from the new primary. Next primary by **round robin** or **leader election**.
- **Heartbeats**: the primary sends dummy messages when idle.
- **Enterprise blockchain**: removes the **trusted third party** (cost, trust issues). **Four pillars**: shared ledger, smart contracts, security/privacy, consensus.
- **Benefits**: days → near instant, no intermediaries, less fraud, new business models (e.g., IoT + smart contracts).
- **Permissioned public** (pre-authenticated sellers) vs **permissioned private** (fixed consortium). Permissionless = many nodes, low throughput. Permissioned = high throughput, fewer nodes.
- **Hyperledger** (Linux Foundation): cross-industry open standard for distributed ledgers. **Fabric v1.0 released July 2017**, modular (plug-and-play consensus, privacy, membership), supports private transactions.
- **Hyperledger projects**: Fabric, Sawtooth, Indy (identity), Burrow (EVM), Cello (dashboard), Explorer (query blocks).
- **Fabric**: modular, permissioned, chaincode in **Go/Java/Node.js**, no built-in cryptocurrency (assets instead).
- **Fabric prerequisites**: git, curl, Docker, Docker Compose, Go. Install gives **samples + binaries + Docker images**.
- **Fabric binaries**: **cryptogen**, **configtxgen**, **peer**.
- **Fabric components**: **ledger** (blockchain + **world state**), **channel**, **peer**, **chaincode**, **MSP/CA**, **orderer (Raft)**, Fabric SDK.
- **Test network**: 2 orgs, 1 peer each, 1 orderer. `network.sh up / down / createChannel / deployCC`.
- **invoke** changes the ledger (via orderer). **query** only reads.


### Week 8

- **Chaincode** = Fabric smart contract (Go/Node.js/Java), runs as a separate process per peer.
- **Fabric transaction flow**: client → **endorsing peers** (simulate and endorse) → client → **orderer** (order into block) → all peers **commit**.
- **Stub functions**: **PutState** (write) and **GetState** (read) on the **world state**.
- **Go chaincode build**: `go mod init`, `go get`, `go build`; deploy with `network.sh deployCC -ccn -ccp -ccl`.
- **Fabric application** uses the **Fabric SDK** (Node.js/Java; also Go, Python) to send transactions via a peer and receive results.
- **Fabric CA**: issues certificates (identities). Start with `network.sh up createChannel -ca`.
- **App steps**: connection profile → CA info → **wallet** → enroll **CA admin** → **register and enroll app user** → **Gateway** → network → contract.
- **evaluateTransaction** = query. **submitTransaction** = changes world state.
- **PoW throughput** ≈ **4.6 tps** (1 MB block, 380 B tx, 10 min). **Visa** ≈ **1736 tps**.
- Tuning block size or block time **cannot** reach Visa without hurting download time or security (about 377.5 MB blocks, or about 1.6 s block time).
- **PoW**: many nodes, low throughput, no finality, high latency, high power use. **BFT**: about 20 to 30 nodes, high throughput, finality, low latency.
- **Consensus finality**: if one correct node appends B before B', no correct node appends B' before B.
- **Bitcoin-NG** (NSDI 2016): **decouples leader election from transaction serialization**.
- **Key block**: PoW, infrequent, elects the leader. **Micro block**: signed by the leader, frequent, carries transactions.
- **Micro block fork**: the new leader misses the last micro blocks, which get pruned. Bitcoin-NG has **lower latency** and **fairness near 1**.
- **CoSi**: many witnesses collectively sign, using a **tree** to aggregate. Uses **Schnorr multi-signature**.
- **Schnorr**: V_i = g^(v_i), V = ∏ V_i, **c = H(V ‖ S)**, r_i = v_i − c·x_i, **r = Σ r_i**, signature (c, r). **Verify**: V' = g^r · Y^c and check H(V' ‖ S) = c.
- **2 CoSi rounds emulate 3 PBFT rounds**. **BLS** is another, more scalable, multi-signature scheme.


### Week 9

- **Bitcoin-NG problem**: a faulty micro block is found only at the end of the round, so the leader's whole chain is discarded (DoS risk).
- **ByzCoin**: PoW + PBFT via CoSi. A **sliding window of the last w key blocks** decides the **consensus (trustee) group**, with shares by blocks mined.
- **ByzCoin efficiency**: communication **O(n²) → O(log n)**, verification **O(n) → O(1)**.
- **Performance triangle**: **scalability, security, decentralization** (trade-offs).
- **Algorand**: BA\* (binary Byzantine agreement) on a **random committee** chosen by **cryptographic sortition**. **Honest majority of money.** About 1 minute per block, millions of users, **no PoW**, very low fork probability.
- **Sortition**: each user runs a **VRF** with SK, seed, threshold τ, role, weight w, total weight W → (hash, proof, j). **j > 0** = selected. Others verify the proof.
- **Final vs tentative consensus**: final = everyone agrees; tentative = possible disagreement. Rerun BA\* with a **new committee** each round until final.
- **Strong synchrony** (known time bound for most honest users) gives **liveness**. **Weak synchrony** (asynchronous only for a bounded time) is tolerated for **safety**.
- **Algorand trade-offs**: needs a **very large network**, and assumes the adversary cannot hold the network for long.
- **Identity**: collection of attributes. **Centralized identity** has central breach and attacker-in-the-middle risk. **SSO** (IdP + consumers) is still centralized. **KYC** binds digital to physical identity.
- **Decentralized identity challenges**: verify the **issuer** and the **holder**.
- **SSI**: the holder controls what to present, to whom.
- **DID** = `did:method:identifier`, a URI that resolves to a **DID document** stored in a **verifiable data registry**. **Controller** can equal **subject**.
- **DID document**: id, controller, authentication/verification methods (public keys), service endpoints, representation (JSON/XML).
- **DID flow**: generate keys → create document → sign with SK and register → verifier fetches the document and checks signature and authenticates.
- **Blockchain as registry**: transparent, immutable, tamper-evident. **Sidetree** (on Bitcoin/Ethereum), **Hyperledger Indy** (public permissioned).
- **VC** = credential with **metadata + claims + proof**. Roles: **issuer, holder, verifier, subject**. The **registry stores DIDs, schemas, revocation info, not the VCs.**
- **VP**: holder's presentation, signed with the **holder's private key**, can show part of a VC.
- **VC trust model**: no registration, bilateral trust (verifier trusts issuer), **everyone trusts the registry**.
- **Verification steps**: holder's signature → issuer's signature → revocation check → service endpoint.
- **Hyperledger Aries**: for creating, transmitting and storing verifiable credentials.


### Week 10

- **Interoperability**: different blockchains exchange **assets** (permissionless) or **data** (permissioned) while keeping autonomy.
- **TTP / centralized exchange**: holds accounts on both chains; **risks** are theft and shutdown with your funds.
- **Asset exchange** between two individuals needs **atomicity** (all or nothing).
- **Challenges**: no escrow, synchronization, exchange-rate change, failures.
- **Atomic swap guarantees**: all swap if all conform; conforming parties not worse off; no incentive for coalitions.
- **Hash lock**: locked with h = H(x), unlocked by revealing x. **Time lock**: funds released or refunded after a time (or block height). **HTLC** = both.
- **Two-party swap**: Alice picks secret x, HTLC on chain 1 (timeout **4Δ**); Bob copies **same h** on chain 2 (timeout **2Δ**); Alice reveals x; Bob uses x. **Bob's timeout must be shorter** (Alice knows the secret).
- **Three-party swap**: timeouts **6Δ, 5Δ, 4Δ**; S is revealed in the reverse order (Alice → Carol → Bob). Failure only hurts the deviator.
- **Permissioned interoperability**: **verifiable data transfer** (consensus view of source). Uses **relays**, **verification policy**, **exposure control**, **data acceptance policy**.
- **Example data**: **Bill of Lading** from logistics network to trade finance network; **Letter of Credit** guarantees payment.
- **Hyperledger Indy**: own **public permissioned ledger** for identity, **Indy Plenum (RBFT)**, **Indy Node**, **Indy SDK**; supports VCs and **zero-knowledge proofs**.
- **Roles**: **Steward** (registers DIDs), **Trust Anchor (101)** (issues credentials).
- **Indy flow**: connect to pool (genesis file) → steward (seed) → register DIDs (NYM) → **schema** (government) → **credential definition** (university, type CL) → **offer → request (master secret) → credential** → **proof request** (attributes, predicates) → **proof** → **verify**.
- **Predicate** = zero-knowledge condition check. Schemas are versioned, never deleted.


### Week 11

- **Aries**: shared tools for **creating, transmitting and storing credentials**, peer to peer. Fills the communication gap in Indy.
- **ACA-Py**: core capabilities + **DIDComm protocols** + **REST API**. A **controller** sends HTTP requests, agent sends **webhooks**. Agent is **stateful**, transport-independent.
- **ACA-Py commands**: `provision`, `start`. **Mandatory**: one inbound and one outbound transport. `--wallet-type indy`, `--seed`, `--genesis-file`, `--admin`, `--admin-insecure-mode` (testing only), `--webhook-url`.
- **Admin API**: `/status`, `/wallet/did`, `/wallet/did/create` (local only), `/ledger/register-nym` (steward), `/ledger/did-verkey`, connections, issue-credential, present-proof.
- **Blockchain risks**: **common** (1.0 and 2.0: 51%, private key, criminal use, double spending, privacy leakage) and **specific** (smart contracts: criminal contracts, bugs, under-optimized, underpriced operations).
- **51%**: more than 50% of hash power or stake lets the attacker rewrite the chain, making honest blocks orphans.
- **Private key**: loss or theft means loss of coins. Use hardware storage.
- **Double spending attack**: TXv to vendor + TXa to colluding address, with a colluding pool, and the vendor not waiting for confirmations.
- **Privacy leakage**: linkage graph by tracing inputs. **Mixins** (decoy coins) help but are not foolproof.
- **Selfish mining**: attacker with **less than 50%** keeps mined blocks **private**, and publishes when it benefits. Aim is **higher revenue** and attracting honest miners to its pool. **Eight scenarios** based on the lead (publish at lead 1 → race, lead 2 → publish all, lead above 2 → reveal one at a time).
- **Eclipse attack**: attacker fills the victim's **peer tables** ("tried" table with attacker IPs, "new" table with junk, fresh timestamps), then the victim connects only to the attacker. Allows a **"51%-like" attack with about 40%** power. Fixed by protocol changes.
- **Front running**: attacker sees a pending transaction and uses a **higher gas price** to go first. Types: **displacement, insertion, suppression**. Also **asymmetric** and **bulk**. Example of suppression: **Fomo3D** (flooding the network so the deadline never extends).
- **Good use case**: (1) problem not better solved by other tech, (2) **identifiable business network** (participants, assets, transactions), (3) **need for trust**.
- **Questions**: current solution, participants and interaction, who operates and governs, **verifiable data** (sensor data problem), incentives, identity, assets and transactions, access control, benefits for each participant, legacy systems.
- **Not a good fit** if a **trusted third party or central database** works. "Centralized is bad" is a **myth**.


### Week 12

- **Land records on blockchain**: every participant would store everyone's records, and the government needs control and identity. **Better: digitize and keep in a central government database.**
- **Land trading**: participants include investors and startups (**crowdfunding**, **fractional ownership**, profit sharing). Public chain: unknown identities. Private chain: who verifies identity?
- **Open issues**: full nodes, signing out, **lost or inherited keys**, privacy, identity validation. **DIDs** might help.
- **Currency criteria**: medium of exchange, unit of account, store of value.
- **Stellar**: **Federated Byzantine Agreement** (SCP), federated voting (**vote → accept → confirm**), quorums from **own trust choices**, 2 to 5 s, anchors and distributed exchange, lumens.
- **Ripple**: banks and real-time settlement, **XRP**, about 5 s, **not formally verified** (can violate safety and liveness), gateways and market makers.
- **Project Ubin (MAS Singapore)**: **5 phases**: tokenized SGD → **RTGS and gridlock** (net settlement) → **DvP** (atomic cash vs securities) → **cross-border PvP** → **multi-currency ecosystem**.
- **Government data**: no single point of trust, hierarchy, poor traceability, **data duplication** increases breaches. Blockchain **logs access**, data **off-chain with hash on-chain**.
- **GST with smart contracts**: auto-compute tax at each stage, pay authority directly, refunds, no return filing. **IGST, SGST, CGST**.
- **India's draft national blockchain strategy** (Jan 2021) lists many use cases. **Australia's roadmap** shows finance and insurance leading.
- **Main bottleneck**: **who stores the ledger** and its size.
- **Decentralized marketplace**: remove the broker. Challenges: **Byzantine providers, Byzantine/Sybil consumers, verifiability, confidentiality**. Threat model: **at most 1/3 Byzantine providers**.
- **Guarantees**: interface **safety** (same requests, same order) and **liveness**.
- **Design**: **public blockchain** for consumers (open, ordering), **private blockchain** for providers, and **interoperability** between them in both directions.
