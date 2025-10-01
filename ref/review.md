## Senior Associate Editor: 1

Comments to Author:

(There are no comments.)

## Associate Editor: 2

Comments to Author:

The reviewers commonly acknowledge the large-scale dataset, the identification of novel FSC patterns and issues, and the provision of open-source tools. However, significant concerns regarding generalizability, technical rigor, validation, and clarity need to be addressed.

To help the authors prepare the major revision, the following main changes are noted:

- Explicitly qualify conclusions about the broader Ethereum ecosystem due to the dataset being limited to verified contracts (<1%). Clearly state this limitation in the methodology and adjust claims regarding prevalence and security to reflect potential sample bias. (R2, R3)
- Provide clear technical details about the design and implementation of the security checkers. Present a comprehensive validation methodology, **including precision/recall metrics, false positive rates, and comparison with existing tools.** Address false positives specifically for the mutable code detector, explaining how permission checks are handled or quantifying their rate. Validate the reported 1180 security issues to confirm they are real and assess detector accuracy (missing/misreporting). Discuss the technical challenges and feasibility of adapting detectors for bytecode analysis of unverified contracts. (R2, R3, R4)
- Clearly articulate how FSCs introduce novel characteristics and security concerns compared to conventionally deployed contracts. Differentiate the security risks specific to factory contracts versus those affecting factory-deployed contracts. (R3)
- Provide concrete examples or case studies illustrating the real-world impact and potential exploits for the identified vulnerability categories beyond the Tornado Cash example. Assess the practical impact, severity, and potential economic implications of the discovered issues. (R2, R3, R4)
- Provide more details about the manual analysis process, including the background of the auditors, time commitment, and the method for resolving conflicts in identifying patterns and issues. Improve the clarity of Algorithm-1 and explain the scope of algorithmic descriptions. (R4) Clarify the distinction between the two initial limitations discussed in the introduction if they are presented as separate research gaps. (R3)
- Make Section 6.2 more comprehensive by including recent surveys and relevant literature. (R1)

Other changes should be considered as well:

- Discuss potential improvements to the clustering methodology (e.g., incorporating code-based features) and reflect on the accuracy achieved with the current name-based approach. (R2)
- Briefly discuss or acknowledge other related risks in upgradable smart contracts, such as storage collisions in proxy patterns, beyond the focus on create2-related issues. (R2)
- Add a brief discussion or acknowledgment regarding FSCs on other EVM-compatible chains or the generalizability of findings beyond the Ethereum mainnet. (R1, R3)
- Frame the technical contributions accurately, acknowledging that some aspects involve applying existing tools or cataloging known concepts while highlighting the novelty of the large-scale empirical analysis and FSC-specific tooling/findings. (R4)
- Carefully proofread the manuscript to correct typos and grammatical errors mentioned by reviewers. (R2, R4)

# REVIEWS

## Referee: 1

Recommendation: Needs Minor Revision

### Comments:

I suggest re-writing Section 6.2 (to make it more comprehensive and adding recent surveys) and adding the discussion about non-Ethereum FCSs.

### Additional Questions:

Review's recommendation for paper type: Full length technical paper

Does this paper present innovative ideas or material?: Yes

In what ways does this paper advance the field?: The exploration of FSCs has not yet been systematically studied. Yet, factory-related contracts empirically exhibit potential security threats that can affect many contracts (if a mass adopted pattern is insecure). Thus, this work is timely, important, and potentially impactful.

Is the information in the paper sound, factual, and accurate?: Yes

If not, please explain why.:

Rate the paper on its contribution to the body of knowledge in software engineering (none=1, very important=5): 5

What are the major contributions of the paper?: 1) Empirical study on Ethereum Mainnet FSCs.

2) FSC detector with security checkers

3) Comprehensive security analysis of FSC contracts

4) Openly accessible artifacts

Rate how well the ideas are presented (very difficult to understand=1, very easy to understand=5): 5

Rate the overall quality of the writing (very poor=1, excellent=5): 4

Does this paper cite and use appropriate references?: No

If not, what important references are missing?: Section 6.2 is too shallow. I suggest to cite and follow some recent surveys, like this one:

https://dl.acm.org/doi/abs/10.1145/3593293

Should anything be deleted from or condensed in the paper?: No

If so, please explain.:

Is the treatment of the subject complete?: No

If not, What important details / ideas/ analyses are missing?: A brief discussion of non-Ethereum smart contracts through the perspective of FSC would be good to have in the paper.

If this is a Journal-First Paper, does it differ by more than 70% from any other previous publication?: Yes

Comments:

Please help ACM create a more efficient time-to-publication process: Using your best judgment, what amount of copy editing do you think this paper needs?: Light

Most ACM journal papers are researcher-oriented. Is this paper of potential interest to developers and engineers?: Yes

## Referee: 2

Recommendation: Needs Major Revision

Comments:

Summary of this paper:

This paper presents an empirical study investigating Factory-related Smart Contracts (FSCs) on the Ethereum blockchain. Through comprehensive analysis of 482,542 open-source smart contracts, the authors identify 8,083 factory contracts and 243,938 factory-deployed contracts. The study systematically examines three key aspects such as prevalence, implementation patterns, and security issues. The authors develop a specialized factory contract detector and four static security analyzers, uncovering 1,180 previously undocumented security issues.

Strength:

- Large-scale analysis (482K contracts) with quantitative and qualitative insights.
- Open-sources tools and datasets for reproducibility.

Weakness

- Limited dataset scope
- Potential overclaiming of findings given the small percentage of total contracts analyzed
- Insufficient real-world vulnerability case studies beyond the Tornado Cash example
- Manual analysis bottleneck

Detail comments:

This paper presents an empirical study on FSCs in Ethereum, analyzing 482,542 open-source smart contracts to identify 8,083 factory contracts and 243,938 factory-deployed contracts. The study addresses three key research questions: prevalence, implementation patterns, and security issues, which provides valuable insights into FSC applications and risks. However, the study’s dataset is limited to verified (open-source) contracts, which represent less than 1% of all Ethereum contracts [Etherscan]. While the findings are insightful, **the generalizability of claims about the broader Ethereum ecosystem is constrained**. Additionally, the security contributions, though useful, would benefit from deeper validation to strengthen their impact. Below are detailed concerns and suggestions for improvement.

1.      My first concern is the limited dataset scope. **This paper analyses only <1% of total smart contracts**, yet conclusions are framed as representative of the entire Ethereum ecosystem. Since unverified contracts may exhibit different patterns, the claims about prevalence (RQ1) and security (RQ3) should be explicitly qualified to eliminate overclaims. Please clearly state this limitation in the methodology and adjust conclusions to reflect the sample bias.

2.      Following the dataset problem, I am also concerned about the generalizability of the four security detectors. It is necessary to support bytecode analysis for measuring all smart contracts. The four detectors rely on heuristic IR patterns from Solidity source code, which limits applicability to unverified (bytecode-only) contracts. Please explain the technical challenges in adapting the detectors for bytecode analysis. Please discuss the feasibility of adapting detectors for bytecode (e.g., via symbolic execution or decompilation). If impractical, acknowledge this as a limitation.

3.      Clustering relies solely on contract names, which may introduce noise (e.g., misleading names like "ProxyFactory" in non-proxy contexts). Do you find any incorrect classification? Incorporating code-based features (e.g., function signatures, opcode sequences) may improve accuracy.

4.      I also found there is few concrete examples to show the damages of the security issues in FSCs. While the Tornado Cash case study illustrates mutable code risk**s, the other three vulnerability categories lack concrete examples. Please include at least one exploit per vulnerability, e.g., a locked-fund incident due to unhandled create2 failures**. Adding attack events can emphasize the security contribution of this paper.

5.      In addition, this paper focuses on create2-related bugs but seems to overlook the risks in upgradable smart contracts such as storage collisions in proxy patterns.

6.      You may include false positives in detecting mutable code bug. The detector flags bugs if there is any control flow from delegatecall to create2, but safe permission checks (e.g., onlyOwner) may mitigate risks. Please explain how your algorithm excludes permission-guarded paths or report precision/recall metrics to quantify false positives.

Typo issues:

- Page 12, Line 48, the reference to the figure should be Figure-7
- Page 23, Line 34, USCHunt focus => USCHunt focuses

Reference:

[Etherscan] Ethereum-community, “Contracts with verified source codes,” 2020. [Online]. Available:

https://etherscan.io/contractsVerified

Additional Questions:

Review's recommendation for paper type: Full length technical paper

Does this paper present innovative ideas or material?: Yes

In what ways does this paper advance the field?:

Is the information in the paper sound, factual, and accurate?: Yes

If not, please explain why.:

Rate the paper on its contribution to the body of knowledge in software engineering (none=1, very important=5): 3

What are the major contributions of the paper?:

Rate how well the ideas are presented (very difficult to understand=1, very easy to understand=5): 3

Rate the overall quality of the writing (very poor=1, excellent=5): 3

Does this paper cite and use appropriate references?: Yes

If not, what important references are missing?:

Should anything be deleted from or condensed in the paper?: No

If so, please explain.:

Is the treatment of the subject complete?: Yes

If not, What important details / ideas/ analyses are missing?:

If this is a Journal-First Paper, does it differ by more than 70% from any other previous publication?: Yes

Comments:

Please help ACM create a more efficient time-to-publication process: Using your best judgment, what amount of copy editing do you think this paper needs?: Light

Most ACM journal papers are researcher-oriented. Is this paper of potential interest to developers and engineers?: Yes

## Referee: 3

Recommendation: Reject

Comments:

This paper presents a comprehensive empirical study of Factory-related Smart Contracts (FSCs) on Ethereum. Analyzing 482,542 contracts, the authors find that factory contracts have become the dominant deployment method (>90% since 2020). They identify six implementation patterns and discover 1,180 contracts with security issues across four categories. The research contributes a factory contract detector, pattern identification methodology, and security checkers for FSC-specific vulnerabilities, providing valuable insights for smart contract developers and the Ethereum community.

However, I have several concerns regarding the clarity, technical rigor, and completeness of the work.

1. While the paper presents a meaningful direction in security research for Factory-related Smart Contracts (FSCs), the two limitations mentioned in the current work do not appear to have substantial differences. The authors distinguish between "insufficient consideration of security issues within the FSC context" and "lack of comprehensive investigation of factories and factory-deployed contracts," but these limitations seem to overlap significantly rather than representing distinct research gaps.

2.The paper identifies two components of Factory-related Smart Contracts (FSCs): factory contracts and factory-deployed contracts. However, a significant shortcoming is the lack of **clear articulation regarding how these two types differ from conventional EOA-deployed contracts.** The paper fails to explicitly outline the distinctive characteristics of FSCs that might introduce novel security concerns, which undermines a crucial aspect of the paper's motivation. Furthermore, when discussing security issues, the authors do not adequately differentiate between risks specific to factory contracts versus those affecting factory-deployed contracts. It remains unclear whether security vulnerabilities manifest similarly or differently across these two contract types.

3.From a technical perspective, the paper exhibits notable weaknesses. The factory detector primarily relies on Slither's analysis results without demonstrating significant innovation in detection methodology. This approach represents a relatively straightforward application of existing tools rather than a novel technical contribution. Moreover, the method employed for unverified contracts—using transaction patterns for detection—is prone to substantial false negatives. This approach fails to identify factory contracts that have not yet deployed other contracts or have limited transaction history.

4.The paper claims to have detected "1,180 newly discovered security issues" using security checkers, but it fails to provide clear technical details about the design and implementation of these checkers. Furthermore, there is insufficient discussion of the validation methodology for these security checkers. The absence of precision and recall metrics, false positive rates, or comparison with existing security tools makes it difficult to assess the reliability of the reported security issues.

5.The study focuses exclusively on the Ethereum mainnet, which the authors acknowledge as a limitation. While Ethereum is the most prominent smart contract platform, the findings may not generalize to other EVM-compatible blockchains like Polygon, Arbitrum, or Optimism. This limits the broader applicability of the research findings.

6. **While the paper identifies security issues in FSCs, it does not quantify their economic impact. Given that smart contracts often manage significant financial assets, understanding the potential financial losses associated with these vulnerabilities would provide valuable context for prioritizing security efforts. Also, apart from the Tornado Cash DAO attack case study, the paper provides limited analysis of real-world exploits targeting FSC vulnerabilities.**

Additional Questions:

Review's recommendation for paper type: Full length technical paper

Does this paper present innovative ideas or material?: Yes

In what ways does this paper advance the field?:

Is the information in the paper sound, factual, and accurate?: Yes

If not, please explain why.:

Rate the paper on its contribution to the body of knowledge in software engineering (none=1, very important=5): 2

What are the major contributions of the paper?:

Rate how well the ideas are presented (very difficult to understand=1, very easy to understand=5): 3

Rate the overall quality of the writing (very poor=1, excellent=5): 3

Does this paper cite and use appropriate references?: Yes

If not, what important references are missing?:

Should anything be deleted from or condensed in the paper?: No

If so, please explain.:

Is the treatment of the subject complete?: Yes

If not, What important details / ideas/ analyses are missing?:

If this is a Journal-First Paper, does it differ by more than 70% from any other previous publication?:

Comments:

Please help ACM create a more efficient time-to-publication process: Using your best judgment, what amount of copy editing do you think this paper needs?: None

Most ACM journal papers are researcher-oriented. Is this paper of potential interest to developers and engineers?: Yes

## Referee: 4

Recommendation: Needs Major Revision

Comments:

Paper Summary:

This paper systematically studies factory-related smart contracts (FSCs) on Ethereum, focusing on their prevalence, design patterns, and security issues. To this end, the authors develop a static analysis framework that detects factory contracts and the contracts they deploy. The authors analyze a dataset of 482,542 Ethereum contracts (from the mainnet) to answer research questions about how common FSCs are, what unique functionality and patterns they exhibit, and what security risks they introduce. Overall, the paper is well written, providing valuable insights into FSCs, There are still several aspects the authors could consider to improve their manuscript. I provide my detailed comments as follows:

Comments for authors:

- -----------------------------
- -

Strengths:

1. Comprehensive empirical dataset: The study covers 482,542 Ethereum contracts and identifies 8,083 factory contracts and 243,938 contracts they deploy, which is a large-scale dataset regarding the factory-related smart contracts.

2. Novel code patterns and issues with FSCs: The paper systematically uncovers six distinct FSC design patterns and four classes of security issues. These categories are clearly motivated and illustrated. Some security issues (like the metamorphic contract upgrade problem) are presented as newly discovered, which advances understanding of FSC-specific risks.

3. SA tools: The authors built four security checkers for FSC-specific vulnerabilities. This is valuable for the community, as existing tools do not target these patterns. They also discuss actionable recommendations (such as using audited libraries) and make their artifacts public, which aids reproducibility and future research.

Weaknesses:

1. Manual Analysis: Much of the pattern identification and issue classification relies on manual auditing by experts. Although the authors use guidelines and multiple reviewers to reduce bias, however, this process is inherently subjective and many details are missing. what is the background of the experts? are the students or the smart contract developers? The authors mentioned "each auditor analyzes the contracts independently and hold weekly group discussions to minimize subjective bias", what are the time cost for each auditor? The definitions of “patterns” or “issues” could vary depending on different auditors, how did they solve the conflicts?

2. Performance evaluation. The methodology is generally sound, combining static analysis, blockchain data mining, and manual auditing. The use of 482k contracts and specialized detectors are reasonable. One concern is that there is no standard (ground-truth) dataset to estimate the effectiveness of the tools, the authors report that they find "1180 real-world smart contracts with four types of security issues", did they validate all of these 1180 real-world security issues? are the detectors missing or misreporting any security issues?

3. Lack of severity evaluation: The paper reports the quantity of security issues found but does not deeply assess their practical impact or severity. For example, it is unclear how often the identified vulnerabilities would actually be exploitable or economically significant. Without validation or a risk assessment for each issue, it is hard to judge their real-world importance. I would suggest the authors to validate their reported security issues with real-world examples.

4. Technical contributions & novelty. While the empirical scale and focused analysis are novel, many of the identified patterns (e.g. minimal proxies, create2 usage) and general security concerns (e.g. ownership mismanagement) **are known in the smart-contract community.** The contribution is more in cataloging them than in introducing fundamentally new concepts. The technical contributions are limited, e.g., implementing rule-based detectors for designed code patterns, these tools are useful but the technical contributions are still limited.

5. Presentation. The overall presentation of this paper is good, which is well-written and easy to follow. There are some typos the authors need to careful proof-read the paper and correct them, such as RQ2, "UniswapV2Factory [15] shown in Figure ?? uses".  The algorithm part of algorithm-1 is hard to follow and unclear, also why only provide algorithm description only for part-1 but not others?

Additional Questions:

Review's recommendation for paper type: Full length technical paper

Does this paper present innovative ideas or material?: Yes

In what ways does this paper advance the field?:

Is the information in the paper sound, factual, and accurate?: Yes

If not, please explain why.:

Rate the paper on its contribution to the body of knowledge in software engineering (none=1, very important=5): 3

What are the major contributions of the paper?:

Rate how well the ideas are presented (very difficult to understand=1, very easy to understand=5): 4

Rate the overall quality of the writing (very poor=1, excellent=5): 4

Does this paper cite and use appropriate references?: Yes

If not, what important references are missing?:

Should anything be deleted from or condensed in the paper?: No

If so, please explain.:

Is the treatment of the subject complete?: Yes

If not, What important details / ideas/ analyses are missing?:

If this is a Journal-First Paper, does it differ by more than 70% from any other previous publication?: Yes

Comments:

Please help ACM create a more efficient time-to-publication process: Using your best judgment, what amount of copy editing do you think this paper needs?: Moderate

Most ACM journal papers are researcher-oriented. Is this paper of potential interest to developers and engineers?: Yes
