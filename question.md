# 审稿问题梳理与旧稿对应原文摘录（question.md）

本文件按审稿人逐条罗列问题，并为每条问题摘录 paper_old.tex 中与之最相关的原文（含文件与起始行标注），以便后续逐条对照修改与撰写回复。

## Referee 1

- 问题 1：建议重写 Section 6.2（更全面并加入近期综述），并补充对非以太坊（其他 EVM 链）FSC 的讨论。
  - 原文摘录 A（Threats to Validity 对非以太坊链的讨论）
    - 文件：`paper_old.tex:860`
    - 摘录：
      > This study has the following limitations that can be further improved in future works. Firstly, we currently only focus on smart contracts on Ethereum; we can expand the scope of our research to other EVM-compatible chains, such as Polygon, Arbitrum, and Optimism, thereby making the study more comprehensive. Furthermore, with the development of the Ethereum ecosystem, new implementation patterns of factory-related smart contracts are constantly emerging, such as create3 factories \cite{eip-3171}. We will further complement these implementation patterns and the corresponding security considerations.
  - 原文摘录 B（Related Work – Security Analysis 小节当前内容的广度）
    - 文件：`paper_old.tex:868`
    - 摘录：
      > Given the relevance of smart contracts to the finance, substantial researches \cite{DBLP:conf/kbse/XueMLSYP20,DBLP:conf/issta/LiaoZCN22,DBLP:conf/issta/GhalebRP22,DBLP:journals/pacmpl/GrechKJBSS18,DBLP:conf/uss/0001L21,DBLP:conf/pldi/BrentGLSS20, DBLP:conf/ccs/DuanZPLLX022} are conducted in the field of smart contract security analysis. ... However, with the diversification of contract patterns and increased composability, these tools may struggle to identify vulnerabilities that arise in specific context, leaving this aspect relatively unexplored. USCHunt \cite{DBLP:conf/uss/BodellMD23} focus on security issues with proxy-based upgradeable patterns, identifying six types of vulnerabilities and discovering 2546 insecure contracts across blockchains. ... To the best of our knowledge, these tools have not specifically addressed security issues in the factory context. Our work fills this gap by thoroughly examining four security issues related to FSCs, providing case studies and outlining their triggering conditions.

## Referee 2

- 问题 1（数据集范围 <1%，需明确限制并避免过度外推）：
  - 原文摘录 A（仅使用已验证合约的数据集说明）
    - 文件：`paper_old.tex:435`
    - 摘录：
      > We first use a widely used open-source smart contract dataset \cite{opensourcedata} to obtain 482,542 verified smart contract addresses deployed on the Ethereum mainnet. These contracts were deployed between 2017 and 2024. Next, we leverage the blockchain explorer Etherscan \cite{etherscan} to collect the source code for these contracts.
  - 原文摘录 B（可能引发“对整个以太坊生态普遍化结论”的表述）
    - 文件：`paper_old.tex:303`
    - 摘录：
      > Then we conduct a large-scale empirical analysis on 482,542 Ethereum contracts ... Our findings reveal that factory contracts dominate in contract deployment, with an average of 92.7\% of Ethereum contracts deployed by factories.

- 问题 2（四个安全检测器的可泛化性；需讨论字节码支持及技术挑战）：
  - 原文摘录（验证/未验证合约上的工厂检测实现与局限）
    - 文件：`paper_old.tex:443`
    - 摘录：
      > Our FSC detector identifies factory contracts using the following two schemes: For verified contract with public source code, the detector utilizes Slither \cite{slither-tool} to query and compile the source code into IR. It then checks each function’s IR for \textit{new Contract()}, \textit{create}, or \textit{create2} opcodes. ... For unverified contracts, we attempt to retrieve the bytecode and disassemble it to detect create or create2 opcodes. However, ... disassemblers ... do not accurately translate bytecode ... Therefore, This method leads to false positives ... Consequently, the detector detects factory contracts based on on-chain transactions. ... it further checks if there are multiple transaction records with the \textit{create} or \textit{create2} type. If so, it suggests that the contract ... thus identifying the contract as a factory.

- 问题 3（聚类仅依赖合约名称，可能引入噪声；建议引入代码特征）：
  - 原文摘录 A（名称向量 + 聚类 + 人工复核）
    - 文件：`paper_old.tex:463`
    - 摘录：
      > ... We conduct a clustering analysis ... The specific steps involved converting contract names into vector embeddings using Word2Vec \cite{DBLP:journals/corr/word2vec}, capturing semantic associations with clustering algorithms, and manually reviewing the clustering results by identifying the constructs incorporating EIP protocol name as part of their names.
  - 原文摘录 B（聚类结果描述方式）
    - 文件：`paper_old.tex:510`
    - 摘录：
      > By conducting a cluster analysis on the collected FSCs, we identify four relatively clear clusters and categorize the remainder as miscellaneous. Upon manually reviewing the clustering outcomes, we discern the principal applications of FSCs ...

- 问题 4（除 Tornado Cash 外缺少具体现实攻击/损失案例）：
  - 原文摘录 A（仅给出 Tornado Cash 案例的表述）
    - 文件：`paper_old.tex:652`
    - 摘录：
      > In the following, we will first conduct a case study of the Tornado Cash governance attack \cite{tornado-cash-attack}, in which the attacker leveraged the metamorphic pattern ... and then provide a simplified implementation of the metamorphic pattern.
  - 原文摘录 B（安全问题总量与“案例研究”表述）
    - 文件：`paper_old.tex:646`
    - 摘录：
      > We ultimately find 1,180 real-world smart contracts with four type of security issues using developed detectors. ... Next, we present in-depth case studies, outlining impacts and solutions.

- 问题 5（除 create2 相关问题外，未讨论可升级合约的其他风险，如代理存储冲突）：
  - 原文摘录（Related Work 提及但正文未展开存储冲突等）
    - 文件：`paper_old.tex:868`
    - 摘录：
      > ... USCHunt \cite{DBLP:conf/uss/BodellMD23} focus on security issues with proxy-based upgradeable patterns, identifying six types of vulnerabilities and discovering 2546 insecure contracts across blockchains. ... To the best of our knowledge, these tools have not specifically addressed security issues in the factory context.

- 问题 6（“Mutable Code”检测可能有误报；需说明权限检查路径处理或给出精确率/召回率）：
  - 原文摘录 A（Mutable Code 检测总体描述与算法）
    - 文件：`paper_old.tex:476`
    - 摘录：
      > Then, we implement four static detectors at the source code level, each addressing specific security issues: the \textit{Mutable Code Detector}, ... Specifically, the \textit{Mutable Code Detector} ... performs cross-contract inter-procedural control flow analysis ... to identify whether a contract modifies its code in place after self-destruction. ... We will discuss the specific implementation of each detector in detail in Section~\ref{sec:rq4securityrisks}.
  - 原文摘录 B（对“变形/可变代码”结果的人工核验，但未提供整体精确率/召回率）
    - 文件：`paper_old.tex:724`
    - 摘录：
      > ... We conduct cross-contract analysis based on the contract deployment chain, revealing a total of 91 metamorphic factory-deployed contracts. We manually verify them to ensure no false positives.

- 拼写/标注问题：
  - 原文摘录 A（USCHunt 动词单复数）
    - 文件：`paper_old.tex:869`
    - 摘录：
      > ... USCHunt \cite{DBLP:conf/uss/BodellMD23} focus on security issues with proxy-based upgradeable patterns, ...
  - 原文摘录 B（“shown in Figure ...” 引用处）
    - 文件：`paper_old.tex:536`
    - 摘录：
      > For instance, UniswapV2Factory \cite{uniswapv2factory} shown in Figure~\ref{lst:uniswap} uses \textit{create2(0,add(),mload(),salt)} to create new pair contracts, ...

## Referee 3

- 问题 1（引言中两个“局限/研究空白”的区分度不足、过于重合）：
  - 原文摘录（两条研究空白的原述）
    - 文件：`paper_old.tex:343`
    - 摘录：
      > However, existing studies have two main research gaps. \textbf{(1) Insufficient consideration of security issues within the FSC context.} ... \textbf{(2) Lack of a comprehensive investigation of factories and factory-deployed contracts.} ...

- 问题 2（需清晰阐明工厂合约/工厂部署合约相对 EOA 直部署合约的区别，并区分两类对象的安全风险）：
  - 原文摘录 A（EOA 与工厂部署差异的图文说明）
    - 文件：`paper_old.tex:402`
    - 摘录：
      > Figure~\ref{fig:deployment} illustrates the comparison between contracts deployed by \underline{E}xternally \underline{O}wned \underline{A}ccounts (EOA) ... and those deployed through a factory contract. In a direct EOA deployment, ... Conversely, factory deployment involves a two-stage process. ...
  - 原文摘录 B（RQ3 答案中对“安全风险归属”的区分）
    - 文件：`paper_old.tex:836`
    - 摘录：
      > Answer to RQ3: Both factory contracts and factory-deployed contracts carry security risks. Specifically, four kinds of discovered issues: \textit{Mutable Code}, \textit{Unexpected Ownership Transfer}, \textit{Unhandled Low-Level Contract Creation}, and \textit{Unverified Master Contract}. ...

- 问题 3（工厂检测主要依赖 Slither；未验证合约用交易模式，易漏报）：
  - 原文摘录（方法与局限）
    - 文件：`paper_old.tex:443`
    - 摘录：同 Referee 2 / 问题 2 的摘录。

- 问题 4（声称发现 1180 个安全问题，但缺少检测器设计细节与验证：精确率/召回率/对比现有工具）：
  - 原文摘录 A（四个检测器的总述）
    - 文件：`paper_old.tex:476`
    - 摘录：同 Referee 2 / 问题 6 的摘录 A。
  - 原文摘录 B（各类安全问题的“Detection Method”描述存在，但无系统性指标）
    - 文件：`paper_old.tex:736`（Unexpected Ownership Transfer 示例）、`paper_old.tex:791`（Unhandled Low-Level Contract Creation 示例）、`paper_old.tex:825`（Unverified Master Contract 示例）
    - 摘录：各小节以“\textit{Detection Method.}”方式描述规则/流程，但未报告整体精确率/召回率或与工具对比结果。

- 问题 5（研究仅覆盖以太坊主网，泛化性受限）：
  - 原文摘录（Threats to Validity）
    - 文件：`paper_old.tex:860`
    - 摘录：同 Referee 1 / 原文摘录 A。

- 问题 6（未量化经济影响，除 Tornado Cash 外缺少真实攻击分析）：
  - 原文摘录 A（案例研究引入及范围）
    - 文件：`paper_old.tex:646`，`paper_old.tex:652`
    - 摘录：同 Referee 2 / 问题 4 的两处摘录。

## Referee 4

- 问题 1（人工分析依赖较多，缺少审计人员背景、时间成本、冲突解决方法等细节）：
  - 原文摘录 A（方法部分对人工审计流程的描述）
    - 文件：`paper_old.tex:467`
    - 摘录：
      > ... we engage three experts with experience in smart contract security auditing to assist in the investigation of FSCs. We require each auditor to analyze the contracts independently and hold weekly group discussions to minimize subjective bias.
  - 原文摘录 B（Threats to Validity 中对指南、流程与耗时的补充）
    - 文件：`paper_old.tex:852`
    - 摘录：
      > ... To reduce subjectivity, we first implement a predefined set of guidelines for auditors during the factory contract audit. ... Then we employ a three-round iterative review process to find factory-based patterns and security risks. Three trained smart contract security auditors conduct independent reviews and votes in each round. ... Our four smart contract experts totally take around 900 working hours on manual evaluation and discussion.

- 问题 2（性能评估：1180 个问题是否均已验证？检测器是否漏报/误报？）：
  - 原文摘录 A（总量陈述）
    - 文件：`paper_old.tex:646`
    - 摘录：
      > We ultimately find 1,180 real-world smart contracts with four type of security issues using developed detectors. ...
  - 原文摘录 B（部分类别的人工核验说明，但未给总体指标）
    - 文件：`paper_old.tex:724`
    - 摘录：同 Referee 2 / 问题 6 的摘录 B。

- 问题 3（缺少严重性/影响评估与现实影响量化）：
  - 原文摘录（目前为案例与对策层面的描述）
    - 文件：`paper_old.tex:876`
    - 摘录：
      > ... We also implement four static security detectors and identify 1,180 newly discovered security issues. Through case studies, we highlight the security implications of FSCs and provide actionable countermeasures.

- 问题 4（技术贡献与新颖性：较多为规则化检测/编目，依赖现有工具）：
  - 原文摘录 A（依赖 Slither 进行分析）
    - 文件：`paper_old.tex:443`
    - 摘录：同 Referee 2 / 问题 2 的摘录。
  - 原文摘录 B（基于规则的检测器实现表述）
    - 文件：`paper_old.tex:476`，`paper_old.tex:791` 等
    - 摘录：四类检测器以规则/流程方式实现与说明（如低级创建需验证返回地址等），技术路线以规则化/静态分析为主。

- 问题 5（呈现与可读性：个别图/表/算法表述不清，如 Algorithm-1 仅覆盖一部分）：
  - 原文摘录 A（算法展示集中于“Mutable Code/Metamorphic”）
    - 文件：`paper_old.tex:660`
    - 摘录：
      > \begin{algorithm} \caption{Detect Metamorphic Contract} ... \end{algorithm}
  - 原文摘录 B（其余检测器以“Detection Method.”文字描述，无统一算法伪码）
    - 文件：`paper_old.tex:736`，`paper_old.tex:791`，`paper_old.tex:825`
    - 摘录：小节内通过“\textit{Detection Method.}”叙述规则与流程，但未统一提供算法伪代码。

备注：以上引文均来自旧稿 `paper_old.tex`，后续撰写 response letter 时，将逐条对照这些原始表述，结合新稿 `paper_new.tex` 的改动与补充，形成系统化、模板化的正式回复。

