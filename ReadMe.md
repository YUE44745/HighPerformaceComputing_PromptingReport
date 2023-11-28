**这个是高性能程序开发这门课程的一项课程作业，其主题是一项关于使用AI来进行学习某项技能的提示词的演技，我组所选子项目则如下所诉**
**我组所使用大模型为通义千问**
## 子题目（可以使用ChatGPT, 文心一言，Moonshot，例如尝试“下面用苏格拉底的方式教授编程”）
- 大模型UVM教学
## 参考提示工程指南 | Prompt Engineering Guide (promptingguide.ai)
- 两人一组，提交测试报告（5号字，含截图不超过15页）
- 课程背景
- Prompt设计思路
- Prompt实践摘要与亮点分析
- 组内成员介绍与分工
- 对课程的建议与意见

## 问题设计思路
1. 什么是UVM，它是用来干什么的
2. 为什么要学习UVM
3. 学习UVM需要哪些基础前置知识
4. 学习UVM的基本方法 
5. 学习UVM需要学习哪些内容
6. 针对UVM的各个内容进行提问
7. 在针对各个内容进行提问时，要求给出详细内容与相关示例
8. 总结学习UVM的各个方面

### 关于 prompt engineering guide 的一些学习笔记（Prompt Engineering）
#### basic
1. 一门新的学科，关注提示词开发和优化。不仅仅关于设计和研发提示词，还有LLM交互和研发的各种技术。可以提高安全性、增强LLM能力。
2. > 除非特别说明，本指南默认所有示例都是基于 OpenAI 的大语言模型 text-davinci-003 进行测试，并且使用该模型的默认配置，如 temperature=0.7 和 top-p=1 等。
3. model settings:
   - _temperature_: 关于输出准确性。值越小，越准确。值越大，越有创造力。
   - _Top\_p_: 一起称为 _nucleus sampling_ 技术，同上。一般更改一个即可。
4. prompt contain _instruction_ and _question_, and _context_/_inputs_/_examples_
5. > 提示工程（Prompt Engineering）就是探讨如何设计出最佳提示词，用于指导语言模型帮助我们高效完成某项任务。
6. _zero-shot prompting_: no examples or demonstrations
7. _few-shot prompting_: provide examples
8. elments of a prompt:
   - Instruction
   - Context
   - Input Data 
   - Output Indicator
9. tips for desinging prompts
   - instructon and context separate
   - specificity
   - avoid impreciseness
   - say to do is necessary when say not to do
#### more examples and key concepts
** the best way to learn concepts is by going through examples**, so I will use the 通义千问 to go through these examples.
1.  text summarization
   ```
   Explain antibiotics

   A:
   ```
   ```Antibiotics are medications that are used to treat bacterial infections. They work by killing or inhibiting the growth of bacteria, which can help the body fight off the infection and heal.

   There are many different types of antibiotics, each with their own specific mechanisms of action and effectiveness against different types of bacteria. Some common examples include penicillins (such as amoxicillin), cephalosporins (such as cephalexin), macrolides (such as azithromycin), and fluoroquinolones (such as ciprofloxacin).

   It is important to use antibiotics only when necessary and as directed by a healthcare provider, because overuse or misuse can lead to antibiotic resistance, which occurs when bacteria develop the ability to survive exposure to antibiotics that would normally kill them or inhibit their growth. This can make it more difficult to treat infections in the future, and can even lead to the development of "superbugs" that are resistant to multiple types of antibiotics.

   In addition, antibiotics are not effective against viral infections, such as colds or the flu, so they should not be used to treat these conditions. It is also important to finish the full course of antibiotics prescribed by a healthcare provider, even if symptoms improve before the end of the treatment, to ensure that all of the bacteria causing the infection have been eliminated and reduce the risk of antibiotic resistance.
   ```
   ```
   ~
   Explain the above in one sentence:
   ```
   ```
   Antibiotics are medications used to treat bacterial infections by killing or inhibiting bacterial growth, but overuse/misuse can lead to antibiotic resistance, making future infections harder to treat; they are ineffective against viruses and finishing the full course is crucial to eliminate bacteria and reduce antibiotic resistance risk.
   ```

2.  informaion extraction
3.  quesetion answering
4.  text classification(give more information or examples)
5.  conversation(_role prompting_)
6.  code generation
7.  reasoning(break the problem into steps)
#### more advanced prompting engineering techniques
1. _Zero-shot Prompting_ is okey when the task is not complex, while it is necessary to use the _few-shot Prompting_.
2. _Few-shot Prompting_ is providing LLM with examples.
   > Following the findings from Min et al. (2022), here are a few more tips about demonstrations/exemplars when doing few-shot:
   > "the label space and the distribution of the input text specified by the demonstrations are both important (regardless of whether the labels are correct for individual inputs)"
   > the format you use also plays a key role in performance, even if you just use random labels, this is much better than no labels at all.
   > additional results show that selecting random labels from a true distribution of labels (instead of a uniform distribution) also helps.
3. _chain-of-thought(CoT) prompting_
4. **"let's think step by step"** is amazing.
5. Auto-CoT(这个在中文版里面没有这部分的内容)：问题聚类；简单抽样演示得到CoT
6. self-consisitency: sample multiple,diverse reasoning paths through few-shot CoT.
7. generate knowledge prompting: in commonsense reasoning
8. Tree of Thoughts(ToT):感觉很神奇，没怎么看懂。但是至少知道了这个可以用。
   ```
   Imagine three different experts are answering this question.
   All experts will write down 1 step of their thinking,
   then share it with the group.
   Then all experts will go on to the next step, etc.
   If any expert realises they're wrong at any point then they leave.
   The question is...
   ```
9. Retrieval Augmented Generation (RAG)（检索增强生成）：感觉new biying应该用的就是这种方法。
10. Automatic Reasoning and Tool-use (ART)（自动推理并使用工具）
**后面的几个因为我实在是没有看懂，所以没有写任何想关的**
#### 一些应用（由于课程任务也是和代码相关，所以重点看一些这些方面的）
1. PAL(program-aided language models): CoT是使用自然语言来惊醒得到一步步的解决办法，但是使用PAL是通过程序来解决中间步骤的问题。