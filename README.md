# Quantum-Computation Lecture Notes

A series of **Chinese lecture notes on quantum computing**, centered on the theme of **quantum algorithms for scientific computation**. The notes start from the basic language of quantum computing (qubits, measurement, quantum gates), progress through the core algorithm primitives (QFT, QPE, amplitude amplification, Hamiltonian simulation), unify them under the modern framework of quantum algorithms (Block-encoding, Qubitization, LCU, QSP/QSVT), and finally arrive at cutting-edge applications in scientific computing — the quantum simulation of partial differential equations and the Schrödingerization method.

The notes are typeset in LaTeX (including quantum circuit diagrams) and developed rigorously in a "Definition–Theorem–Lemma–Example" style, suitable for readers who want to systematically study quantum computing, especially the quantum-for-scientific-computing direction.

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
    ├── QFT-QPE.ipynb          # QFT & QPE
    ├── Suzuki_Trotter-Taylor_Series.ipynb  # Hamiltonian simulation (Trotter / Taylor)
    └── results/               # Run outputs (circuit SVGs + numerical results)
```

## Overview

| Module | Topic | PDF | LaTeX source |
| ------ | ------ | ----- | -------------- |
| [Model 1](#model-1-mathematical-foundations-of-quantum-computing) | Mathematical foundations of quantum computing | [PDF](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.pdf) | [tex](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.tex) |
| [Model 2](#model-2-core-quantum-algorithm-components) | Core quantum algorithm components | [PDF](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.pdf) | [tex](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.tex) |
| [Model 3](#model-3-modern-framework-for-quantum-algorithms) | Modern framework for quantum algorithms | [PDF](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.pdf) | [tex](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.tex) |
| [Model 4](#model-4-schrödingerization-method) | Schrödingerization method | [PDF](Notes/Model4_Schrodingerization/Schrodingerization.pdf) | [tex](Notes/Model4_Schrodingerization/Schrodingerization.tex) |

### Model 1: Mathematical Foundations of Quantum Computing

Unlike classical Newtonian mechanics, quantum mechanics starts from four mathematical postulates and derives all observable conclusions; every subsequent algorithm, protocol, and constraint builds upon these four postulates. This module gives the full language of quantum computing.

- **Axioms of quantum mechanics (the four postulates)**: state-space postulate, evolution postulate, measurement postulate, composite-system postulate;
- **Qubits**: single qubit, Bloch sphere representation, multiple qubits and tensor products, density operators;
- **Quantum logic gates**: single-qubit gates (Pauli / rotation gates), multi-qubit gates (CNOT / SWAP / Toffoli), universal gate sets and the Solovay–Kitaev theorem, quantum circuits and reversible computing;
- **Quantum measurement**: projective measurements and observables, general measurement operators and POVM, two basic principles of measurement, expectation-value estimation (the Hadamard test), measurement and sampling error;
- **Fundamental constraints of quantum mechanics**: the no-cloning theorem, the no-deleting theorem, the irreversibility of measurement collapse, entanglement (constraints and resources beyond product states);
- **A framework for evaluating quantum algorithms**: general structure of quantum algorithms, complexity measures, error analysis (hybrid arguments and linear error growth), fault-tolerant computing and the threshold theorem.

### Model 2: Core Quantum Algorithm Components

Almost every quantum algorithm uses the following four **quantum algorithm primitives** as subroutines.

- **Quantum Fourier transform (QFT)**: definition and basic properties, binary decomposition and tensor-product structure, circuit implementation in $O(n^2)$;
- **Quantum phase estimation (QPE)**: problem setup and the Hadamard test, controlled-$U^{2^j}$ and binary decomposition, the QFT-based QPE circuit, error analysis ($T = O(1/\varepsilon)$ for constant success probability; $t = d + \lceil\log_2\delta^{-1}\rceil$ for failure probability $\delta$), application: amplitude estimation;
- **Amplitude amplification (AA) and optimal amplitude amplification (OAA)**: Grover search (the prototype of amplitude amplification), the general framework (geometric rotations, signal bits), deterministic amplification for known $p$;
- **Lie–Trotter and Hamiltonian simulation**: problem setup, the Lie product formula and first-order Trotter, commutator-based error bounds, symmetric splitting and higher-order Suzuki formulas, implementing local evolutions and the commuting case.

Circuit diagrams for QFT / QPE / AA are drawn with the `qcircuit` package.

### Model 3: Modern Framework for Quantum Algorithms

The primitives in Model 2 must all handle **non-unitary objects**. This module unifies them under a "matrix-function transformation" framework built from three progressively deeper concepts.

- **Block-encoding (an input model for non-unitary matrices)**: input models and matrix-query oracles, the $(\alpha, m, \varepsilon)$-BE definition, several constructions (diagonal / SVD / $s$-sparse / Hermitian), basic calculus (adjoint / product / tensor product / addition);
- **Qubitization (turning reflections into rotations)**: a scalar heuristic (rotations and Chebyshev polynomials), qubitization of Hermitian BE, qubitization of general BE;
- **LCU (quantum implementation of linear combinations)**: prepare/select structure, lemma and proof, oblivious amplitude amplification;
- **QSP and QET (encoding polynomials in phase factors)**: scalar representation theorem, parity conditions, real polynomials, quantum eigenvalue transformation;
- **QSVT (singular value transformation)**: generalized matrix functions, qubitization of general matrices and the QSVT theorem, matrix dilation (Hermitian-dilation equivalence);
- **Applications**: Hamiltonian simulation via the Jacobi–Anger expansion in $O(t + \log(1/\varepsilon)/\log\log(1/\varepsilon))$, solving linear systems (QLSP) in $O(\kappa^2 \log(\kappa/\varepsilon))$, ground-state preparation and fixed-point amplitude amplification.

### Model 4: Schrödingerization Method

This module applies the components built in the previous three modules to **scientific computing**, in particular the quantum solution of linear systems and partial differential equations (PDEs).

- **The HHL algorithm (solving linear systems)**: problem setup, algorithm description, implementation of the controlled rotation, complexity analysis $O(\kappa^2/\varepsilon)$ (including amplitude amplification), comparison with QSVT-HHL;
- **Overview of common Hamiltonian simulation methods**: Trotter/Suzuki product formulas, the Taylor-series approach with LCU, Qubitization and QSVT methods, comparison and choice;
- **The Schrödingerization method**: motivation (quantum simulation of PDEs), warped phase transformation (semidefinite case: $v = e^{-p}u \to i\partial_t \hat{v} = -\xi L \hat{v}$; general case: $A = H_1 - iH_2 \to i\partial_t \hat{v} = (\eta H_1 + H_2)\hat{v}$), recovery theorem and recovery intervals, smooth initialization (optimal $\mu_{\max} = O(\log(1/\varepsilon))$), the five-step Schrödingerization workflow, heat equation and advection equation (upwind scheme) examples, source-term augmentation and autonomization, complexity and quantum advantage;
- **A family of unitarization methods**: a unified view and selection criteria for Schrödingerization, LCHS, Transmutation, and moment-matching dilation;
- **References and extensions**: the latest advances in Schrödingerization (Jin–Liu–Yu PRA 2023 / PRL 2024, Hu–Jin–Liu–Zhang Quantum 2024, etc.).

## Code Implementations (`Code/`)

Following the [implementation roadmap](Code/量子算法实现路线图.md) — each algorithm is completed with the unified template **mathematics → hand-written implementation → official implementation → numerical verification → circuit diagram → result analysis**, preferring `unitarylab_algorithms` / `unitarylab` and falling back to `Qiskit` only when necessary — the following notebooks are implemented:

| Notebook | Content | Run outputs |
| --------- | ------ | --------- |
| [Grover.ipynb](Code/Grover.ipynb) | Grover search: mathematics (initial state, Oracle, Diffuser, why multiple iterations) and hand-written vs official implementation | [grover](Code/results/fundamental_algorithm/grover/) |
| [AA-OAA.ipynb](Code/AA-OAA.ipynb) | Amplitude amplification (AA) and optimal amplitude amplification (OAA): relation to Grover, good/bad subspace, reflections, OAA's key projection, numerical experiments | [amplitude_amplification](Code/results/fundamental_algorithm/amplitude_amplification/) |
| [QFT-QPE.ipynb](Code/QFT-QPE.ipynb) | QFT definition and unitarity, QFT and phases; QPE problem setup, registers and the three-step flow (Hadamard → controlled-U → inverse QFT) with numerical implementation | [qft](Code/results/linear_algebra/qft/), [qpe](Code/results/fundamental_algorithm/qpe/) |
| [Suzuki_Trotter-Taylor_Series.ipynb](Code/Suzuki_Trotter-Taylor_Series.ipynb) | Hamiltonian simulation: Lie–Trotter/Suzuki product formulas vs the Taylor-series approach (truncation + LCU) | [trotter](Code/results/hamiltonian_simulation/trotter/), [taylor](Code/results/hamiltonian_simulation/taylor/) |

The roadmap continues toward **LCU → Block Encoding → Qubitization → QSP/QSVT → quantum linear systems → PDE solving**.

## References and Sources

The notes are primarily compiled from the following materials:

1. **Lin Lin**, *Lecture Notes on Quantum Algorithms for Scientific Computation* (2022) — the mathematical foundations of Model 1, and the main source for Models 2 and 3;
2. **Lin Lin & Nathan Wiebe**, *Quantum Algorithms for Scientific Computation* (2026) — a supplementary source for Model 2;
3. **M4S8 / M4S9 teaching slides** (HHL and PDE quantum simulation, in Chinese) — the source for Model 4;
4. Classic literature:
   - A. W. Harrow, A. Hassidim, S. Lloyd, *Quantum algorithm for linear systems of equations*, PRL 103, 150502 (2009);
   - A. M. Childs, R. Kothari, R. D. Somma, *Quantum algorithm for systems of linear equations with exponentially improved dependence on precision*, SICOMP 46, 1920 (2017);
   - A. Gilyén, Y. Su, G. H. Low, N. Wiebe, *Quantum singular value transformation and beyond*, STOC 2019;
   - D. W. Berry, A. M. Childs, R. Cleve, R. Kothari, R. D. Somma, *Simulating Hamiltonian dynamics with a truncated Taylor series*, PRL 114, 090502 (2015);
   - G. H. Low, I. L. Chuang, *Hamiltonian simulation by qubitization*, Quantum 3, 163 (2019);
- Schrödingerization: S. Jin, N. Liu, Y. Yu, *Quantum simulation of partial differential equations via Schrödingerisation: technical details*, PRA 108, 032603 (2023), [arXiv:2212.14703](https://arxiv.org/abs/2212.14703); the same authors, PRL 133, 230602 (2024), [arXiv:2212.13969](https://arxiv.org/abs/2212.13969); J. Hu, S. Jin, N. Liu, L. Zhang, *Quantum circuits for partial differential equations via Schrödingerisation*, Quantum 8, 1563 (2024), [arXiv:2403.10032](https://arxiv.org/abs/2403.10032); see also LCHS [arXiv:2303.01029](https://arxiv.org/abs/2303.01029), near-optimal non-unitary dynamics [arXiv:2312.03916](https://arxiv.org/abs/2312.03916), moment-matching dilation [arXiv:2507.10285](https://arxiv.org/abs/2507.10285), transmutation [arXiv:2601.03616](https://arxiv.org/abs/2601.03616), etc.

## Public Resources

- [arXiv:1806.01838](https://arxiv.org/abs/1806.01838) Gilyén–Su–Low–Wiebe, *Quantum singular value transformation and beyond*;
- [arXiv:1610.06546](https://arxiv.org/abs/1610.06546) Low–Chuang, *Hamiltonian simulation by qubitization*;
- [QSPPACK](https://github.com/qsppack/QSPPACK): numerical solver for QSP/QSVT phase factors;
- Local reference folder: `G:\Agent_Projects\自学_量子计算_薛定谔化\References` (day16–day19 slides, QASC summer 2026 sections, Schrödingerization circuit notes, and the complete reference archive).

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

## Roadmap

- [x] Roadmap and foundation-algorithm notebooks (Grover, AA/OAA, QFT/QPE, Trotter/Taylor Hamiltonian simulation);
- [ ] Continue along the roadmap: **LCU → Block Encoding → Qubitization → QSP/QSVT → quantum linear systems → PDE solving**;
- [ ] Extend with more frontier topics (e.g., Maxwell equations, interface problems with physical boundary conditions, fractional heat equations, ground-state / thermal-state preparation, etc.).
