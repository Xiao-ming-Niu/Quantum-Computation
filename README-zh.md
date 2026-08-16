# 量子计算讲义笔记

一套**中文量子计算讲义**与**配套 Python 实现**的双轨仓库,主线聚焦 **"量子算法用于科学计算"**。内容从量子计算的基础语言(量子比特、测量、量子门)出发,经过核心算法构件(QFT、QPE、振幅放大、哈密顿量模拟),统一到现代量子算法框架(Block-encoding、Qubitization、LCU、QSP/QSVT),最终落脚于科学计算的前沿——偏微分方程(PDE)的量子模拟与薛定谔化方法。

## 项目亮点

- **讲义与代码双轨对应**:`Notes/` 下的四模块 LaTeX 讲义与 `Code/` 下的 notebook 一一对应,讲义讲清"为什么",代码演示"怎么做";
- **渐进式实现路线**:9 个 notebook 覆盖 [实现路线图](Code/量子算法实现路线图.md) 的主体(Grover → AA/OAA → QFT/QPE → 哈密顿量模拟 → LCU/Block-Encoding → Qubitization → QSP → QSVT → HHL),每个算法附带**电路图(SVG)与数值结果**;
- **统一实验模板**:每个算法严格按 **数学原理 → 手写实现 → 官方实现 → 数值验证 → 电路图 → 结果分析** 完成,优先使用 `unitarylab` / `unitarylab_algorithms`,必要时再回退到 `Qiskit`;
- **严谨的 LaTeX 排版**:讲义采用 `ctexcap` + `physics` + `qcircuit`,以"定义—定理—引理—例"结构展开,含量子电路图。

## 仓库结构

```text
Quantum-Computation/
├── README.md                 # 项目说明(英文)
├── README-zh.md              # 项目说明(中文,本文档)
├── Notes/                    # 讲义笔记(LaTeX 源文件 + PDF)
│   ├── Model1_QuantumComputationBasics/          # 模块一:量子计算数学基础
│   ├── Model2_CoreQuantumAlgorithmComponents/    # 模块二:核心量子算法构件
│   ├── Model3_ModernFrameworkForQuantumAlgorithms/# 模块三:现代量子算法统一框架
│   └── Model4_Schrodingerization/                # 模块四:薛定谔化方法
└── Code/                     # 算法实现(notebook + 运行结果)
    ├── 量子算法实现路线图.md    # 实现路线图与统一实验模板
    ├── Grover.ipynb           # Grover 搜索
    ├── AA-OAA.ipynb           # 振幅放大(AA/OAA)
    ├── QFT-QPE.ipynb          # QFT 与 QPE
    ├── Suzuki_Trotter-Taylor_Series.ipynb  # 哈密顿量模拟(Trotter / Taylor)
    ├── LCU-BE.ipynb           # LCU 与 Block-Encoding
    ├── Qubitization.ipynb     # Qubitization + Chebyshev
    ├── QSP.ipynb              # QSP 与 QSP 哈密顿量模拟
    ├── QSVT.ipynb             # QSVT 与量子线性求解
    ├── HHL.ipynb              # HHL 线性方程组求解
    └── results/               # 运行结果(电路图 SVG + 数值结果)
        ├── fundamental_algorithm/    # 基础算法:grover、AA/OAA、QPE
        ├── hamiltonian_simulation/   # 哈密顿量模拟:trotter、taylor、qsp
        └── linear_algebra/           # 线性代数:qft、lcu、qsp、hhl、qsvt_qlsa
```

## 内容概览:讲义(Notes/)

| 模块 | 主题 | PDF | LaTeX 源文件 |
| ------ | ------ | ----- | -------------- |
| [Model 1](#模块一量子计算数学基础) | 量子计算数学基础 | [PDF](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.pdf) | [tex](Notes/Model1_QuantumComputationBasics/QuantumComputationBasics.tex) |
| [Model 2](#模块二核心量子算法构件) | 核心量子算法构件 | [PDF](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.pdf) | [tex](Notes/Model2_CoreQuantumAlgorithmComponents/CoreQuantumAlgorithmComponents.tex) |
| [Model 3](#模块三现代量子算法统一框架) | 现代量子算法统一框架 | [PDF](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.pdf) | [tex](Notes/Model3_ModernFrameworkForQuantumAlgorithms/ModernFrameworkForQuantumAlgorithms.tex) |
| [Model 4](#模块四薛定谔化方法) | 薛定谔化方法 | [PDF](Notes/Model4_Schrodingerization/Schrodingerization.pdf) | [tex](Notes/Model4_Schrodingerization/Schrodingerization.tex) |

### 模块一:量子计算数学基础

**学习目标**:建立量子计算的语言——用 Bra-ket 记号描述量子态、测量与量子门,理解量子力学四大公设及其对计算的约束。

与经典的 Newton 力学不同,量子力学从四条数学公设出发推导一切可观测结论,后续所有算法、协议与约束都建立在这四大公设之上。

- **量子力学的公理体系(四大假设)**:态空间公设、演化公设、测量公设、复合系统公设;
- **量子比特**:单量子比特、Bloch 球表示、多量子比特与张量积、密度算子;
- **量子逻辑门**:单量子比特门(Pauli / 旋转门)、多量子比特门(CNOT / SWAP / Toffoli)、通用门集与 Solovay–Kitaev 定理、量子电路与可逆计算;
- **量子测量**:投影测量与可观测量、一般测量算子与 POVM、测量的两个基本原理、期望值估计(Hadamard 检验)、测量与采样误差;
- **量子力学基本约束**:不可克隆定理、不可删除定理、测量坍缩的不可逆性、纠缠(超越乘积态的约束与资源);
- **量子算法的评价框架**:算法的一般结构、复杂度度量、误差分析(混合论证与误差线性增长)、容错计算与阈值定理。

### 模块二:核心量子算法构件

**学习目标**:掌握四类量子算法原语——QFT、QPE、振幅放大、Lie–Trotter 哈密顿量模拟——的定义、电路与复杂度,理解它们为何是几乎所有量子算法的子程序。

几乎所有量子算法都以以下四类**量子算法原语**为子程序。

- **量子傅里叶变换(QFT)**:定义与基本性质、二进制分解与张量积结构、电路实现 $O(n^2)$;
- **量子相位估计(QPE)**:问题设定与 Hadamard 检验、受控 $U^{2^j}$ 与二进制分解、QFT 基 QPE 电路、误差分析(常数成功概率下 $T = O(1/\varepsilon)$;失败概率 $\delta$ 时 $t = d + \lceil\log_2\delta^{-1}\rceil$)、应用:振幅估计;
- **振幅放大(AA)与最优振幅放大(OAA)**:Grover 搜索(振幅放大的原型)、一般框架(几何旋转、信号比特)、已知 $p$ 的确定性放大;
- **Lie–Trotter 与哈密顿量模拟**:问题设定、Lie 乘积公式与一阶 Trotter、交换子型误差界、对称分裂与高阶 Suzuki 公式、局部演化的实现与交换情形。

QFT / QPE / AA 的电路图均用 `qcircuit` 宏包绘制。

### 模块三:现代量子算法统一框架

**学习目标**:理解 Block-encoding → Qubitization → LCU → QSP/QSVT 的统一框架,掌握"如何把矩阵函数变换实现为量子电路"这一现代量子算法设计的核心能力。

Module 2 中的原语都要处理**非酉的对象**,本模块用三个层层递进的概念把它们统一到"矩阵函数变换"的框架之下。

- **Block-encoding(非酉矩阵的输入模型)**:输入模型与矩阵查询 oracle、$(\alpha,m,\varepsilon)$-BE 定义、若干构造(对角 / SVD / s-稀疏 / Hermitian)、基本运算(共轭转置 / 乘积 / 张量积 / 加法);
- **Qubitization(把反射变成旋转)**:标量启发(旋转与 Chebyshev 多项式)、Hermitian BE 的 qubitization、一般 BE 的 qubitization;
- **LCU(线性组合的量子实现)**:prepare / select 结构、引理与证明、oblivious 振幅放大;
- **QSP 与 QET(相位因子编码多项式)**:标量表示定理、奇偶性条件、实多项式、量子本征值变换;
- **QSVT(奇异值变换)**:广义矩阵函数、一般矩阵的 qubitization 与 QSVT 定理、矩阵膨胀(厄米膨胀等价);
- **应用**:Jacobi–Anger 展开的哈密顿量模拟 $O(t + \log(1/\varepsilon)/\log\log(1/\varepsilon))$、线性方程组求解(QLSP) $O(\kappa^2 \log(\kappa/\varepsilon))$、基态制备与固定点振幅放大。

### 模块四:薛定谔化方法

**学习目标**:理解 HHL 与主流哈密顿量模拟方法的优劣;掌握薛定谔化方法(Schrödingerization),能把线性方程组与 PDE 转化为可量子求解的形式。

本模块把前三模块建立的构件用于**科学计算**,特别是线性方程组与偏微分方程(PDE)的量子求解。

- **HHL 算法(求解线性方程组)**:问题设定、算法描述、受控旋转的实现、复杂度分析 $O(\kappa^2/\varepsilon)$(含振幅放大)、与 QSVT-HHL 的对比;
- **常用哈密顿量模拟方法综述**:Trotter/Suzuki 乘积公式、Taylor 级数法与 LCU、Qubitization 与 QSVT 方法、对比与选择;
- **薛定谔化方法(Schrödingerization)**:动机(PDE 的量子模拟)、warped phase transformation(半正定情形 $v = e^{-p}u \to i\partial_t \hat{v} = -\xi L \hat{v}$;一般情形 $A = H_1 - iH_2 \to i\partial_t \hat{v} = (\eta H_1 + H_2)\hat{v}$)、恢复定理与恢复区间、smooth initialization(最优 $\mu_{\max} = O(\log(1/\varepsilon))$)、薛定谔化的五步流程、热方程与对流方程(迎风格式)两个例子、带源项增广与自治化、复杂度与量子优势;
- **酉化方法族**:薛定谔化、LCHS、Transmutation 与 moment-matching dilation 的统一视角与选择准则;
- **文献与延伸**:薛定谔化方法的最新进展(Jin–Liu–Yu PRA 2023 / PRL 2024、Hu–Jin–Liu–Zhang Quantum 2024 等)。

## 内容概览:代码实现(Code/)

遵循 [量子算法实现路线图](Code/量子算法实现路线图.md) 的规划,每个算法统一按 **数学原理 → 手写实现 → 官方实现 → 数值验证 → 电路图 → 结果分析** 的模板完成,优先使用 `unitarylab` / `unitarylab_algorithms`,必要时再使用 `Qiskit`。已实现以下 notebook(按路线图顺序):

| # | Notebook | 内容 | 运行结果 |
| -- | --------- | ------ | --------- |
| 1 | [Grover.ipynb](Code/Grover.ipynb) | Grover 搜索:初始态、Oracle、Diffuser、多次迭代的几何解释;手写与官方实现对比 | [grover](Code/results/fundamental_algorithm/grover/) |
| 2 | [AA-OAA.ipynb](Code/AA-OAA.ipynb) | 振幅放大(AA)与最优振幅放大(OAA):与 Grover 的关系、good/bad subspace、反射、OAA 关键 projection 与数值实验 | [amplitude_amplification](Code/results/fundamental_algorithm/amplitude_amplification/) |
| 3 | [QFT-QPE.ipynb](Code/QFT-QPE.ipynb) | QFT 的数学定义与酉性、QFT 与相位的关系;QPE 问题设定、寄存器与三步执行流程(Hadamard → 受控 U → 逆 QFT)及数值实现 | [qft](Code/results/linear_algebra/qft/)、[qpe](Code/results/fundamental_algorithm/qpe/) |
| 4 | [Suzuki_Trotter-Taylor_Series.ipynb](Code/Suzuki_Trotter-Taylor_Series.ipynb) | 哈密顿量模拟:Lie–Trotter / Suzuki 乘积公式与 Taylor 级数法(截断 + LCU) | [trotter](Code/results/hamiltonian_simulation/trotter/)、[taylor](Code/results/hamiltonian_simulation/taylor/) |
| 5 | [LCU-BE.ipynb](Code/LCU-BE.ipynb) | LCU(prepare / select、后选择得到 $A/\alpha$)与 Block-Encoding 的定义、$\alpha$ 的意义、手写构造与不唯一性 | [lcu](Code/results/linear_algebra/lcu/) |
| 6 | [Qubitization.ipynb](Code/Qubitization.ipynb) | Qubitization + Chebyshev + Qubitized Walk:从 Block-Encoding 到旋转、为何需要 Qubitization、Chebyshev 多项式的出现 | —(数值实验在 notebook 内,未单独导出) |
| 7 | [QSP.ipynb](Code/QSP.ipynb) | QSP:从 Chebyshev 到 QSP、Phase Gate、表示定理、奇偶性约束、多项式逼近与 QSP 哈密顿量模拟 | [qsp](Code/results/linear_algebra/qsp/)、[qsp_ham_sim](Code/results/hamiltonian_simulation/qsp/) |
| 8 | [QSVT.ipynb](Code/QSVT.ipynb) | QSVT:从 QSP 到 QSVT、SVD、奇变换、实验 $p(x)=x^3$;以及量子线性系统求解(逆多项式、缩放因子) | [qsvt_qlsa](Code/results/linear_algebra/qsvt_qlsa/) |
| 9 | [HHL.ipynb](Code/HHL.ipynb) | HHL 线性方程组求解:问题设定、厄米性要求、QPE → 受控旋转 → 逆 QPE → 后选择的完整流程与成功概率分析 | [hhl](Code/results/linear_algebra/hhl/) |

> 每个 `results` 子目录均包含**电路图(SVG)** 与 **数值结果(txt)**;部分 notebook 还直接内嵌 matplotlib 数值对比图。

## 快速开始

### 阅读讲义

直接打开 `Notes/` 下各模块的 **PDF**(见[内容概览](#内容概览讲义notes));或按[编译说明](#编译说明)从 LaTeX 源文件自行编译。

### 运行 notebook

环境要求:

- Python 3 + Jupyter(Notebook / Lab);
- 科学计算库:`numpy`、`matplotlib`,`scipy`(QSP 等 notebook 需要);
- 量子模拟库:`unitarylab` / `unitarylab_algorithms`(各 notebook 首个代码 cell 已包含相关导入,可按其提示安装)。

启动方式:

```bash
jupyter notebook
```

打开 `Code/` 下任一 notebook,按顺序执行 cell 即可复现结果;运行产物会写入对应的 `results/` 子目录。

### 编译讲义

```bash
cd Notes/Model1_QuantumComputationBasics
xelatex QuantumComputationBasics.tex
```

详细说明见[编译说明](#编译说明)。

## 学习路径建议

**前置知识**:

- **线性代数**:矩阵、特征值分解、奇异值分解(SVD)——讲义会用到但建议提前熟悉;
- **Python 基础**:`numpy` 向量化操作、Jupyter 使用;
- **量子力学**:可选。讲义从量子力学的四大公设讲起,无需先修。

**推荐顺序**:

1. 讲义按 `Model1 → Model2 → Model3 → Model4` 顺序精读,建立完整知识链:
   语言 → 构件 → 统一框架 → 科学计算应用;
2. 代码按 `1 → 9`(路线图顺序)动手实现,每个算法先手写、再与官方实现对比、最后验证数值;
3. 完成 QSVT 与 HHL 后,即可进入最终目标——**PDE 求解**(路线图第 18 步)。

## 参考文献与资料来源

讲义主要参考以下材料整理而成:

1. **Lin Lin**, *Lecture Notes on Quantum Algorithms for Scientific Computation* (2022)——模块一的数学基础,及模块二、模块三的主要来源;
2. **Lin Lin & Nathan Wiebe**, *Quantum Algorithms for Scientific Computation* (2026)——模块二的补充来源;
3. **Xiantao Li**, *A Quantum Path to Partial Differential Equations*(讲义,2026),[arXiv:2607.09639](https://arxiv.org/abs/2607.09639)——模块四的来源;
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

