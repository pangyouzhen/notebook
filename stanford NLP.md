# stanford NLP

[网址链接](http://52opencourse.com/70/%E6%96%AF%E5%9D%A6%E7%A6%8F%E5%A4%A7%E5%AD%A6%E8%87%AA%E7%84%B6%E8%AF%AD%E8%A8%80%E5%A4%84%E7%90%86%E7%AC%AC%E4%B8%80%E8%AF%BE-%E5%BC%95%E8%A8%80%EF%BC%88introduction%EF%BC%89)

## 引言（什么是NLP）
### NLP主要难点问题 -- 歧义
### 常用模型
- 统计模型（主流）（下文介绍统计模型）
- 语言模型

## 文本处理基础
### 正则表达式（略）
### 分词
#### 词典
- 文本语料库的元素
    - type： 词典的元素，独立词条
    - token：独立词条在文本中每次出现的次数

#### 分词算法

- 基于机械的分词方法（只有词库）
- 基于统计的分词方法（结巴分词）
- 基于理解的分词方法（人）

#### 分词难点
- 切分歧义：中文书面语占比不大
- 未登录词：常见的方法有互信息，语言模型，基于最大熵或隐形马尔科夫模型的统计分类

#### 结巴分词的原理

最大概率法。使用了大规模语料库+HMM模型

- 已登录词。就是词库进行搜索。如何实现高效的搜索。第一个就是词库的存储了，高效的存储，第二个就是如何进行切分，遇到歧义的词如何进行切分，比如中国人，是中国 人？还是中国人
- 未登录词。HMM模型，使用了维特比算法。

### 文本归一化
大小写转换，词干提取，繁简互换（）

### 断句
句子分为大句和小句，大句子一般由“！”，“。”，“；”，“\“”、“？”等分割，小句一般由“，”分割，起停顿作用，需要上下文搭配表达特定的语义。

# 最小编辑距离（MED）

## Why

### 文本比较

linux 下的diff命令就是利用最小编辑距离进行比较的

### 拼写检查（spell correction）
将每个词与词典中的词条进行比较，如果不存在就被认为是个错误，然后提示N个最有可能的词---拼写检查
### DNA分析
### 命名实体抽取(Named Entity Extraction)
例如`IBM`与`IBM Inc`可以将候选文本与词典中的每个实体名称进行编辑距离计算，当发现文本中的某一字符串的编辑距离小于给定阀值，将其作为实体名候选词，获取实体名候选词后，根据所处上下文使用启发式规则和分类的方法判定候选词是否的确为实体名
### 实体共指(Entity Coreference)
根据任意两个实体名之间的最小编辑距离判定是否存在共指关系?`IBM`与`IBM Inc.`
### 机器翻译
1. 识别平行网页对
  什么是平行网络？抽取HTML标签连接成字符串，用最小编辑距离考察相似度。并结合文档长度比例，句对齐翻译模型配合使用，识别最终的平行网页对
2. 自动评测
3. 字符串核函数

## What

又被称为levenshtein距离，是指两个字符串之间，由一个转成另一个所需要的最少编辑次数，允许编辑的操作包括，将一个字符串替换成另一个字符（substitution,s）插入一个字符(insert，i),或者删除一个字符(delete)
- 如何利用动态规划求解最小编辑距离




### 变形
就是如何改进最小编辑距离

### 链接
[网址链接](http://52opencourse.com/96/%E6%96%AF%E5%9D%A6%E7%A6%8F%E5%A4%A7%E5%AD%A6%E8%87%AA%E7%84%B6%E8%AF%AD%E8%A8%80%E5%A4%84%E7%90%86%E7%AC%AC%E4%B8%89%E8%AF%BE-%E6%9C%80%E5%B0%8F%E7%BC%96%E8%BE%91%E8%B7%9D%E7%A6%BB%EF%BC%88minimum-edit-distance%EF%BC%89)

# 语言模型
### N-gram介绍
**如何计算一个句子出现的概率。**
$$p(S) = p(w_{1},w_{2},...,w_{n})= p(w_{1})p(w_{2}|p_w{1})p(w_{3}|w_{1},w_{2})...$$
基于马尔科夫(Markov Assumption)；下一个词的出现仅依赖于它前面的一个或者几个词

$bigram$
$$p(S)=p(w_{1})p(w_{2}|w_{1})P(w_{3}|w_{1},w_{2})...=p(w_{1})p(w_{2}|w_{1})p(w_{3}|w_{2})...p(w_{n}|w_{n-1})$$
$trigram$
$$p(S)=p(w_{1})p(w_{2}|w_{1})P(w_{3}|w_{1},w_{2})...=p(w_{1})p(w_{2}|w_{1})p(w_{3}|w_{2},w_{1})...p(w_{n}|w_{n-1},w_{n-2})$$

实际问题中，我们面临如何依赖词的个数即n
- 更大的n,对于下一个词更有约束力，具有更大的辨别力
- 更小的n,在训练语料库中出现的次数更多，具有更可靠的统计信息，具有更高的可靠性
  一般采用的是bigram，随后是trigram

### 构造语言模型
通过计算最大似然估计(Maximum Likelihood Estimate)构建模型

[例子](http://52opencourse.com/111/%E6%96%AF%E5%9D%A6%E7%A6%8F%E5%A4%A7%E5%AD%A6%E8%87%AA%E7%84%B6%E8%AF%AD%E8%A8%80%E5%A4%84%E7%90%86%E7%AC%AC%E5%9B%9B%E8%AF%BE-%E8%AF%AD%E8%A8%80%E6%A8%A1%E5%9E%8B%EF%BC%88language-modeling%EF%BC%89)

可能的问题：某些词并没有出现过，所以导致整体的概率为0

### 语言模型评价
- 实用方法；通过具体应用中的表现来看
- 理论方法：迷惑度/困惑度/混乱度(preplexity) 其基本思想是给测试集赋予较高概率值的语言模型较好

### 数据稀疏与平滑技术

基本思想：降低已出现的n-grams的条件概率分布，使未出现的n-grams条件概率分布不为0
- Add-One(Laplace) smoothing

    加一平滑法，又称拉普拉斯定律公式如下：
        - MLE estimate:
    $$p(w_{i}|w_{i-1}) = \frac{c(w_{i-1},w_{i})}{c(w_{i-1})}$$
        - add-1 estimate:
    $$p(w_{i}|w_{i-1}) = \frac{c(w_{i-1},w_{i})+1}{c(w_{i-1})+v}$$
    其中v是所有的bigram的个数
- Good-turing Smoothing

    其基本思想是利用频率的类别信息对频率进行平滑，调整出现为c的n-gram频率为$c^{*}$:
    $$r^{*}=(r+1)\frac{n_{r+1}}{n_{r}}$$
    $$p(x:c(x)=r) = \frac{r^{*}}{N}$$
    $$ where N=\sum_{r=0}^{\infty}r^{*}n_{r}=\sum_{r=1}^{\infty}rn_{r}$$

- Interpolation Smoothing

利用低元n-grams模型对高元n-grams进行线性插值
具体步骤如下
    - 首先，确定training data，held-out data,test-data
    - 然后，根据training data 构造初始的语言模型，并确定初始的 $\lambda*s$
    - 根据EM算法迭代地优化，使得held-out data 概率最大化
- Kneser-Ney Smoothing
- Web-scale LMS

### 语言模型的变种

- Class-based N-gram Model
- Topic-based N-gram Model

    该方法将训练集划分为多个子集，并对每个子集分别建立N-grams语言模型，以解决模型的主题自适应问题

- Cache-based N-grams Model
  可能是智能拼音的用法
- Skipping N-gram Model & Trigger-based N-gram Model
  二者的核心思想都是刻画距离的约束关系
- 指数语言模型：最大熵模型MaxEnt、最大熵马尔科夫模型MEMM，条件随机域模型CRF


## 拼写检查
### 任务定义
    拼写纠错一般可以分为两个子任务

    - Spelling Error Detection: 按照错误的类型不同，分为Non-word Errors和Real-word Errors
    - spelling Error correction: 自动纠错，将hte-the
### Non-word Errors
    将单词拼写为词典中并不存在的词 mean -> menn

    - 发现：任何不存在词典中的词都被视为错误，准确率依赖于词典的规模和质量
    - 纠正：查找词典中最为相近的词常见的方法有：Shorttest weight edit distance 和 Highest noisy channel probility
### Real-word Errors:
    将单词拼写为其他单词 there -> three

    - 发现：每个word都作为拼写错误的候选
    - 纠正：从发音和拼写的角度，查找与word最相近的词的集合，常见方法有highest noisy channel probility和classifier
### 基于Noisy channel Model的拼写纠错

    Noisy channel Model即噪声信道模型，或称信源信道模型，普遍用于语音识别，拼写纠错，机器翻译，中文分词，词性标注，音字转换

[链接](http://52opencourse.com/138/%E6%96%AF%E5%9D%A6%E7%A6%8F%E5%A4%A7%E5%AD%A6%E8%87%AA%E7%84%B6%E8%AF%AD%E8%A8%80%E5%A4%84%E7%90%86%E7%AC%AC%E4%BA%94%E8%AF%BE-%E6%8B%BC%E5%86%99%E7%BA%A0%E9%94%99%EF%BC%88spelling-correction%EF%BC%89)

    noisy word(spelling error)被看作是original word(用x表示)通过noisy channel转换得到的，现在已知noisy word，如何求的最大可能的original word(用w表示)，公式如下：
    P(w)为先验概率，P(x|w)为转移概率，二者可以基于训练语料库的建立语言模型和转移矩阵(又称为 error Model，channel Model)得到，具体例子查看链接

### Real—word 拼写纠错

    通常解决办法有两步：
    - For each word in sentence
        - Generate candicate set
            - the word itself
            - all single-letter edit that are English words
            - words that are homophone
    - Choose best candidates
        - Noisy channel model
        - Task-specific classifiter

### 应用

    实际中的拼写纠错系统一般会遵守HCI(Human Computer Interface) 准则
    - if very confident in correction
        - Autocorrect
    - Less confident 
        -give the best correction
    - Less confident 
        - give a correction list
    - Unconfident
        - Just flag as an error
    
    根据应用场景的不同(Domain Sensitivity)，需要对语言模型进行性特别的处理
    
    除了字面的拼写错误，还有可能同音错误，所以有些系统将‘error model’转化为‘phonetic error model’解决拼写纠错问题
    
    另外键盘按键可能引起Spelling error pair，可以根据转移矩阵进行加权
    
    我们还可以将拼写纠错能力转化为分类问题，通过建立语料库，抽取特征，训练分类模型，预测新实例等一系列过程解决


#文本分类(Text Classification)

###  The task of text classification

常见的分类任务
- assigning subject category，topics，or genres：识别文本描述的主题
- spam detection：典型的就是垃圾邮件的识别与过滤
- authorship  identification.作者识别，例如红楼梦的作者
- sentiment Analysis：情感分析 好评差评
- age/gender identification
- language identification

常见的分类方法：
- hand-coded rules：人工总结分类规则
- supervised Machine learning：有监督的机器学习。下文中以朴素贝叶斯为例

### 朴素贝叶斯

在分类的过程中，文本通常被表示为bag of words的形式，即假设文本中每个词汇的出现相互独立，并且不考虑出现的先后顺序。通过判定文本中包含的情感类词汇的判断文本的极性，然后根据度量测试文本与训练文本之间的相似度来进行文本分类

### 贝叶斯的计算

p(c|d)表示文档d属于某类别c的概率，那么：
$$P(c|d) =\frac{P(d|c)P(c)}{P(d)}$$
则文档d的类别为$C_{MAP}$，即后验概率最大的类别，计算过程如下：
$$C_{MAP} = argmax_{{c}\epsilon{C}}P(c|d)=argmax_{{c}\epsilon{C}}\frac{P(d|c)P(c)}{P(d)}$$

### 贝叶斯学习：

我们的主要任务是估计p(c)和p(x|c)
首先，最直接的办法就是在训练语料库的基础上，应用极大似然估计法(Maximum likelihood estimates)估计相应的概率，仍然可能出现估计的概率值为0的情况，解决这一问题的思路是采用贝叶斯估计，采用语言模型中的拉普拉斯平滑技术

### 朴素贝叶斯与语言模型之间的关系

### 多分类朴素贝叶斯：一个实际的例子

### Evaluation:Precision,Recall and F measure

Precison,Recall 和F—measure是文本分类任务中最常用的评价方法

### 文本分类中的实际问题

实际中，朴素贝叶斯分类器的计算中，涉及大量的概率浮点数的乘法计算，在工程实现上，为了避免floating-point underflow 问题，通常将乘法转化成log运算，乘法转化为加法也提高了速度

最后，实际系统中还会有许多其他的特征加权和过滤策略用于优化分类器的性能

### 其他主题

- 二元分类和多元分类：

    解决多元分类问题的基本思想是转化成二元分类任务，通常有如下的两种解决方式
    - 一对多：训练时依次将某个类别的样本归为一类，其余剩余的样本归为另一类
    - 一对一法
- 软分类和硬分类

    即大多时候文档以一定的概率属于特定的类别，即文档可以同时属于多个类别

- 层次化分类

    一般实用系统面临的分类任务基于层次化分类体系，通常的解决办法有自底向上和自顶向下两种策略，基本思想是将每层看作独立的多元分类任务，知识上下层级之间可以传递分类概率，也可以进行剪枝，节省计算，最终的训练分类器模型个数至少是层次化类别体系中的非叶节点的个数

# 情感分析(sentiment analysis)

### Why?

又被称为倾向性分析，意见抽取(Opinion extraction)，意见挖掘（Opinion mining）,情感挖掘（sentiment mining），主观分析（subjectivity）,它是对带有感情色彩的主观性文本进行分消息、处理、归纳、推理的过程，如从评论文本中分析用户对数码相机的变焦价格，大小重量闪光，等属性的情感倾向。
例子如下：
- 电影的影评
- google product search
- bing shopping
    - twitter sentiment 基金。情感分析的主要目的是识别用户对事物或人的看法、态度。参与的主体包括: Holder(Source): 观点持有者Target(aspect): 评价对象；Type of attitude:评价观点
    - from a set of types: like,love,hate,value,desire,etc.
    - simple weighted polarity:positive,negative,neutral,together with strength
- text containing the attitude:评价文本，一般是句子或者是整篇文档

通常我们面临的情感分析任务包括如下几类：
1. Simplest task:态度是消极还是积极
2. More complex：评分的等级
3. Advanced:Detect the target,source,or complex attitude type

后续任务以simplest task 为例

### A Baseline Algorithm

可以将问题拆取为如下的子任务:
1. Tokenization：正文抽取，过滤时间，电话号码，切词等
2. Feature Extraction：根据形容词和频率进行构建，但是应当注意否定词
3. 使用不同的分类器模型进行分类
4. 总结：其中的难点是什么？
    - 语言的表达含蓄微妙
    - 有的评论含有转折

### sentiment Lexicons

情感分析模型非常依赖于情感词典抽取特征和规则。文中提供了一些情感词典资源

### learning sentiment lexicons

常见的情感词典构建方法是基于半指导的bootstrapping 方法，主要包括两步
1. use a small amount of information(seed)
    a. A few labeled examples
    b. A few hand-built patternd
2. to bootstrap a lexicon

详细方法见原文
### Other sentiment tasks
实际上，一篇文档中往往提及不同的方面/属性/对象,且对于不同的属性持有不同的倾向性例如:'the food is great but the service is awful' 一般通过frequent + rules的方法抽取评价的属性，如下：
    - find all highly frequent across reciews('fish tacos')
    - filter by rules like 'occurs right after sentiment word','great fish tacos' means fish tacosn likely aspect.

通常，我们面临一种问题：评价属性缺失，准确的讲，评价属性不在句子中，这是很常见的现象，此时就需要结合上下文环境，如来自某电影的评价属性的缺失基本上就是电影名或者演员，可以基于已知评价属性的句子训练分类器，然后对评价属性缺失的句子进行属性预测。


[以gensim训练词向量](http://zake7749.github.io/2016/08/28/word2vec-with-gensim/)