# Hi, I'm Rémi

**Blockchain / L2 Engineer · Software Security Engineer · Applied Zero-Knowledge**
*CIFRE PhD candidate — IMT Atlantique × Vistory*

I build distributed systems that scale, and I use cryptography — primarily zero-knowledge proofs — as the lever that lets them scale without giving up correctness. My core focus is **throughput, latency, and verifiable integrity** in blockchain infrastructure: where the bottlenecks actually are, how to model them, and how to engineer around them.

I work with a **security-engineering background** that I bring into every layer of the stack. Security is not a review step at the end of the project; it is a design constraint from the first sketch of the architecture — threat modeling, attack-surface reduction, and verification informing the design itself rather than patching it afterwards.

---

## What I do

- **L2 scaling architectures** — zk-rollups, optimistic rollups, state channels, sidechains
- **Zero-knowledge engineering** — Groth16 circuits in Circom, applied cryptography (Poseidon, KZG, EIP-4844), prover/verifier pipelines
- **Performance modeling** — analytical and empirical study of consensus protocols, prover backends, and data-availability layers
- **Security by design** — threat modeling of distributed protocols, smart-contract attack surfaces, cryptographic-assumption analysis, trusted-setup hygiene
- **Trustless infrastructure** — anchoring, integrity proofs, Merkle aggregation, on-chain settlement contracts

I work end-to-end: from the formal model down to the Solidity verifier deployed on testnet — with the threat model carried along the whole way.

---

## Selected work

### ⚡ ZK-Rollup for Monetary Transactions — *L2 scaling, end-to-end*
Reference implementation accompanying my CIFRE doctoral thesis. A full zk-rollup compressing batches of up to **8192 transactions** into a single Groth16 proof, with EIP-4844 blobs as the data-availability layer, deployed on **Ethereum Sepolia**.

- Circom circuits (per-batch-size R1CS) + Groth16 verifier contracts on Sepolia
- Sequencer / Executor / Prover / DA / L1 client — all subsystems isolated and instrumented
- Dual prover backend: `snarkjs` (reference) and `rapidsnark` (production)
- EIP-4844 type-3 transactions binding the validity proof to the blob commitment
- Empirical benchmarks: **~1750 tx/s** prover throughput at N=8192 with `rapidsnark`, **O(1) on-chain verification** independent of batch size
- Explicit threat model: replay protection via state-root chaining, blob/proof binding via `blobhash(0)`, documented limitations (sequencer centralisation, unauthenticated ingestion, trusted-setup boundary)

> **Key result:** the system is bandwidth-bound, not proof-bound. Verification gas amortises per-transaction as 1/N — this is the mechanism through which proof succinctness translates into throughput scaling.

---

### 🔗 Recursive SNARK Benchmark — *From O(N) to O(1) verification*
Empirical demonstration that replacing N independent Groth16 proofs of an iterated computation with a **single proof compressing the whole chain** collapses verification cost from `O(N)` to `O(1)`.

- MiMC recurrence over BN254, parameterised chain circuit (1 → 100 transitions)
- Side-by-side measurement of verifier time, proof size, and prover cost
- Documents the standard rollup trade-off: heavy off-chain proving, cheap on-chain verification

> Built as a teaching artefact for the proof-aggregation argument that underpins every modern rollup design.

---

### 🔐 Data Integrity Platform — *Production trustless anchoring* (ROAB)
On-premise platform for verifiable data integrity through blockchain anchoring. Built as a multi-service architecture deployed in containers.

- REST API ingestion → Merkle aggregation → dual-layer anchoring (**L2 + L1**)
- Solidity smart contract (`DataIntegrityAnchor`) for timestamped Merkle root storage
- Three independently-verifiable proof types: L2 anchor, L1 anchor, single-entry proof
- TypeScript microservices (API + anchoring worker) + PostgreSQL + Docker Compose
- Designed with explicit isolation of key material, RPC trust boundaries, and on-premise deployment to reduce external attack surface

> **Key insight:** decoupling data availability from verifiable integrity — and using the L2/L1 split to trade settlement cost against finality guarantees.

---

### 🧪 Blockchain Consensus Simulator — *Performance modeling at scale*
Scientific simulator comparing **PoW, PoS, PoA** across 10² → 10⁴ nodes, with physically-grounded models (automatic difficulty adjustment, BFT communication overhead, propagation delay, orphan rate).

- Four metrics: throughput, finality latency, energy per transaction, security score
- Interactive parameter sweeps (PySide6 + Matplotlib)
- Quantified result: PoW energy/tx grows **×102 over the range**, security plateaus at validator caps — predictive framework for protocol design

> Used to characterise the structural — not implementation-level — limits of each consensus family.

---

### 🛡️ Zero-Knowledge Identity System — *Applied Groth16 pipeline*
Minimal but rigorous end-to-end ZK identity scheme: prove knowledge of a secret linked to a registered commitment, without revealing it.

- Poseidon-based commitment scheme, Circom circuit, snarkjs Groth16 backend
- Full pipeline: register → prove → verify, with explicit notes on nullifier reuse, replay protection, and trusted-setup hygiene
- Clean reference implementation of the soundness / zero-knowledge / completeness triad

---

### 🔍 Smart Contract Vulnerability Analyzer — *Static analysis for Solidity*
Static analyser covering the ten canonical Solidity vulnerability classes (reentrancy, integer overflow, access control, `tx.origin`, `delegatecall`, weak randomness, DoS, `selfdestruct`, unchecked calls, timestamp dependence).

- One detector per vulnerability class, paired vulnerable / safe example corpus
- Heuristic pattern matching + lightweight structural analysis
- CLI with JSON output for CI integration

> Built to internalise the offensive perspective: you can't design secure smart contracts without understanding what each class of exploit actually looks like at the bytecode level.

---

### 🎮 Veilcrypt — *ZK fog-of-war for trustless games* *(work in progress)*
Asynchronous multiplayer dungeon crawler with cryptographic fog of war, in the lineage of Dark Forest.

- Noir circuits + Solidity verifier (Foundry), TypeScript/React/Phaser client
- Deterministic world generation: the dungeon exists only as `tile(seed, x, y, depth) → content`
- Four action circuits: scout, move, fight, descend
- Demonstrates that ZK can power real, playable applications — not just financial primitives

---

## Methodology

Across every project, the same loop:

1. **Model** the system formally — what does the math say is achievable, and what is the threat model?
2. **Identify the binding constraint** — throughput? verification cost? data availability? prover memory? trust assumption?
3. **Engineer around it** — circuit design, batching, aggregation, layer choice, attack-surface reduction
4. **Measure** — empirical benchmarks, not assumptions

This is how research insights become production constraints — and how production observations feed back into the model.

---

## Stack

**ZK / Cryptography** — Circom, snarkjs, rapidsnark, Noir, Groth16, Poseidon, KZG, EIP-4844
**Smart contracts** — Solidity, Foundry, EVM (Cancun), static analysis
**Security** — threat modeling, smart-contract attack surfaces, cryptographic-protocol review
**Backend / Infra** — Python, TypeScript, Node.js, Docker, PostgreSQL, FastAPI
**Frontend** — React, Phaser
**Analysis** — NumPy, Matplotlib, performance benchmarking

---

## Collaboration

I'm particularly interested in problems involving:

- L2 / rollup infrastructure (zk or optimistic)
- Production deployment of ZK proof systems
- Scalability and performance engineering for distributed protocols
- Smart-contract security review and trustless architectures
- Verifiable computation and data integrity

Open to **full-time positions and freelance missions** in these areas.

---

## 📫 Contact

- **LinkedIn:** [Rémi Barbier](https://www.linkedin.com/in/r%C3%A9mi-barbier-2a713b179/)
