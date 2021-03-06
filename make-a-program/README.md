# 如何构建一个识别英语的程序

现在我们不讨论你如何学英语，而是**让你构建一个可以识别、交流英语的程序，你会如何设计？**

## 简单的需求分析

以中文为例，当你听到一个女人对一个男人说：“你是一个男人吗？”时，你会收集到哪些信息？你需要哪些信息来明确这个女人想表达的确切意思？

首先是听力输入，你需要确保麦克风录入了音频，然后拿到的声波内容是 U*#@&*!&*&*。之后我们需要将声波内容输入到一大堆分析器中进行分析，并得到比较精准的意图。

第一个可能是性别分析器，通过一定的规则识别出这是一个男性的声音还是女性的声音。因为这句话是男的说出来还是女的说出来表达的意思是不一样的。

第二个就是内容识别器，先是加载粤语匹配引擎和粤语语料库发现声波无法匹配解析，那么换成普通话引擎和语料库。此时如果你的语料库里有 “你”、“是”、“一个”、“男人”、“吗” 这些声音素材，那么就可以匹配解析出这句话：“你是一个男人吗？”。**换言之，如果你没有粤语语料库和解析引擎，即便是给你一段粤语录音你也听不懂。如果这句话有一个生僻单词你语料库里没有，那么也是无法识别出来。**

之后还有更多识别器，比如年龄、情绪识别器、重音和疑问语气识别句等，这些因素共同决定了这句话究竟想要传达什么意思。如果是一个女性的激动的感叹语气“你是一个男人吗！”，那么可以推测出这个女的跟男的有一定的关系，这个男的做出了一些伤天害理的事情导致这个女性在质问。如果是一个轻声细语的疑问句“你是一个男人吗？”，可能是一名女性想确认对方的性别。当然更准确表达这个意图的句子应该是“你是男性吗？”或者“男的女的？”。

## 比较基础的方案设计

上面需求分析只是简单的介绍了 `声音 -> 听力识别器 -> 意图` 的过程，实际上**语言交流是听说读写，其中包含两个识别器（听力识别器和视力识别器），一个核心理解器，两个表达器（口语表达器和书写表达器）**。通过对应的实际场景，我们可以简单的梳理出对应需要的功能。

### 听力识别器

* **听力能力**
  * 说明：要求可以输入声音并转换成一种可分析的信号。
  * 训练：买个好麦克风，对应人类是保护好耳朵和听力。
* **口音识别器**
  * 说明：各类方言比如粤语，各种口音比如东北口音、广东口音、英式发音和美式发音。
* **语言特性识别器**
  * 说明：语言之间会有不同特性，比如中文没有略读，都是一个一个字念出来，而英文会为了说话省劲而略读或者连读，比如 “drink it” 并不是单个蹦的 “准克一特”，而是类似 “准kei特”。中文的 “喝它” 就是 “喝它”，不会有类似 “赫特” 之类的变化。
  * 训练：扩充特殊语言引擎的匹配规则，扩充语料库，当听到 “准kei特” 可以识别出是 “drink it”。
* 音量调节和杂音处理器
  * 说明：可以通过算法过滤无用杂音，并将小音量调大使其清晰。人类天然进化出这种能力，无需特殊训练。
* 语气、性别、身份、语速识别器
  * 说明：人类天然进化出这种能力，无需特殊训练。
* 上下文缓存器
  * 说明：交流过程要有上下文内容缓存，结合输入理解器。

### 视力识别器

* 视力能力
* 图形识别器
  * 说明：不同字体、变形（英文大小写、中文繁简体等）都可以识别出来具体字符，同时需要识别标点符号等输入理解器。
  * 训练：识别能力、精准度和速度。比如一眼看出 `message` 和 `massage` 是不一样的。
* 上下文缓存器

### 理解器

理解器可以说是最重要的部分了，也是最难的部分

* **语料库**
  * 说明：字母、单词、发音、多重语境含义、历史文化背景、不同形态，同义词反义词相近词。
  * 训练：需要长期积累和扩充，需要大量训练。
* **识别引擎**
  * 说明：单词拼装起来的句型句式、语法、时态含义和规则、标点符号、单复数、惯用表达。
  * 训练：单点突破，专项训练，逐步体系化积累。
* **思考和思维能力**
  * 说明：针对意图结合之前的记忆以及经验得出自己想要表达的意图。
  * 训练：结构性表达，思维能力锻炼，思考和总结能力。这个与语言无关。
* 上下文缓存器

### 口语表达器

当理解器思考运算并得到想要表达的意图之后，就需要开始表达传递出去。

* **意图语料组装器**
  * 说明：将意图结合语料中的单词、句型句式、惯用表达进行匹配组合，挑选出最符合你意图的语句。
* **发音器**
  * 说明：根据组装出来的内容，结合特殊的连读、略读等语言特性，转换成发声信号。对应人类的话是**控制舌头、声带和呼吸系统的肌肉使其变成对应形状，让气流通过声带发出对应声音。**

### 书写表达器

* 意图语料组装器
* 书写表达器
  * 说明：将语料组装结果以视觉的方式表达，对于人类是控制手部肌肉书写出对应形状。

从上面可以看出，口语听力相对于阅读写作更加困难，主要因为实时性的要求。你必须迅速反馈不经过思考，这要求**你要无意识的去用英语表达**，所以语言学习没有技巧，只有大量训练。