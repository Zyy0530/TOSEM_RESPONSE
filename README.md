你是一个撰写Response的专家：
这是一篇投稿到TOSEM的论文，当前论文已经根据审稿人的意见，进行了充分的修改，具体来说：
/Users/mac/ResearchSpace/TOSEM_RESPONSE/paper_new.tex 这个是最新版本的论文
/Users/mac/ResearchSpace/TOSEM_RESPONSE/paper_old.tex 这个是旧版本的论文
/Users/mac/ResearchSpace/TOSEM_RESPONSE/review.md 这个是审稿人的具体的意见

现在，我们需要基于新的论文，撰写对审稿人的回复。具体来说：
/Users/mac/ResearchSpace/TOSEM_RESPONSE/ref这个文件夹给出了另外一篇“标准”的tex文件和对应渲染出来的pdf文件。
这两个文件是我们接下来回复审稿人的“重要参考”！！！你需要完全仿照这篇文章的tex格式进行撰写我们自己的response letter


具体来说，你需要：
阅读：/Users/mac/ResearchSpace/TOSEM_RESPONSE/ref/reference.tex文件，重点学习他的（1）整体结构（2）对每一个审稿人的具体的问题的回复方式（3）样式
你可以直接copy这个模版，来撰写我们自己的response.tex

阅读所有审稿人的每一条意见，理解审稿人的疑惑、质疑、要求改进的地方


然后，带着审稿人的问题，我们需要针对每一个审稿人的每一个问题，针对每一个回复，参照提供的模版的格式，进行回复。

怎么进行针对性的回复？
你需要带着审稿人的问题，带着问题去阅读旧版本的论文：/Users/mac/ResearchSpace/TOSEM_RESPONSE/paper_old.tex，从而了解到审稿人具体质疑旧版本论文的点在哪里
然后，带着旧版本论文的上下文以及具体审稿人的问题，你需要去阅读并定位/Users/mac/ResearchSpace/TOSEM_RESPONSE/paper_new.tex中新版本的论文。
最后，如果新版本的论文解决了审稿人的问题，你需要按照规定的格式要求，在response.tex文件中撰写对应的合适的内容进行回复。



现在，你需要做的事情为：
首先阅读审稿人的所有问题review.md, 针对每一个问题，阅读对应的原文paper_old.tex，然后撰写一个question.md
这个md文件应该按照每一位审稿人，一条一条罗列审稿人的每一个问题，针对每一个问题，都需要摘录对应的原文内容

很好，你需要基于已经梳理的这个question.md文件，对每一个问题进行带着问题，一一对应的，去新的论文中判断当前问题是否已经被修复
然后，你需要撰写fix.md文件



当你fix.md撰写完毕之后，你需要对正式的仿照“阅读：/Users/mac/ResearchSpace/TOSEM_RESPONSE/ref/reference.tex文件，重点学习他的（1）整体结构（2）对每一个审稿人的具体的问题的回复方式（3）样式
你可以直接copy这个模版，来撰写我们自己的response.tex” 这个模版，一一回复审稿人的问题 写入正式的回复

同样，你需要认真制定Step-by-Step的计划，并进行高度思考模式


现在，你需要帮我绘制一份表格，这个表格需要包含下面几列：
major concern ｜ reviewers ｜  previous versions ｜ new versions

这个表格是对全文的高度概括，回复所有审稿人的关键性问题。
要求如下，对于一些审稿人的共性concern，你需要再reviewers这一列中标注具体是哪几位，使用R1,R2,R3这种形式来制定多个reviewer
previous versions和new versions中需要说明，旧版本是怎么写的，而新版本又是怎么写的
例如，之前旧版本只有ETH上的受限的源代码的合约，而新版本收集了ETH和polygon上再bigquery上所有的字节码

我认为，你需要表达的点包括但不限于：
(1) 原始数据集范围：之前：仅Eth上已经被验证的合约，之后：eth和poly上在bigquery上的所有合约字节码
(2) 原始数据集截止时间：2023年Q3，之后：eth：2025年Q2，poly：2024年Q3
(3) Factory Detector：之前：源码级别的分析工具，无Evaluation，之后字节码级别的分析工具，包含Evaluation步骤
(4) Patterns Analysis: 只有部分有例子，之后：所有patterns均提供代码示例
(5) security issues analysis scope：之前：罗列四种，最新：分为Attack Vector和Security Issue，添加了新型攻击向量和安全事件


你现在需要做：（1）阅读新文件和旧文件，以及审稿人有疑问的地方（2）分清哪个审稿人在哪里有疑问，以及不同审稿人疑问的共性组合（3）帮我撰写这个表格，至少包含上述我提到的5个要点，你还要基于审稿人的major concern，撰写除了上述要点之外的修改的点，进行拓展。
要真实的符合当前response.tex的全部内容

你需要将这个表格放在“META-REVIEW FROM THE EDITORS”之前的合适位置，并用一段连贯的文字来说明这个表格是干嘛用的
你需要用专业、精简的英文文字来表达
将撰写的表格放在/Users/mac/ResearchSpace/TOSEM_RESPONSE/table文件夹，并在正文中引用这个表格

