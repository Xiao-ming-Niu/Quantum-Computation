# Quantum-Computation Lecture Notes

A repository of **Chinese lecture notes on quantum computing** together with **accompanying Python implementations**, centered on the theme of **quantum algorithms for scientific computation**. The content starts from the basic language of quantum computing (qubits, measurement, quantum gates), progresses through the core algorithm primitives (QFT, QPE, amplitude amplification, Hamiltonian simulation), unifies them under the modern quantum algorithm framework (Block-encoding, Qubitization, LCU, QSP/QSVT), and finally arrives at the frontier of scientific computation — the quantum simulation of partial differential equations (PDEs) and the Schrödingerization method.

## Highlights

- **Dual-track notes and code**: the four LaTeX modules under `Notes/` and the notebooks under `Code/` correspond one-to-one — the notes explain "why", the code demonstrates "how";
- **A progressive implementation roadmap**: 9 notebooks cover the core of the [implementation roadmap](Code/量子算法实现路线图.md) (Grover → AA/OAA → QFT/QPE → Hamiltonian simulation → LCU/Block-Encoding → Qubitization → QSP → QSVT → HHL), each with **circuit diagrams (SVG) and numerical results**;
- **A unified experiment template**: every algorithm strictly follows **mathematics → hand-written implementation → official implementation → numerical verification → circuit diagram → result analysis**, preferring `unitarylab` / `unitarylab_algorithms` and falling back to `Qiskit` only when necessary;
- **Rigorous LaTeX typesetting**: the notes are built with `ctexcap` + `physics` + `qcircuit`, developed in a "Definition–Theorem–Lemma–Example" structure, including quantum circuit diagrams.

## Repository Structure

```text
Quantum-Computation/
├── README.md                 # Project description (English)
├── README-zh.md              # Project description (Chinese)
├── Notes/                    # Lecture notes (LaTeX source + PDF)
│   ├── Model1_QuantumComputationBasics/          # Model 1: Mathematical foundations of quantum computing
│   ├── Model2_CoreQuantumAlgorithmComponents/    # Model 2: Core quantum algorithm components
│   ├── Model3_ModernFrameworkForQuantumAlgorithms/# Model 3: Modern framework for quantum algorithms
│   └── Model4_Schrodingerization/                # Model 4: Schrödingerization method
└── Code/                     # Algorithm implementations (notebooks + results)
    ├── 量子算法实现路线图.md    # Implementation roadmap & unified experiment template
    ├── Grover.ipynb           # Grover search
    ├── AA-OAA.ipynb           # Amplitude amplification (AA/OAA)
    ├── QFT-QPE.ipynb          # QFT and QPE
    ├── Suzuki_Trotter-Taylor_Series.ipynb  # Hamiltonian simulation (Trotter / Taylor)
    ├── LCU-BE.ipynb           # LCU and Block-Encoding
    ├── Qubitization.ipynb     # Qubitization + Chebyshev
    ├── QSP.ipynb              # QSP and QSP Hamiltonian simulation
    ├── QSVT.ipynb             # QSVT and quantum linear-system solving
    ├── HHL.ipynb              # HHL linear-system solver
    └── results/               # Run outputs (circuit SVGs + numerical results)
        ├── fundamental_algorithm/    # Fundamental algorithms: grover, AA/OAA, QPE
        ├── hamiltonian_simulation/   # Hamiltonian simulation: trotter, taylor, qsp
        └── linear_algebra/           # Linear algebra: qft, lcu, qsp, hhl, qsvt_qlsa
```

## Notes Overview (Notes/)

| Module | Topic | PDF | LaTeX source |
| ------ | ------ | ----- | -------------- |
| [Model 1](#model-1-mathematical-foundations-of-quantum-computing) | Mathematical foundations of quantum computing | [PDF](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.pdf) | [tex](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.tex) |
| [Model 2](#model-2-core-quantum-algorithm-components) | Core quantum algorithm components | [PDF](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.pdf) | [tex](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.tex) |
| [Model 3](#model-3-modern-framework-for-quantum-algorithms) | Modern framework for quantum algorithms | [PDF](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.pdf) | [tex](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.tex) |
| [Model 4](#model-4-schrödingerization-method) | Schrödingerization method | [PDF](Notes/Model4_Schrodingerization/Schrodingerization.pdf) | [tex](Notes/Model4_Schrodingerization/Schrodingerization.tex) |

### Model 1: Mathematical Foundations of Quantum Computing

**Learning objective**: build the language of quantum computing — describe quantum states, measurement, and quantum gates in Bra-ket notation, and understand the four postulates of quantum mechanics and their constraints on computation.

Unlike classical Newtonian mechanics, quantum mechanics derives all observable conclusions from four mathematical postulates; every subsequent algorithm, protocol, and constraint builds upon these four postulates.

- **Axioms of quantum mechanics (the four postulates)**: state-space postulate, evolution postulate, measurement postulate, composite-system postulate;
- **Qubits**: single qubit, Bloch sphere representation, multiple qubits and tensor products, density operators;
- **Quantum logic gates**: single-qubit gates (Pauli / rotation gates), multi-qubit gates (CNOT / SWAP / Toffoli), universal gate sets and the Solovay–Kitaev theorem, quantum circuits and reversible computing;
- **Quantum measurement**: projective measurements and observables, general measurement operators and POVM, two basic principles of measurement, expectation-value estimation (the Hadamard test), measurement and sampling error;
- **Fundamental constraints of quantum mechanics**: the no-cloning theorem, the no-deleting theorem, the irreversibility of measurement collapse, entanglement (constraints and resources beyond product states);
- **A framework for evaluating quantum algorithms**: general structure of quantum algorithms, complexity measures, error analysis (hybrid arguments and linear error growth), fault-tolerant computing and the threshold theorem.

### Model 2: Core Quantum Algorithm Components

**Learning objective**: master the definitions, circuits, and complexity of four quantum algorithm primitives — QFT, QPE, amplitude amplification, and Lie–Trotter Hamiltonian simulation — and understand why they serve as subroutines of almost every quantum algorithm.

Almost every quantum algorithm uses the following four **quantum algorithm primitives** as subroutines.

- **Quantum Fourier transform (QFT)**: definition and basic properties, binary decomposition and tensor-product structure, circuit implementation in $O(n^2)$;
- **Quantum phase estimation (QPE)**: problem setup and the Hadamard test, controlled-$U^{2^j}$ and binary decomposition, the QFT-based QPE circuit, error analysis ($T = O(1/\varepsilon)$ at constant success probability; $t = d + \lceil\log_2\delta^{-1}\rceil$ for failure probability $\delta$), application: amplitude estimation;
- **Amplitude amplification (AA) and optimal amplitude amplification (OAA)**: Grover search (the prototype of amplitude amplification), the general framework (geometric rotations, signal bits), deterministic amplification for known $p$;
- **Lie–Trotter and Hamiltonian simulation**: problem setup, the Lie product formula and first-order Trotter, commutator-based error bounds, symmetric splitting and higher-order Suzuki formulas, implementing local evolutions and the commuting case.

QFT / QPE / AA circuits are drawn with the `qcircuit` package.

### Model 3: Modern Framework for Quantum Algorithms

**Learning objective**: understand the unified framework of Block-encoding → Qubitization → LCU → QSP/QSVT, and master the core capability of modern quantum algorithm design — implementing matrix-function transformations as quantum circuits.

The primitives in Model 2 must all handle **non-unitary objects**; this module unifies them under a "matrix-function transformation" framework built from three progressively deeper concepts.

- **Block-encoding (input model for non-unitary matrices)**: input models and matrix-query oracles, the $(\alpha, m, \varepsilon)$-BE definition, several constructions (diagonal / SVD / $s$-sparse / Hermitian), basic operations (conjugate transpose / product / tensor product / addition);
- **Qubitization (turning reflections into rotations)**: a scalar heuristic (rotations and Chebyshev polynomials), qubitization of Hermitian BE, qubitization of general BE;
- **LCU (quantum implementation of linear combinations)**: prepare / select structure, lemma and proof, oblivious amplitude amplification;
- **QSP and QET (encoding polynomials in phase factors)**: scalar representation theorem, parity conditions, real polynomials, quantum eigenvalue transformation;
- **QSVT (singular value transformation)**: generalized matrix functions, qubitization of general matrices and the QSVT theorem, matrix dilation (Hermitian-dilation equivalence);
- **Applications**: Hamiltonian simulation via the Jacobi–Anger expansion in $O(t + \log(1/\varepsilon)/\log\log(1/\varepsilon))$, solving linear systems (QLSP) in $O(\kappa^2 \log(\kappa/\varepsilon))$, ground-state preparation and fixed-point amplitude amplification.

### Model 4: Schrödingerization Method

**Learning objective**: understand the strengths and weaknesses of HHL and mainstream Hamiltonian simulation methods; master the Schrödingerization method to cast linear systems and PDEs into quantum-solvable form.

This module applies the components built in the previous three modules to **scientific computing**, in particular the quantum solution of linear systems and partial differential equations (PDEs).

- **The HHL algorithm (solving linear systems)**: problem setup, algorithm description, implementing the controlled rotation, complexity analysis $O(\kappa^2/\varepsilon)$ (including amplitude amplification), comparison with QSVT-HHL;
- **Overview of common Hamiltonian simulation methods**: Trotter/Suzuki product formulas, the Taylor-series approach with LCU, qubitization and QSVT methods, comparison and selection;
- **The Schrödingerization method**: motivation (quantum simulation of PDEs), warped phase transformation (semidefinite case: $v = e^{-p}u \to i\partial_t \hat{v} = -\xi L \hat{v}$; general case: $A = H_1 - iH_2 \to i\partial_t \hat{v} = (\eta H_1 + H_2)\hat{v}$), recovery theorem and recovery intervals, smooth initialization (optimal $\mu_{\max} = O(\log(1/\varepsilon))$), the five-step Schrödingerization workflow, examples of the heat equation and the advection equation (upwind scheme), source-term augmentation and autonomization, complexity and quantum advantage;
- **A family of unitarization methods**: a unified view and selection criteria for Schrödingerization, LCHS, Transmutation, and moment-matching dilation;
- **References and extensions**: the latest advances in Schrödingerization (Jin–Liu–Yu PRA 2023 / PRL 2024, Hu–Jin–Liu–Zhang Quantum 2024, etc.).

## Code Overview (Code/)

Following the [implementation roadmap](Code/量子算法实现路线图.md), every algorithm is completed with the unified template **mathematics → hand-written implementation → official implementation → numerical verification → circuit diagram → result analysis**, preferring `unitarylab` / `unitarylab_algorithms` and falling back to `Qiskit` only when necessary. The following notebooks are implemented (in roadmap order):

| # | Notebook | Content | Run outputs |
| -- | --------- | ------ | --------- |
| 1 | [Grover.ipynb](Code/Grover.ipynb) | Grover search: initial state, Oracle, Diffuser, geometric explanation of multiple iterations; hand-written vs official implementation | [grover](Code/results/fundamental_algorithm/grover/) |
| 2 | [AA-OAA.ipynb](Code/AA-OAA.ipynb) | Amplitude amplification (AA) and optimal amplitude amplification (OAA): relation to Grover, good/bad subspace, reflections, OAA's key projection and numerical experiments | [amplitude_amplification](Code/results/fundamental_algorithm/amplitude_amplification/) |
| 3 | [QFT-QPE.ipynb](Code/QFT-QPE.ipynb) | QFT definition and unitarity, relation between QFT and phases; QPE problem setup, registers and the three-step flow (Hadamard → controlled-U → inverse QFT) with numerical implementation | [qft](Code/results/linear_algebra/qft/), [qpe](Code/results/fundamental_algorithm/qpe/) |
| 4 | [Suzuki_Trotter-Taylor_Series.ipynb](Code/Suzuki_Trotter-Taylor_Series.ipynb) | Hamiltonian simulation: Lie–Trotter / Suzuki product formulas vs the Taylor-series approach (truncation + LCU) | [trotter](Code/results/hamiltonian_simulation/trotter/), [taylor](Code/results/hamiltonian_simulation/taylor/) |
| 5 | [LCU-BE.ipynb](Code/LCU-BE.ipynb) | LCU (prepare / select, post-selecting $A/\alpha$) and Block-Encoding: definition, the role of $\alpha$, hand-written constructions and non-uniqueness | [lcu](Code/results/linear_algebra/lcu/) |
| 6 | [Qubitization.ipynb](Code/Qubitization.ipynb) | Qubitization + Chebyshev + Qubitized Walk: from Block-Encoding to rotations, why Qubitization is needed, the emergence of Chebyshev polynomials | — (numerical experiments inside the notebook, not separately exported) |
| 7 | [QSP.ipynb](Code/QSP.ipynb) | QSP: from Chebyshev to QSP, the Phase Gate, the representation theorem, parity constraints, polynomial approximation and QSP Hamiltonian simulation | [qsp](Code/results/linear_algebra/qsp/), [qsp_ham_sim](Code/results/hamiltonian_simulation/qsp/) |
| 8 | [QSVT.ipynb](Code/QSVT.ipynb) | QSVT: from QSP to QSVT, SVD, odd transformations, experiment $p(x) = x^3$; plus quantum linear-system solving (inverse polynomial, scaling factor) | [qsvt_qlsa](Code/results/linear_algebra/qsvt_qlsa/) |
| 9 | [HHL.ipynb](Code/HHL.ipynb) | HHL linear-system solver: problem setup, the Hermiticity requirement, the full QPE → controlled rotation → inverse QPE → post-selection flow and success-probability analysis | [hhl](Code/results/linear_algebra/hhl/) |

> Each `results` subdirectory contains a **circuit diagram (SVG)** and **numerical results (txt)**; some notebooks also embed matplotlib comparison plots directly.

## Quick Start

### Reading the Notes

Open the **PDFs** of each module under `Notes/` (see [Notes Overview](#notes-overview-notes)); or compile from the LaTeX sources following [Compilation](#compilation).

### Running the Notebooks

Environment requirements:

- Python 3 + Jupyter (Notebook / Lab);
- Scientific computing libraries: `numpy`, `matplotlib`, and `scipy` (needed by notebooks such as QSP);
- Quantum simulation libraries: `unitarylab` / `unitarylab_algorithms` (each notebook's first code cell includes the relevant imports and hints).

To launch:

```bash
jupyter notebook
```

Open any notebook under `Code/` and run the cells in order to reproduce the results; outputs are written to the corresponding `results/` subdirectories.

### Compiling the Notes

```bash
cd Notes/Model1_QuantumComputationBasics
xelatex QuantumComputationBasics.tex
```

See [Compilation](#compilation) for details.

## Suggested Learning Path

**Prerequisites**:

- **Linear algebra**: matrices, eigenvalue decomposition, singular value decomposition (SVD) — used throughout the notes, but recommended to be familiar with beforehand;
- **Python basics**: vectorized `numpy`, Jupyter usage;
- **Quantum mechanics**: optional. The notes start from the four postulates of quantum mechanics, so no prior coursework is required.

**Recommended order**:

1. Read the notes in `Model1 → Model2 → Model3 → Model4` order to build the complete knowledge chain: language → components → unified framework → scientific-computing applications;
2. Implement the code in `1 → 9` (roadmap order), hand-writing each algorithm first, then comparing with the official implementation, and finally verifying numerically;
3. After completing QSVT and HHL, move to the final goal — **PDE solving** (roadmap step 18).

## References and Sources

The notes are primarily compiled from the following materials:

1. **Lin Lin**, *Lecture Notes on Quantum Algorithms for Scientific Computation* (2022) — the mathematical foundations of Model 1, and the main source for Models 2 and 3;
2. **Lin Lin & Nathan Wiebe**, *Quantum Algorithms for Scientific Computation* (2026) — a supplementary source for Model 2;
3. **Xiantao Li**, *A Quantum Path to Partial Differential Equations* (lecture notes, 2026), [arXiv:2607.09639](https://arxiv.org/abs/2607.09639) — the source for Model 4;
4. Classic literature:
   - A. W. Harrow, A. Hassidim, S. Lloyd, *Quantum algorithm for linear systems of equations*, PRL 103, 150502 (2009);
   - A. M. Childs, R. Kothari, R. D. Somma, *Quantum algorithm for systems of linear equations with exponentially improved dependence on precision*, SICOMP 46, 1920 (2017);
   - A. Gilyén, Y. Su, G. H. Low, N. Wiebe, *Quantum singular value transformation and beyond*, STOC 2019;
   - D. W. Berry, A. M. Childs, R. Cleve, R. Kothari, R. D. Somma, *Simulating Hamiltonian dynamics with a truncated Taylor series*, PRL 114, 090502 (2015);
   - G. H. Low, I. L. Chuang, *Hamiltonian simulation by qubitization*, Quantum 3, 163 (2019);
   - Schrödingerization: S. Jin, N. Liu, Y. Yu, *Quantum simulation of partial differential equations via Schrödingerisation: technical details*, PRA 108, 032603 (2023), [arXiv:2212.14703](https://arxiv.org/abs/2212.14703); the same authors, PRL 133, 230602 (2024), [arXiv:2212.13969](https://arxiv.org/abs/2212.13969); J. Hu, S. Jin, N. Liu, L. Zhang, *Quantum circuits for partial differential equations via Schrödingerisation*, Quantum 8, 1563 (2024), [arXiv:2403.10032](https://arxiv.org/abs/2403.10032); see also LCHS [arXiv:2303.01029](https://arxiv.org/abs/2303.01029), near-optimal non-unitary dynamics [arXiv:2312.03916](https://arxiv.org/abs/2312.03916), moment-matching dilation [arXiv:2507.10285](https://arxiv.org/abs/2507.10285), transmutation [arXiv:2601.03616](https://arxiv.org/abs/2601.03616), etc.

## Public Resources

- [arXiv:1806.01838](https://arxiv.org/abs/1806.01838) Gilyén–Su–Low–Wiebe, *Quantum singular value transformation and beyond* (the original QSVT paper);
- [arXiv:1610.06546](https://arxiv.org/abs/1610.06546) Low–Chuang, *Hamiltonian simulation by qubitization*;
- [QSPPACK](https://github.com/qsppack/QSPPACK): numerical solver for QSP/QSVT phase factors.

## Compilation

The notes compile with **XeLaTeX** (tested on TeX Live 2023) and depend on the following packages:

- `ctexcap` (Chinese section titles), `physics` (quantum-mechanical notation);
- `qcircuit` (quantum circuit diagrams; enable with `\usepackage[braket]{qcircuit}`);
- standard math packages `amsmath` / `amsfonts` / `amssymb`, plus table and float packages.

Example:

```bash
cd Notes/Model1_QuantumComputationBasics
xelatex QuantumComputationBasics.tex
```

> **Typesetting note**: the `qcircuit` macros `\ctrl` / `\meter` can only be used inside a `\Qcircuit` environment; using `$\ctrl{1}$` in running text triggers the Xy-pic "save out of context" error. Also, `\multigate` tends to conflict with `\ctrl` in the same circuit — avoid combining them.
