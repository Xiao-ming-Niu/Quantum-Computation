# 量子计算讲义笔记

本仓库是一套**中文量子计算讲义**系列笔记,主线聚焦 **"量子算法用于科学计算"**。内容从量子计算的基础语言(量子比特、测量、量子门)出发,经过核心算法构件(QFT、QPE、振幅放大、哈密顿量模拟),统一到现代量子算法框架(Block-encoding、Qubitization、LCU、QSP/QSVT),最后落脚于科学计算的前沿应用——偏微分方程的量子模拟与薛定谔化方法。

全套笔记采用 LaTeX 排版(含量子电路图),内容以"定义—定理—引理—例"的形式严谨展开,适合希望系统学习量子计算、特别是量子科学计算方向的读者。

## 目录结构

```text
Quantum-Computation/
├── README.md                 # 项目说明(英文)
├── README-zh.md              # 项目说明(中文,本文档)
├── Notes/                    # 讲义笔记(LaTeX 源文件 + PDF)
│   ├── Model1_QuantumComputationBasics/          # 模块一:量子计算数学基础
│   ├── Model2_CoreQuantumAlgorithmComponents/    # 模块二:核心量子算法构件
│   ├── Model3_ModernFrameworkForQuantumAlgorithms/# 模块三:现代量子算法统一框架
│   └── Model4_Schrodingerization/                # 模块四:薛定谔化方法
└── Code/                     # 代码(预留,目前为空)
```

## 内容概览

| 模块 | 主题 | PDF | LaTeX 源文件 |
| ------ | ------ | ----- | -------------- |
| [Model 1](#模块一量子计算数学基础) | 量子计算数学基础 | [PDF](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.pdf) | [tex](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.tex) |
| [Model 2](#模块二核心量子算法构件) | 核心量子算法构件 | [PDF](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.pdf) | [tex](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.tex) |
| [Model 3](#模块三现代量子算法统一框架) | 现代量子算法统一框架 | [PDF](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.pdf) | [tex](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.tex) |
| [Model 4](#模块四薛定谔化方法) | 薛定谔化方法 | [PDF](Notes/Model4_Schrodingerization/Schrodingerization.pdf) | [tex](Notes/Model4_Schrodingerization/Schrodingerization.tex) |

### 模块一:量子计算数学基础

与经典的 Newton 力学不同,量子力学从四条数学公设出发推导一切可观测结论,后续所有算法、协议与约束都建立在这四大公设之上。本模块完整给出量子计算的语言。

- **量子力学的公理体系(四大假设)**:态空间公设、演化公设、测量公设、复合系统公设;
- **量子比特**:单量子比特、Bloch 球表示、多量子比特与张量积、密度算子;
- **量子逻辑门**:单量子比特门(Pauli / 旋转门)、多量子比特门(CNOT / SWAP / Toffoli)、通用门集与 Solovay–Kitaev 定理、量子电路与可逆计算;
- **量子测量**:投影测量与可观测量、一般测量算子与 POVM、测量的两个基本原理、期望值估计(Hadamard 检验)、测量与采样误差;
- **量子力学基本约束**:不可克隆定理、不可删除定理、测量坍缩的不可逆性、纠缠(超越乘积态的约束与资源);
- **量子算法的评价框架**:算法的一般结构、复杂度度量、误差分析(混合论证与误差线性增长)、容错计算与阈值定理。

### 模块二:核心量子算法构件

几乎所有量子算法都以以下四类**量子算法原语**为子程序。

- **量子傅里叶变换(QFT)**:定义与基本性质、二进制分解与张量积结构、电路实现 $O(n^2)$;
- **量子相位估计(QPE)**:问题设定与 Hadamard 检验、受控 $U^{2^j}$ 与二进制分解、QFT 基 QPE 电路、误差分析(常数成功概率下 $T = O(1/\varepsilon)$;失败概率 $\delta$ 时 $t = d + \lceil\log_2\delta^{-1}\rceil$)、应用:振幅估计;
- **振幅放大(AA)与最优振幅放大(OAA)**:Grover 搜索(振幅放大的原型)、一般框架(几何旋转、信号比特)、已知 $p$ 的确定性放大;
- **Lie–Trotter 与哈密顿量模拟**:问题设定、Lie 乘积公式与一阶 Trotter、交换子型误差界、对称分裂与高阶 Suzuki 公式、局部演化的实现与交换情形。

QFT / QPE / AA 的电路图均用 `qcircuit` 宏包绘制。

### 模块三:现代量子算法统一框架

Module 2 中的原语都要处理**非酉的对象**,本模块用三个层层递进的概念把它们统一到"矩阵函数变换"的框架之下。

- **Block-encoding(非酉矩阵的输入模型)**:输入模型与矩阵查询 oracle、$(\alpha,m,\varepsilon)$-BE 定义、若干构造(对角 / SVD / s-稀疏 / Hermitian)、基本运算(共轭转置 / 乘积 / 张量积 / 加法);
- **Qubitization(把反射变成旋转)**:标量启发(旋转与 Chebyshev 多项式)、Hermitian BE 的 qubitization、一般 BE 的 qubitization;
- **LCU(线性组合的量子实现)**:prepare / select 结构、引理与证明、oblivious 振幅放大;
- **QSP 与 QET(相位因子编码多项式)**:标量表示定理、奇偶性条件、实多项式、量子本征值变换;
- **QSVT(奇异值变换)**:广义矩阵函数、一般矩阵的 qubitization 与 QSVT 定理、矩阵膨胀(厄米膨胀等价);
- **应用**:Jacobi–Anger 展开的哈密顿量模拟 $O(t + \log(1/\varepsilon)/\log\log(1/\varepsilon))$、线性方程组求解(QLSP) $O(\kappa^2 \log(\kappa/\varepsilon))$、基态制备与固定点振幅放大。

### 模块四:薛定谔化方法

本模块把前三模块建立的构件用于**科学计算**,特别是线性方程组与偏微分方程(PDE)的量子求解。

- **HHL 算法(求解线性方程组)**:问题设定、算法描述、受控旋转的实现、复杂度分析 $O(\kappa^2/\varepsilon)$(含振幅放大)、与 QSVT-HHL 的对比;
- **常用哈密顿量模拟方法综述**:Trotter/Suzuki 乘积公式、Taylor 级数法与 LCU、Qubitization 与 QSVT 方法、对比与选择;
- **薛定谔化方法(Schrödingerization)**:动机(PDE 的量子模拟)、warped phase transformation(半正定情形 $v = e^{-p}u \to i\partial_t \hat{v} = -\xi L \hat{v}$;一般情形 $A = H_1 - iH_2 \to i\partial_t \hat{v} = (\eta H_1 + H_2)\hat{v}$)、恢复定理与恢复区间、smooth initialization(最优 $\mu_{\max} = O(\log(1/\varepsilon))$)、薛定谔化的五步流程、热方程与对流方程(迎风格式)两个例子、带源项增广与自治化、复杂度与量子优势;
- **酉化方法族**:薛定谔化、LCHS、Transmutation 与 moment-matching dilation 的统一视角与选择准则;
- **文献与延伸**:薛定谔化方法的最新进展(Jin–Liu–Yu PRA 2023 / PRL 2024、Hu–Jin–Liu–Zhang Quantum 2024 等)。

## 参考文献与资料来源

讲义主要参考以下材料整理而成:

1. **Lin Lin**, *Lecture Notes on Quantum Algorithms for Scientific Computation* (2022)——模块一的数学基础,及模块二、模块三的主要来源;
2. **Lin Lin & Nathan Wiebe**, *Quantum Algorithms for Scientific Computation* (2026)——模块二的补充来源;
3. **M4S8 / M4S9 教学课件**(HHL 与 PDE 量子模拟,中文)——模块四的来源;
4. 经典文献:
   - A. W. Harrow, A. Hassidim, S. Lloyd, *Quantum algorithm for linear systems of equations*, PRL 103, 150502 (2009);
   - A. M. Childs, R. Kothari, R. D. Somma, *Quantum algorithm for systems of linear equations with exponentially improved dependence on precision*, SICOMP 46, 1920 (2017);
   - A. Gilyén, Y. Su, G. H. Low, N. Wiebe, *Quantum singular value transformation and beyond*, STOC 2019;
   - D. W. Berry, A. M. Childs, R. Cleve, R. Kothari, R. D. Somma, *Simulating Hamiltonian dynamics with a truncated Taylor series*, PRL 114, 090502 (2015);
   - G. H. Low, I. L. Chuang, *Hamiltonian simulation by qubitization*, Quantum 3, 163 (2019);
   - 薛定谔化方法:S. Jin, N. Liu, Y. Yu, *Quantum simulation of partial differential equations via Schrödingerisation: technical details*, PRA 108, 032603 (2023), [arXiv:2212.14703](https://arxiv.org/abs/2212.14703); 同作者 PRL 133, 230602 (2024), [arXiv:2212.13969](https://arxiv.org/abs/2212.13969); J. Hu, S. Jin, N. Liu, L. Zhang, *Quantum circuits for partial differential equations via Schrödingerisation*, Quantum 8, 1563 (2024), [arXiv:2403.10032](https://arxiv.org/abs/2403.10032); 另见 LCHS [arXiv:2303.01029](https://arxiv.org/abs/2303.01029)、near-optimal non-unitary dynamics [arXiv:2312.03916](https://arxiv.org/abs/2312.03916)、moment-matching dilation [arXiv:2507.10285](https://arxiv.org/abs/2507.10285)、transmutation [arXiv:2601.03616](https://arxiv.org/abs/2601.03616) 等。

## 公开资源

- [arXiv:1806.01838](https://arxiv.org/abs/1806.01838) Gilyén–Su–Low–Wiebe, *Quantum singular value transformation and beyond*(QSVT 原始论文);
- [arXiv:1610.06546](https://arxiv.org/abs/1610.06546) Low–Chuang, *Hamiltonian simulation by qubitization*;
- [QSPPACK](https://github.com/qsppack/QSPPACK):QSP/QSVT 相位因子的数值求解工具包;
- 本地参考材料:`G:\Agent_Projects\自学_量子计算_薛定谔化\References` 下的 day16–day19 讲义、
  `QASC_summer_2026_Section_1..5`、`薛定谔化与微分方程量子线路.pdf` 与
  `quantum_computing_and_schrodingerization_complete_notes.pdf` 等。

## 编译说明

笔记使用 **XeLaTeX** 编译(TeX Live 2023 测试通过),依赖以下宏包:

- `ctexcap`(中文章节标题)、`physics`(量子力学符号);
- `qcircuit`(量子电路图,需启用 `\usepackage[braket]{qcircuit}`);
- 常用数学宏包 `amsmath` / `amsfonts` / `amssymb`、表格与浮动体宏包等。

编译示例:

```bash
cd Notes/Model1_QuantumComputationBasics
xelatex QuantumComputationBasics.tex
```

> **排版提示**:`qcircuit` 的 `\ctrl` / `\meter` 等宏只能在 `\Qcircuit` 环境内使用,在正文中用 `$\ctrl{1}$` 会触发 Xy-pic "save out of context" 错误;`\multigate` 与 `\ctrl` 在同一电路中易冲突,应避免组合使用。

## 后续计划

- [ ] 补充配套**代码实现**(`Code/` 目录暂为空),可考虑 Qiskit / PennyLane 等框架的电路复现;
- [ ] 扩展更多前沿主题(如 Maxwell 方程、带物理边界条件的界面问题、分数阶热方程、量子态基态/热态制备等)。
