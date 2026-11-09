<div align="center">

# Rémi Barbier

**Blockchain · Zero-Knowledge · Cybersécurité du logiciel**  
**Blockchain · Zero-Knowledge · Software Security**

Ingénieur en cybersécurité du logiciel · Doctorant CIFRE en blockchain  
Software Security Engineer · CIFRE PhD Candidate in Blockchain

[Français](#français) · [English](#english) · [Projets publics / Public repositories](https://github.com/roab-912?tab=repositories) · [LinkedIn](https://www.linkedin.com/in/r%C3%A9mi-barbier-2a713b179/)

</div>

---

## Français

### À propos

Je travaille à l’intersection des **systèmes distribués, de la cryptographie appliquée et de la sécurité logicielle**. Mon objectif est de transformer une propriété attendue — confidentialité, intégrité, vérifiabilité ou résilience — en une architecture, une implémentation et un protocole d’évaluation explicites.

Mon activité doctorale CIFRE, à l’interface d’**IMT Atlantique et de Vistory**, porte sur la blockchain et le passage à l’échelle. Mes dépôts publics présentent des travaux allant des circuits ZK aux contrats Solidity, de l’infrastructure de consensus aux applications de vérification, avec une attention particulière aux hypothèses de confiance et aux limites des résultats.

**Ce portfolio permet d’examiner concrètement mon travail : code, circuits, tests, mesures, décisions d’architecture et documentation.** Les descriptions ci-dessous portent exclusivement sur les projets publics de ce compte ; leur statut distingue les applications expérimentales, les bancs d’essai et les démonstrateurs pédagogiques.

### Domaines de compétence et réalisations associées

| Domaine | Compétences illustrées dans les dépôts | Réalisations |
| --- | --- | --- |
| **Blockchain et systèmes distribués** | Architecture de pipelines L2, disponibilité des données, contrats EVM, intégration de consensus BFT, indexation et reprise | ZK Rollup, Civora, Monitoring Private Blockchain |
| **Ingénierie Zero-Knowledge** | Circuits arithmétiques, séparation des entrées publiques et privées, génération et vérification de preuves, engagements et attestations signées | Clair, ZK Identity, ZK Recursive, Civora |
| **Cybersécurité du logiciel** | Analyse statique heuristique, contrôle d’accès, frontières de confiance RPC, validation des entrées, tests négatifs et réduction de la surface d’attaque | Vulnerability Analyzer, Monitoring, Clair, Ariadne |
| **Investigation blockchain** | Collecte Ethereum bornée, rapprochement transaction/reçu/bloc/logs, normalisation ETH/ERC-20, conservation de la provenance | Ariadne |
| **Évaluation expérimentale** | Instrumentation des coûts de preuve, CPU/mémoire, latence, gas et analyses de sensibilité ; distinction entre modèles et observations | ZK Rollup, ZK Recursive, Consensus Simulator |
| **Ingénierie applicative** | API, interfaces de vérification, persistance, migrations, conteneurisation, tests d’intégration et parcours navigateur | Clair, Ariadne, Monitoring, Civora |

### Projets principaux

#### 1. Clair — application de preuves Zero-Knowledge

[Dépôt SaaS-ZK](https://github.com/roab-912/SaaS-ZK) · **MVP applicatif**

Une application qui permet de composer une règle, de produire une preuve dans le navigateur et de la faire vérifier sans transmettre les valeurs privées au service de compilation.

- Traduction d’un modèle de règles publiques en **Noir / UltraHonk**, **Circom / PLONK** ou **Circom / FFLONK**, ce dernier étant expérimental.
- Calcul des preuves dans un **Web Worker**, versionnement immuable des circuits et liaison de leur empreinte aux paramètres publics.
- Attestations de sources approuvées ; vérification de signatures **P-256 et SHA-256 dans le circuit Noir** pour certaines entrées signées privées.
- Parcours React, comptes et sessions, persistance SQLite, intégration Stripe et vérificateur portable hors ligne après préparation.
- Tests de preuves altérées, paramètres modifiés, isolation des comptes et absence de données privées dans les requêtes du parcours testé.

**Ce que ce projet illustre :** relier cryptographie, confidentialité des flux et expérience de vérification dans une application complète.

**Périmètre :** une preuve sur des données déclarées n’en certifie pas l’origine. Les connecteurs métier et la protection contre la copie restent à développer ; une ouverture publique nécessite une revue de sécurité. L’intégration Stripe est testée par simulation, sans paiement bout en bout attesté dans le dépôt.

[Architecture](https://github.com/roab-912/SaaS-ZK/blob/main/docs/ARCHITECTURE.md) · [Moteurs ZK](https://github.com/roab-912/SaaS-ZK/blob/main/docs/ENGINES.md) · [Sources signées](https://github.com/roab-912/SaaS-ZK/blob/main/docs/SOURCES.md) · [Tests](https://github.com/roab-912/SaaS-ZK/blob/main/docs/TESTING.md)

#### 2. Civora — gouvernance et vote chiffré vérifiable

[Dépôt Civora](https://github.com/roab-912/Civora) · **Distribution expérimentale**

Un système de gouvernance associant registre répliqué, éligibilité ZK, bulletins chiffrés et vérification des reçus.

- Noyau **Go**, réplication **CometBFT**, registre et partitions.
- Intégration de **Semaphore** pour l’éligibilité et d’**ElectionGuard 2.0** pour le vote chiffré.
- Vérification des preuves et des données du registre en **Go et TypeScript** ; application PWA et outils d’audit autonomes.
- Travail sur la reprise, les compteurs persistants, les rotations et les prérequis cryptographiques de récupération, avec **ML-DSA-65 / SHA3-384**.
- Distribution avec inventaire, provenance SLSA et vérification TUF incluant un état anti-retour persistant.

**Ce que ce projet illustre :** intégrer plusieurs protocoles cryptographiques dans un système distribué dont les décisions et les reçus peuvent être vérifiés.

**Périmètre :** le pilote public reste non qualifié. La campagne à dix millions de bulletins, les audits externes, les appareils physiques et le cycle complet de reprise restent à valider ; aucune capacité à cette échelle n’est revendiquée.

[Vérificateur Semaphore](https://github.com/roab-912/Civora/blob/main/internal/semaphore/verifier.go) · [Qualification](https://github.com/roab-912/Civora/tree/main/spec/qualification) · [Décisions d’architecture](https://github.com/roab-912/Civora/tree/main/spec/decisions)

#### 3. ZK Rollup — banc d’essai de passage à l’échelle

[Dépôt Zero-Knowledge-Rollup](https://github.com/roab-912/Zero-Knowledge-Rollup) · **Artefact de recherche**

Un pipeline expérimental de traitement de transferts par lots : séquenceur, pool persistant, exécuteur, prouveur, publication des données et interaction avec Ethereum.

- Circuits **Circom / Groth16**, pilotes **snarkjs** et **rapidsnark**.
- Contrat Solidity de soumission de lots et de vérification ; références de déploiement **Sepolia** documentées.
- Construction de transactions **EIP-4844 de type 3**, encodage de blobs et engagements **KZG**.
- Scripts et résultats d’expériences sur les coûts de preuve, les ressources, le gas et la latence ; campagnes documentées incluant des lots de 8 192 transactions.

**Ce que ce projet illustre :** construire et instrumenter les différentes étapes d’un pipeline ZK/L2 pour étudier leurs coûts et leurs goulets d’étranglement.

**Périmètre :** ce banc d’essai ne constitue pas un rollup de production sécurisé. Le circuit expose un signal de validité ; les racines d’état et le contenu du blob ne sont pas liés cryptographiquement à cet énoncé. Le contrôle `blobhash(0)` du contrat ne suffit pas à établir cette liaison. Les dépôts et retraits ne sont pas implémentés.

[Contrat de soumission](https://github.com/roab-912/Zero-Knowledge-Rollup/blob/main/smart_contract/Rollup.sol) · [Scripts expérimentaux](https://github.com/roab-912/Zero-Knowledge-Rollup/tree/main/scripts) · [Résultats conservés](https://github.com/roab-912/Zero-Knowledge-Rollup/tree/main/bench-out)

#### 4. Ariadne — investigation Ethereum avec provenance

[Dépôt Ariadne](https://github.com/roab-912/Ariadne) · **Application locale v0.2**

Un outil de collecte et d’examen des transactions Ethereum qui conserve les pièces sources et rend visibles les limites de couverture.

- Découverte bornée par adresse via Etherscan V2, puis rapprochement des transactions, reçus, logs et blocs par RPC.
- Normalisation des transferts ETH de premier niveau et des événements ERC-20 standard.
- Montants exacts : entiers Python, `NUMERIC(78,0)` PostgreSQL et chaînes décimales dans l’API.
- Provenance consultable, états partiels explicites, collecte idempotente et séparation des données synthétiques et collectées.
- API Python, interface React/TypeScript, migrations et tests sur PostgreSQL dédié.

**Ce que ce projet illustre :** produire une information exploitable sans perdre sa provenance, sa précision numérique ni ses limites d’interprétation.

**Périmètre :** usage local mono-utilisateur ; transferts internes, attribution d’entités, traçage inter-chaînes et surveillance continue des réorganisations hors périmètre.

[Normalisation](https://github.com/roab-912/Ariadne/blob/main/src/investigation/normalization.py) · [Tests d’intégration](https://github.com/roab-912/Ariadne/tree/main/tests/integration) · [Décisions d’architecture](https://github.com/roab-912/Ariadne/tree/main/docs/adr)

#### 5. Monitoring Private Blockchain — explorateur Besu et connexion vérifiée

[Dépôt Monitoring-Private-Blockchain](https://github.com/roab-912/Monitoring-Private-Blockchain) · **Jalon v0.1 sur laboratoire local**

Une console d’exploration d’une blockchain privée **Besu / QBFT**, avec indexation persistante et contrôle de l’identité du réseau.

- Laboratoire de quatre validateurs et d’un nœud RPC non validateur.
- Vérification du `chainId`, du `networkId` et du hash de genesis avant activation d’une source.
- Indexation des blocs, transactions, reçus et logs ; reprise après arrêt brutal et suspension explicite en cas de désaccord ou de panne RPC.
- Sources RPC autorisées par l’opérateur, contrôle des destinations réseau, séparation API/worker, rôles et quotas persistants.
- Documentation des vérifications sur Besu réel, PostgreSQL et navigateur.

**Ce que ce projet illustre :** intégrer une infrastructure blockchain à une application observable, avec des frontières de confiance et des scénarios de panne explicites.

**Périmètre :** l’administration distante et la gouvernance des validateurs depuis l’interface relèvent des versions futures. Le laboratoire local partage un seul domaine de panne physique.

[État de réalisation et preuves](https://github.com/roab-912/Monitoring-Private-Blockchain/blob/main/docs/STATUS.md) · [Documentation](https://github.com/roab-912/Monitoring-Private-Blockchain/tree/main/docs)

### Démonstrateurs et outils complémentaires

| Projet public | Réalisation | Portée exacte |
| --- | --- | --- |
| [Smart Contract Vulnerability Analyzer](https://github.com/roab-912/Smart-Contract-Vulnerability-Analyzer) | Analyseur Python du source Solidity : dix classes de vulnérabilités, exemples vulnérables/corrigés, rapports CLI et JSON, tests | Analyse heuristique pédagogique ; faux positifs et négatifs possibles. Ne constitue pas un audit de production ni une analyse du bytecode. |
| [Zero-Knowledge Identity System](https://github.com/roab-912/Zero-Knowledge-Identity-System) | Engagement Poseidon, circuit Circom, génération et vérification Groth16 pilotées en Python | Preuve de connaissance d’un secret associé à un engagement ; ne certifie pas une identité civile et ne fournit pas de protection de session contre le rejeu. |
| [Zero-Knowledge Recursive](https://github.com/roab-912/Zero-Knowledge-Recursive) | Comparaison de N preuves de transitions MiMC avec une preuve d’un circuit regroupant N transitions ; mesures et graphiques | Compression monolithique du calcul. La récursion preuve-dans-preuve et l’IVC restent conceptuelles dans ce dépôt. |
| [Custom Blockchain Consensus Simulator](https://github.com/roab-912/Custom-Blockchain-Consensus-Simulator) | Modèles PoW/PoS/PoA, interface PySide6, analyses débit/latence/énergie et scénarios adverses | Simulations paramétrées ; les scores de sécurité sont heuristiques et ne constituent ni des garanties formelles ni des mesures de réseaux réels. |

### Méthode de travail

1. **Définir l’énoncé et le périmètre** : propriété recherchée, données, acteurs et hypothèses de confiance.
2. **Construire une implémentation inspectable** : séparer domaine, cryptographie, persistance et interfaces ; documenter les choix.
3. **Tester les frontières** : preuves invalides, données incohérentes, droits insuffisants, pannes et reprise.
4. **Mesurer avec un contexte explicite** : paramètres, environnement, coûts, résultats bruts et limites de généralisation.
5. **Qualifier les conclusions** : distinguer spécification, comportement implémenté, validation locale et qualification de production.

### Technologies mises en œuvre

| Ensemble | Technologies présentes dans les projets |
| --- | --- |
| ZK et cryptographie | Circom, Noir, Groth16, UltraHonk, PLONK, FFLONK expérimental, snarkjs, rapidsnark, Poseidon, KZG, Semaphore, ElectionGuard, P-256 |
| Blockchain | Ethereum/EVM, Solidity, Sepolia, EIP-4844, Besu, QBFT, CometBFT, JSON-RPC |
| Backend et données | Python, Go, JavaScript, TypeScript, Node.js, FastAPI, PostgreSQL, SQLite |
| Interfaces et analyse | React, PWA, Web Workers, PySide6, NumPy, Matplotlib |
| Validation et exploitation | Docker Compose, migrations, tests unitaires et d’intégration, Playwright, fuzzing dans Civora, documentation d’architecture |

### Recherche et collaboration

Ces travaux constituent une base pour des échanges de recherche ou des missions de **prototypage ZK**, d’**architecture blockchain**, d’**évaluation de performances**, de **sécurité applicative** et d’**outillage de vérification ou d’investigation**.

Pour un directeur de recherche, les dépôts rendent examinables les modèles, les choix expérimentaux et les limites. Pour un client, ils montrent ma capacité à relier un besoin à des composants concrets : circuit, API, stockage, interface, tests et documentation.

**Contact :** [LinkedIn — Rémi Barbier](https://www.linkedin.com/in/r%C3%A9mi-barbier-2a713b179/).

---

## English

### About

I work at the intersection of **distributed systems, applied cryptography and software security**. My goal is to translate a required property — privacy, integrity, verifiability or resilience — into an explicit architecture, implementation and evaluation procedure.

My CIFRE doctoral work, at the interface of **IMT Atlantique and Vistory**, focuses on blockchain and scalability. My public repositories span ZK circuits, Solidity contracts, consensus infrastructure and verification applications, with particular attention to trust assumptions and the limits of experimental results.

**This portfolio provides concrete material for reviewing my work: code, circuits, tests, measurements, architecture decisions and documentation.** The descriptions below cover only this account’s public projects and distinguish experimental applications, research testbeds and educational demonstrations.

### Expertise supported by public work

| Area | Skills illustrated in the repositories | Projects |
| --- | --- | --- |
| **Blockchain and distributed systems** | L2 pipeline architecture, data availability, EVM contracts, BFT consensus integration, indexing and recovery | ZK Rollup, Civora, Monitoring Private Blockchain |
| **Zero-Knowledge engineering** | Arithmetic circuits, public/private input separation, proving and verification, commitments and signed attestations | Clair, ZK Identity, ZK Recursive, Civora |
| **Software security** | Heuristic static analysis, access control, RPC trust boundaries, input validation, negative testing and attack-surface reduction | Vulnerability Analyzer, Monitoring, Clair, Ariadne |
| **Blockchain investigation** | Bounded Ethereum collection, transaction/receipt/block/log consistency checks, ETH/ERC-20 normalization and provenance | Ariadne |
| **Experimental evaluation** | Proving costs, CPU/memory instrumentation, latency, gas and sensitivity analysis; separation of models from observations | ZK Rollup, ZK Recursive, Consensus Simulator |
| **Application engineering** | APIs, verification interfaces, persistence, migrations, containers, integration tests and browser workflows | Clair, Ariadne, Monitoring, Civora |

### Main projects

#### 1. Clair — Zero-Knowledge proof application

[SaaS-ZK repository](https://github.com/roab-912/SaaS-ZK) · **Application MVP**

An application for composing a rule, generating a proof in the browser and verifying it without sending private values to the compilation service.

- Translation of a public rule model into **Noir / UltraHonk**, **Circom / PLONK** or experimental **Circom / FFLONK**.
- Proving in a **Web Worker**, immutable circuit versions and binding of their fingerprint to public inputs.
- Trusted-source attestations, including **in-circuit P-256 signature and SHA-256 verification in Noir** for supported private signed inputs.
- React workflows, accounts and sessions, SQLite persistence, Stripe integration and a portable verifier that works offline after preparation.
- Tests covering modified proofs and public inputs, account isolation and absence of private values from requests in the tested workflow.

**Capability illustrated:** connecting cryptographic implementation, private data flows and a complete verification experience.

**Scope:** proofs over self-declared data do not establish provenance. Business connectors and copy protection remain future work; public release requires a security review. Stripe integration is tested with simulation, without an attested end-to-end payment in the repository.

[Architecture](https://github.com/roab-912/SaaS-ZK/blob/main/docs/ARCHITECTURE.md) · [ZK engines](https://github.com/roab-912/SaaS-ZK/blob/main/docs/ENGINES.md) · [Signed sources](https://github.com/roab-912/SaaS-ZK/blob/main/docs/SOURCES.md) · [Testing](https://github.com/roab-912/SaaS-ZK/blob/main/docs/TESTING.md)

#### 2. Civora — governance and verifiable encrypted voting

[Civora repository](https://github.com/roab-912/Civora) · **Experimental distribution**

A governance system combining a replicated ledger, ZK eligibility, encrypted ballots and receipt verification.

- **Go** core and **CometBFT** replication for the ledger and partitions.
- **Semaphore** eligibility and **ElectionGuard 2.0** encrypted voting integration.
- Proof and ledger-data verification in **Go and TypeScript**, a PWA and standalone audit tools.
- Recovery work, persistent counters, rotations and cryptographic recovery prerequisites using **ML-DSA-65 / SHA3-384**.
- Distribution inventory, SLSA provenance and TUF verification with persistent rollback protection.

**Capability illustrated:** integrating multiple cryptographic protocols into a distributed system with verifiable decisions and receipts.

**Scope:** the public pilot remains unqualified. The ten-million-ballot campaign, external audits, physical-device validation and full recovery cycle are outstanding; no capacity at that scale is claimed.

[Semaphore verifier](https://github.com/roab-912/Civora/blob/main/internal/semaphore/verifier.go) · [Qualification](https://github.com/roab-912/Civora/tree/main/spec/qualification) · [Architecture decisions](https://github.com/roab-912/Civora/tree/main/spec/decisions)

#### 3. ZK Rollup — scalability research testbed

[Zero-Knowledge-Rollup repository](https://github.com/roab-912/Zero-Knowledge-Rollup) · **Research artefact**

An experimental pipeline for batched transfers: sequencer, persistent pool, executor, prover, data publication and Ethereum interaction.

- **Circom / Groth16** circuits with **snarkjs** and **rapidsnark** drivers.
- Solidity batch-submission and verification contract; documented **Sepolia** deployment references.
- **EIP-4844 type-3 transactions**, blob encoding and **KZG** commitments.
- Experimental scripts and retained results on proving costs, resources, gas and latency, including documented runs with 8,192-transaction batches.

**Capability illustrated:** implementing and instrumenting the stages of a ZK/L2 pipeline to investigate their costs and bottlenecks.

**Scope:** this is not a production-secure rollup. The circuit exposes a validity signal; state roots and blob contents are not cryptographically bound to that statement. The contract’s `blobhash(0)` check does not establish that binding. Deposits and withdrawals are not implemented.

[Submission contract](https://github.com/roab-912/Zero-Knowledge-Rollup/blob/main/smart_contract/Rollup.sol) · [Experimental scripts](https://github.com/roab-912/Zero-Knowledge-Rollup/tree/main/scripts) · [Retained results](https://github.com/roab-912/Zero-Knowledge-Rollup/tree/main/bench-out)

#### 4. Ariadne — Ethereum investigation with provenance

[Ariadne repository](https://github.com/roab-912/Ariadne) · **Local application v0.2**

A collection and inspection tool that retains source evidence and exposes coverage limitations.

- Bounded address discovery through Etherscan V2, followed by RPC consistency checks across transactions, receipts, logs and blocks.
- Normalization of top-level ETH transfers and standard ERC-20 events.
- Exact amounts using Python integers, PostgreSQL `NUMERIC(78,0)` and decimal strings in the API.
- Inspectable provenance, explicit partial states, idempotent collection and separation of synthetic and collected data.
- Python API, React/TypeScript interface, migrations and dedicated PostgreSQL integration tests.

**Capability illustrated:** producing usable information while preserving provenance, numerical precision and interpretation boundaries.

**Scope:** local single-user operation; internal transfers, entity attribution, cross-chain tracing and continuous reorganization monitoring are outside the implemented scope.

[Normalization](https://github.com/roab-912/Ariadne/blob/main/src/investigation/normalization.py) · [Integration tests](https://github.com/roab-912/Ariadne/tree/main/tests/integration) · [Architecture decisions](https://github.com/roab-912/Ariadne/tree/main/docs/adr)

#### 5. Monitoring Private Blockchain — Besu explorer and verified connection

[Monitoring-Private-Blockchain repository](https://github.com/roab-912/Monitoring-Private-Blockchain) · **v0.1 milestone on a local lab**

An exploration console for a **Besu / QBFT** private blockchain, with persistent indexing and network-identity checks.

- Four-validator laboratory and a separate non-validating RPC node.
- Checks of `chainId`, `networkId` and genesis hash before activating a source.
- Block, transaction, receipt and log indexing; recovery after abrupt termination and explicit suspension on inconsistencies or RPC failure.
- Operator-approved RPC sources, network-destination controls, API/worker separation, roles and persistent quotas.
- Documented verification using real Besu nodes, PostgreSQL and a browser.

**Capability illustrated:** connecting blockchain infrastructure to an observable application with explicit trust boundaries and failure scenarios.

**Scope:** remote administration and validator governance through the interface are future milestones. The local lab shares one physical failure domain.

[Implementation status and evidence](https://github.com/roab-912/Monitoring-Private-Blockchain/blob/main/docs/STATUS.md) · [Documentation](https://github.com/roab-912/Monitoring-Private-Blockchain/tree/main/docs)

### Additional demonstrators and tools

| Public project | Implementation | Exact scope |
| --- | --- | --- |
| [Smart Contract Vulnerability Analyzer](https://github.com/roab-912/Smart-Contract-Vulnerability-Analyzer) | Python Solidity-source analyzer: ten vulnerability classes, vulnerable/corrected examples, CLI/JSON reports and tests | Educational heuristic analysis with possible false positives and negatives; neither a production audit nor bytecode analysis. |
| [Zero-Knowledge Identity System](https://github.com/roab-912/Zero-Knowledge-Identity-System) | Poseidon commitment, Circom circuit and Python-orchestrated Groth16 proving/verification | Knowledge of a secret associated with a commitment; no civil-identity certification or session replay protection. |
| [Zero-Knowledge Recursive](https://github.com/roab-912/Zero-Knowledge-Recursive) | Comparison of N MiMC-transition proofs with one proof of a circuit containing N transitions; measurements and plots | Monolithic computation compression. Proof-in-proof recursion and IVC remain conceptual in this repository. |
| [Custom Blockchain Consensus Simulator](https://github.com/roab-912/Custom-Blockchain-Consensus-Simulator) | PoW/PoS/PoA models, PySide6 interface, throughput/latency/energy analysis and adversarial scenarios | Parameterized simulations; heuristic security scores are neither formal guarantees nor measurements of live networks. |

### Working method

1. **Define the statement and scope:** required property, data, actors and trust assumptions.
2. **Build an inspectable implementation:** separate domain logic, cryptography, persistence and interfaces; document decisions.
3. **Test the boundaries:** invalid proofs, inconsistent data, insufficient permissions, failures and recovery.
4. **Measure with explicit context:** parameters, environment, costs, raw results and limits to generalization.
5. **Qualify conclusions:** distinguish specification, implemented behavior, local validation and production qualification.

### Technologies used

| Area | Technologies present in the projects |
| --- | --- |
| ZK and cryptography | Circom, Noir, Groth16, UltraHonk, PLONK, experimental FFLONK, snarkjs, rapidsnark, Poseidon, KZG, Semaphore, ElectionGuard, P-256 |
| Blockchain | Ethereum/EVM, Solidity, Sepolia, EIP-4844, Besu, QBFT, CometBFT, JSON-RPC |
| Backend and data | Python, Go, JavaScript, TypeScript, Node.js, FastAPI, PostgreSQL, SQLite |
| Interfaces and analysis | React, PWA, Web Workers, PySide6, NumPy, Matplotlib |
| Validation and operations | Docker Compose, migrations, unit and integration tests, Playwright, fuzzing in Civora, architecture documentation |

### Research and collaboration

This work provides a basis for research discussions and engagements involving **ZK prototyping**, **blockchain architecture**, **performance evaluation**, **application security**, and **verification or investigation tooling**.

For research supervisors, the repositories expose models, experimental choices and limitations. For clients, they show my ability to connect a requirement to concrete components: circuits, APIs, storage, interfaces, tests and documentation.

**Contact:** [LinkedIn — Rémi Barbier](https://www.linkedin.com/in/r%C3%A9mi-barbier-2a713b179/).

---

<sub>Portfolio fondé sur les dépôts publics consultés le 9 novembre 2026. Les validations citées sont celles documentées dans les dépôts ; elles ne constituent pas une certification indépendante. Les conditions de réutilisation sont propres à chaque dépôt. / Portfolio based on public repositories reviewed on 9 November 2026. Referenced validations are those documented in the repositories and do not constitute independent certification. Reuse terms are repository-specific.</sub>
