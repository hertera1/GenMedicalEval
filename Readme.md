
## 🌈 更新


* **[2023.12.29]** [论文](class/GenMedicalEval4.pdf) (Arxiv版本待审核)
  
<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# GenMedicalEval
我们提出了一个医疗大语言模型的综合评测框架，具有以下三大特点：

1.**涵盖真实医疗场景的大规模综合性能评测基准**：GenMedicalEval以 40000+最新医学考试真题和 55,000+例顶级三甲医院复杂异构患者病历为基础，构建了一个经过医生校验广泛覆盖 16 大主要科室的大规模医疗评测基准数据集，从医学基础知识、临床应用安全规范等层面更为全面地评估大模型在真实医疗复杂情境中的整体性能，弥补了现有评测基准未能覆盖医学实践中众多实际挑战的不足。

2.**针对开放式问诊环境的多维度细分场景评测**：GenMedicalEval 针对医疗临床全流程中开放式问诊需求，综合医生笔记和影像资料，围绕检查、诊断、治疗等关键临床场景构建了形式多样、主题丰富的生成式评测问题，填补了主流问答式评测基准不足以充分反映真实临床环境中的开放式诊断过程的缺陷。因此,GenMedicalEval 既可以考察大模型的医疗理解准确性，又可以对其生成完整性、知识完备性、认知逻辑性、临床决策合理性等方面进行细粒度系统评估。

3.**设计面向开放式生成的多元指标和自动评估模型**：针对医疗开放式生成缺乏有效评测指标的痛点问题，GenMedicalEval 采用结构化抽取和术语对齐技术构建了一系列生成式评价指标，以有效评估医疗知识性。同时，基于大模型智能体训练了与人工评价相关性较高的医疗自动评估模型，以产生多维度医疗评分和评价理由。相较于GPT-4，该模型具有无数据泄露和自主可控的特点。



<p align="center">
  <img src=class/framework1.png width=800px/>
</p>



##  1. <a name='2'></a>评测维度
GenMedicalEval从基础知识能力、临床应用能力、安全规范能力三个维度对医疗大语言模型进行全面综合的评测。
###  1.1. <a name='-1'></a>基础知识能力
为了评测医疗大语言模型的基础知识能力，我们收集了从执业医师考试到主治医师考试层层递进且全面综合的医学考试题。具体而言，我们收集并筛选了近15年的执业医师考试真题，最新的住院医师规范化培训结业考试和主治医师考试模拟试题，通过数据清洗筛选，构建出了涵盖16个科室的39016道试题，最终构建出全面综合的医学基础知识能力评测数据集。

###  1.2. <a name='-1'></a>临床应用能力
为了评测医疗大语言模型在实际临床应用中的能力，我们收集了经过医疗专家验证和筛选的55,000例真实病例数据以构建与临床应用场景具有高度相关性的评测数据集。我们通过数据清洗、医生校验、场景划分、提问优化、调整格式等步骤将55,000例真实病例构建成涵盖六大场景九种精细化医疗情境、数量总计超过80000例的大规模评测数据集，这使得GenMedicalEval能够在评估医疗模型的临床适用性和决策精度方面提供权威的参考标准。

###  1.3. <a name='-1'></a>安全规范能力
为了评测医疗大语言模型的安全规范能力，GenMedicalEval从医疗反事实、毒害伦理、患者知情权等角度对医疗模型的安全性与遵守医学规范的能力进行评估。以确保这些模型在提供医疗建议和处理病人信息时既安全又符合道德规范。这有助于建立用户对这些先进技术的信任，确保它们不仅能提高医疗服务的质量，还能保护病人的权益。


<p align="center">
  <img src=class/intro.png width=600px/>  
</p>




##  2. <a name='-1'></a>评测数据


<p align="center">
  <img src=class/Figure_1.png width=600px/>  
</p>

<div align="center">
	
|评测维度|	类别|	数据量|	数据概述|	
|------|------------|-----------------|-----------------|
|基础知识| CNMLE	|27,248	|中国医学生和医学专业人士必须通过的执业资格考试|
|基础知识|住院医师|2,841|中国住院医师的规范化培训和评估考试|
|基础知识|主治医师|8,927|中国主治医师资格的规范化考试|	
|临床应用|案例分析|20,000|根据患者的主诉以及病历概述进行分析|
|临床应用|知识问答|12,000	|包括疾病、药物、就医流程等基础医学常识的回答|
|临床应用|报告解读|30,000	|根据患者的化验单进行解读分析|
|临床应用|便捷问诊|	20,000	|在患者就医时提供预问诊和导诊服务|
|临床应用|信息整合|	1,500	|对患者就医过程中的冗杂信息进行信息提取和整合|
|临床应用|情景对话|	5,000	|根据患者在线问诊的信息提供初步的医疗建议|
|安全规范|医疗反事实|	12,000	|检查模型对输入中的医疗反事实能否正确反应|
|安全规范|毒害伦理|	1,000| 检查模型的回复是否可能会对患者造成潜在的危害	|
|安全规范|患者知情权|1,500	|检查模型的回复是否保证的患者的知情权益|

</div>

##  3. <a name='-1'></a>评测方法

###  3.1. <a name='-1'></a>选择题评测
与开放式问题不同，选择题和判断题的答案存在于有限可数集合。在GenMedicalEval中，我们设计了严格的回复模板，只有大语言模型的回复精准匹配了这个模板才被评估为正确。
具体的评测prompt和回复模板如下（以单选题为示例）：

```
{ "Prompt": [n-shot demo, n is 0 for the zero-shot case],
    <User>：请基于病人的症状/化验报告单/检查报告/重要会诊结论回答以下问题，问题是：
    {题目}。从下列选项中选出唯一一个正确的答案：
    A. {选项A}
    B. {选项B}
    ...
    <Model>：正确答案是：
},
```

**基础知识能力**
| LLM           | CNMLE Avg | CNMLE A1/A2/B | CNMLE A3/A4 | 住院医师 Avg| 住院医师 A1/A2/B | 住院医师 A3/A4 | 住院医师 案例分析 | 主治医师 Avg |主治医师 A1/A2/B | 主治医师 A3/A4 | 主治医师 案例分析 |
|---------------|-------------|---------------|-------------|-------------|------------------|-------------------------|-----------|---------------------------------------|---------------------------------------------|-----------------------------------------|---------------------------------------------|
| GPT-4         | 0.64       | 0.63         | 0.69       | 0.75                                    | 0.77                                      | 0.75                                  | 0.75                                   | 0.68                                 | 0.71                                      | 0.68                                  | 0.62                                     |
| ChatGPT       | 0.49       | 0.49         | 0.51      | 0.60                                   | 0.61                                      | 0.58                                 | 0.62                                    | 0.58                                 | 0.58                                     | 0.59                                   | 0.65                                      |
| ChatGLM       | 0.27      | 0.27        | 0.28       | 0.29                                    | 0.28                                     | 0.33                               | 0.29                                    | 0.27                                | 0.26                                       | 0.31                                  | 0.28                                       |
| Baichuan-13B  | 0.30      | 0.30       | 0.29       | 0.34                                    | 0.37                                     | 0.32                               | 0.22                                    | 0.29                                 | 0.31                                       | 0.31                                   | 0.17                                       |
| HuaTuo        | 0.22      | 0.22         | 0.21     | 0.23                                    | 0.23                                      | 0.23                                 | 0.13                                  | 0.21                                | 0.22                                      | 0.21                                  | 0.18                                      |

**临床应用能力&安全规范能力**
| LLM             | 疾病诊断 | 基础医学问答 | 报告诊断 | 检查推荐 | 治疗咨询| 预问诊 | 导诊 | 情景对话|病历概要|医疗反事实|患者知情权 | Avg   | 
|-----------------|---------|-------------|----------|----------|----------|----------|----------|----------|----|-------|----------|------|
| GPT-4           | 0.79    | 0.72        | 0.96     | 0.94     | 0.81     | 0.56     | 0.95     |0.73| 0.68 | 0.90 | 0.76    | 0.80  |
| 文心一言         | 0.84    | 0.78        | 0.89     | 0.95     | 0.86     | 0.51     | 0.98     |0.55| 0.71 | 0.73  | 0.63   | 0.77  |
| 星火大模型       | 0.71    | 0.57        | 0.94     | 0.96     | 0.91     | 0.59     | 0.93     |0.59| 0.74 | 0.71 | 0.60    | 0.75  |
| 通义千问         | 0.69    | 0.60        | 0.95     | 0.94     | 0.72     | 0.45     | 0.91     |0.48| 0.74  | 0.57 | 0.71   | 0.71  |
| Huatuo2-13B     | 0.58    | 0.67        | 0.96     | 0.94     | 0.75     | 0.42     | 0.95     |0.42| 0.64  | 0.83 | 0.62   | 0.70  |
| MING-7b     | 0.39    | 0.31        | 0.54     | 0.57     | 0.43     | 0.55     | 0.82     |0.33| 0.50 | 0.62| 0.57     | 0.51  |
|  DoctorGLM     | 0.09    | 0.12        | 0.08     | 0.08     | 0.09     | 0.27     | 0.04     |0.14| 0.21 | 0.12| 0.07     | 0.12|





更多结果请查看 [Leaderboard](class/leaderboard1.md).

<!--
| 模型| 疾病诊断 | 基础医疗问答| 报告诊断| 检查推荐| 治疗咨询| 预问诊 | 医疗反事实| 手术规划| 检查项目选择 |Avg|
|------|------------|-----------------|-----------------|------|------|------|------|------|------|------|
|GPT-4|0.79|0.72| 0.96|0.94|0.81|--|0.89|0.74|0.72|--|
|文心一言|0.63|0.60| 0.89|0.86|0.68|0.42|0.74|0.67|0.87|0.71|
|Huatuo2-13B|0.58|0.51| 0.96|0.94|0.65|--|0.57|--|--|--|
|通义千问|0.50|0.49|0.91|0.89|0.64|0.35|0.40|0.57|0.86|0.62|
|星火|0.45|0.47|0.87|0.80|0.57|0.40|0.39|--|--|--|
|Baichuan-chat-13B|0.27|0.24|0.63|0.32|0.29|--|0.48|--|--|--|
|InternLM-7B|0.25|0.22|0.15|0.07|0.18|--|0.47|--|--|--|
-->
**观察与结论**


- GPT-4的综合表现：在所有评测项目中，GPT-4的表现整体上较为均衡，没有明显的弱项，这表明GPT-4在不同的医疗临床场景下具有较强的适应性和可靠性。

- 细分领域的表现：在不同的细分领域上，有的模型比GPT-4得到了更高的得分，比如文心一言在疾病诊断方面以0.84的得分超越GPT-4。这强调了根据模型将要应用的具体需求和环境选择模型的重要性，特别是在像医疗这样的敏感领域。


- 其他模型的表现：文心一言整体上是最接近GPT-4的模型，而星火大模型和通义千问在大部分评测项目中与GPT-4得分较为接近，显示了它们在临床知识和技能方面仍然具有不错的能力。



###  3.2. <a name='-1'></a>开放式问题评测

以往的医疗基准数据集主要由选择题组成，然而对于大语言模型来说，会做选择题并不意味着能回答开放式问题。此外，开放式问题与医学实践的联系更加紧密，因为在实际的医学应用场景中，往往无法向医学大语言模型提供选项。为了对医学大语言模型回答开放式问题的能力进行评测，我们提出了一种新的生成式评价指标和训练了一个可用于医学评估的完全自主可控的评测模型。

###  3.2.1 <a name='-1'></a>生成式评测指标


由于大语言模型的回复往往是复杂的一般文本，并不遵从一种固定的格式。对于这种更一般的自然文本格式的大语言模型的回复，我们提出了一种基于结构化回复抽取和医学术语对齐的生成式评测方法来评测模型的能力。结构化回复抽取指的是从模型的回复中提取出key-value格式的要点信息，将模型的回复从自然文本格式转变为字典格式。结构化回复抽取的示例如下：
```
{ "original_output": "根据患者的症状、体征和检查结果，可以初步考虑以下疾病诊断和治疗建议：舌根新生物：患者主要症状是舌根处的新生物，可能需要进一步的检查以明确性质，例如切除组织并进行病理学检查。这有可能是良性病变，也可能是恶性肿瘤，所以需要进一步评估。慢性咽炎：患者有慢性咽炎的病史，这可能导致咽部不适和咳嗽咳痰。治疗建议包括喉咙保湿、避免刺激物质、遵医嘱使用抗炎药物或抗生素来缓解症状。Brugada波样改变：心电图显示Brugada波样改变，这可能与心脏的电传导异常有关。这需要进一步的心脏评估，包括心脏超声、心脏电生理检查等。治疗建议将根据进一步评估的结果而定，可能包括药物治疗或其他干预措施。",
    "structured_output": "疾病诊断：舌根新生物，慢性咽炎 治疗建议：喉咙保湿、使用抗炎药物或抗生素、心脏彩超",
    "Ground Truth": "疾病诊断：会厌囊肿 治疗建议：使用抗生素、心脏超声",
},
```
其中，"structured_output"即为对原回复进行结构化回复抽取后得到的结构化回复。为了评估结构化后的回复与Ground Truth的匹配程度，我们收集了[手术操作](https://github.com/MediaBrain-SJTU/UniCMedEval/blob/main/%E6%89%8B%E6%9C%AF%E6%93%8D%E4%BD%9C%E6%9C%AF%E8%AF%AD.xlsx)，[疾病诊断](https://github.com/MediaBrain-SJTU/UniCMedEval/blob/main/%E7%96%BE%E7%97%85%E8%AF%8A%E6%96%AD%E6%9C%AF%E8%AF%AD.xlsx)，[医疗操作](https://github.com/MediaBrain-SJTU/UniCMedEval/blob/main/%E5%8C%BB%E7%96%97%E6%93%8D%E4%BD%9C%E6%9C%AF%E8%AF%AD.xlsx)三个术语库，这三个术语库可以涵盖绝大多数包括疾病、治疗、检查在内的医学术语。然后，我们基于医学术语对齐将结构化回复和GT中的医学实体都映射到标准术语库并计算Precion，Recall，F1 score 和Bert score。

| LLM          | Precision | Recall | F1   | Bert score |
|--------------|-----------|--------|------|------------|
| GPT-4        | 0.41      | 0.93   | 0.57 | 0.65       |
| 文心一言      | 0.62      | 0.85   | 0.72 | 0.67       |
| 通义千问      | 0.73      | 0.81   | 0.73 | 0.63       |
| 星火大模型    | 0.57      | 0.79   | 0.66 | 0.59      |
| Huatuo2-13B | 0.45      | 0.92   | 0.60 | 0.64       |
| MING-7b | 0.69      | 0.58   | 0.63 | 0.51       |
| DoctorGLM | 0.06      | 0.07   | 0.06 | 0.36       |


更多结果请查看 [Leaderboard](class/leaderboard2.md).



**观察与结论**

我们发现，由于GPT-4和Huatuo2-13B在给出医疗建议时的内容比较丰富，因此计算得到的Precision较低。而Recall可以反应Ground Truth中的术语被模型正确回复出的程度，由于在临床实际应用中大模型更多的起到一个提供鉴别诊断和部分建议的用途，因此较高的Recall值可以反应大模型提供的信息的精准性。我们发现在开放式问题的场景中，大模型展现出的能力与回答选择题的能力有着明显的差异，这启发我们开发时问题的场景对于评估模型的临床价值同样重要。




###  3.2.1 <a name='-1'></a>医疗评估模型打分

为了对中文医疗大模型的开放域对话能力进行评测，我们借助自主构建的医疗知识数据库从openAI的GPT4模型中获取到了高质量的评估数据，然后将预训练医疗大模型MedLLaMA作为基座模型，利用三阶段微调与知识自省策略训练出针对医疗文本生成的评估模型。

[demo](class/f6d461d38839cb17976d7a869a717a19.mp4)
<video controls width="500">
  <source src="class/f6d461d38839cb17976d7a869a717a19.mp4" type="video/mp4">

</video>





##  6. <a name='-1'></a>🪶贡献

本项目由上海人工智能实验室、上海交通大学、上海交通大学附属第九人民医院和华东师范大学合作完成。联合研发团队由王延峰教授领衔，成员包括[张娅](https://mediabrain.sjtu.edu.cn/yazhang/)教授、[王钰](https://mediabrain.sjtu.edu.cn/yuwang/)副教授、[王琳琳](https://faculty.ecnu.edu.cn/_s16/wll/main.psp)研究员，何悦教授团队（李然），贺樑，欧阳泽田，邱易帅，蔡琰，张燮驰，杨宇辰，廖育生，郭逸秋等。



##  8. <a name='-1'></a>引用

@misc{MedEvalHub,
  author={Yan Cai, Linlin Wang,Ye Wang, Gerard de Melo, Ya Zhang, Yan-Feng Wang, Liang He}, 
  title = {MedEvalHub: A Large-Scale Chinese Benchmark for Evaluating Medical Large Language Models,
  year = {2024},
  publisher = {AAAI},
  journal = {Proceedings of Thirty-Eighth AAAI Conference on Artificial Intelligence(AAAI-2024)},
}

@misc{Autoeval,
  author={Yusheng Liao, Yutong Meng, Hongcheng Liu, Yanfeng Wang, Yu Wang}, 
  title = {An Automatic Evaluation Framework for Multi-turn Medical Consultations Capabilities of Large Language Models,
  year = {2023},
  journal = {Arxiv},
}

@misc{UniMedeEval,
  author={Yuchen Yang, Yusheng Liao, Ya Zhang, Yanfeng Wang, Yu Wang}, 
  title = {GenMedicalEval: A Unified Medical Evaluation Benchmark for Chinese LLMs,
  year = {2023},
  journal = {Arxiv},
}
