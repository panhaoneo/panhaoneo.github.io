+++
title = 'AI入门学习规划'
date = 2025-02-08T12:22:58+08:00
draft = false
+++

2025年AI在国内已经出现deepseek这个现象级产品了。今天是2月8日，今年有个规划就是学习一下AI的知识。
想达到的目标是能理解AI的基本原理和训练过程等。

## HN的建议

首先，虽然我认为学习多种语言（python、R、matlab、julia）是有益的，但我建议选择一种，以免自己不知所措和惊慌失措。我建议使用 python，因为它有很好的工具和大量的学习资源，而且大多数前沿神经网络操作都是用 python 进行的。

那么对于整体课程，我建议：

1. 从基础机器学习（不是神经网络）开始，特别是阅读 [scikit-learn](https://scikit-learn.org/stable/index.html) 文档并在 YouTube 上观看一些教程。花一些时间熟悉 [jupyter notebook](https://jupyter.org/)和 pandas，并解决一些实际问题（kaggle 很棒，或者在 google 上搜索让你感兴趣的数据集）。确保你可以解决回归、分类和聚类问题，并了解如何衡量解决方案的准确性（了解诸如精度、召回率、mse、过度拟合、训练/测试/验证分割等内容）

2. 熟悉传统机器学习后，通过学习 [fast.ai](https://www.fast.ai/) 课程深入研究神经网络。这门课程非常棒，可以让你自信地构建近乎前沿的问题解决方案

3. 选择一个特定的问题领域并观看斯坦福相关课程（例如计算机视觉的 [cs231n](https://cs231n.stanford.edu/) 或 NLP 的 [cs224n](https://web.stanford.edu/class/cs224n/)）

4. 开始阅读论文。我建议使用 Mendeley 做笔记并整理。斯坦福课程会提到论文。阅读这些论文以及它们引用的论文。

5.开始尝试自己的想法和实施方案。

在完成上述操作的同时，补充：

* [Talking Machines](https://www.thetalkingmachines.com/) 和 [O'Reilly Data Show](https://www.oreilly.com/radar/topics/oreilly-data-show-podcast/)播客

* 在 Twitter 上关注 Richard Socher、Andrej Karpathy 和其他顶尖研究人员

祝你好运并享受！

## 资源整理
 - [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/) 免费的在线书籍，介绍神经网络和深度学习的。
 - [Goodfellow、Bengio 和 Courville 合著的第一本官方深度学习书籍](https://www.deeplearningbook.org/),本书有[中文版](https://book.douban.com/subject/27087503/)
 - [ 由 Andrew Ng 创办的深度学习在线课程](https://www.deeplearning.ai/) 
 - [统计学习简介](http://www-bcf.usc.edu/~gareth/ISL/) [统计学习要素](https://web.stanford.edu/~hastie/ElemStatLearn/)两本不错的电子书。与 R 搭配得很好。
 - [fast.ai](http://course.fast.ai)。实用，切中要点，理论+代码。
 - 使用 Scikit-Learn 和 TensorFlow 进行机器学习实践（http://amzn.to/2vPG3Ur）。理论与代码，从 sckikit-learn、pandas、numpy 上的“浅层”学习（例如线性回归）开始；然后转向使用 TF 进行深度学习。
 - 机器学习指南 (http://ocdevel.com/podcasts/machine-learning）。通勤/锻炼背景巩固理论。提供课程和资源。
 - Andrew Ng 在 Coursera 上的教程[1](https://www.coursera.org/learn/machine-learning )非常好。如果你对 Python 编程感兴趣，那么 sentdex[2](https://pythonprogramming.net/data-analysis-tutorials/) 的教程也很不错，涵盖了 scikit、tensorflow 等内容（更多是实践，更少理论）
 -  这实际上并没有回答问题，但我一直认为想要研究神经网络的人应该阅读 Marvin Minsky 的《感知器》。这是一本学术著作。它很短。它写得非常好，而且很容易理解。它塑造了几十年来神经网络研究的历史（呃……不幸的是，它停止了 :-) ）。你应该可以在任何大学图书馆找到它。虽然这个建议并不真正符合海报的要求，但我认为很容易首先寻求现代的、重新包装的解释而忽略科学文献。我认为这是非常危险的。有时我认为人们有点害怕看原始资料，所以如果你好奇的话，这是一个很好的起点。
 - github上的[awesome-deep-learning](https://github.com/josephmisiti/awesome-machine-learning)资源列表
 - github上的[awesome-machine-learning](https://github.com/ChristosChristofidis/awesome-deep-learning)资源列表
 - arxiv.org 学习模型，SemanticScholar 查找论文之间的联系，GitHub 搜索查找其他人的实现以及 Andrej Karpathy 的 Sanity Preserver 网站，可以更轻松地搜索和查看 Arxiv 论文： http://www.arxiv-sanity.com/
 - 在教授人工智能基础知识和内部工作原理直觉的相关主题上，有一个名为“AI Unplugged”[1](http://www.aiunplugged.org)的精彩材料，可以使用笔、卡片等以游戏的方式进行活动。我曾多次向不熟悉 AI/ML 领域的各种受众（儿童和成人）使用这种材料，每次人们似乎都很享受它并对他们所生活的现代世界有了一点了解。

## 我筛选的资源和学习的计划

### 我的学习思路
- 先入门理解机器学习，神经网络和当下最新的ai技术的概念性知识。有个全局的认识。
- 然后再深入学习一些具体的技术，比如深度学习，计算机视觉，自然语言处理等。
- 最后再学习一些实践的项目，比如kaggle上的项目，或者自己找一些数据集，做一些实践项目。

### 我的学习计划
根据你的学习思路和目标，我帮你整理了一份逐步的学习计划，旨在帮助你系统地掌握AI的基本原理、技术和实践项目。你可以根据自己的节奏调整，确保每个阶段都扎实掌握。

#### 第一阶段：AI基础入门（1-2个月）
目标：建立对AI基本原理和概念的全局认识。

1. **了解 AI 的基本概念与发展历程**
   - **AI 的历史与演变**：
     - 了解 AI 从早期的符号主义到现代的深度学习的发展历程。
     - 读一读关于 AI 的一些经典书籍或者文章，例如 **《人工智能：一种现代的方法》（Stuart Russell & Peter Norvig）**，这是 AI 领域的经典教材，系统性地讲解了 AI 的基本原理和发展历史。
   - **AI 的主要分支**：
     - **机器学习**、**深度学习**、**强化学习** 等不同领域的基本概念与区别，了解各自的应用场景。
     - 学习基本的人工智能应用，特别是在计算机视觉、自然语言处理、自动驾驶等领域的前沿进展。

2. **AI 的应用场景与社会影响**
   - **AI 的实际应用**：
     - 阅读一些关于 AI 在实际场景中应用的文章或案例，了解 AI 在医疗、金融、教育、制造业等领域的应用。可以关注一些行业白皮书、技术博客或者 **AI Trends**、**MIT Technology Review** 等媒体上的相关报道。
     - 学习一些典型的 AI 项目，如 Google 的 AlphaGo、Tesla 的自动驾驶系统、OpenAI 的 GPT 系列等，了解它们背后的技术与挑战。
   - **AI 对社会的影响**：
     - 思考 AI 对社会、经济、就业等方面的影响。可以阅读一些关于 **AI伦理**、**AI监管**、**AI对就业的影响** 等方面的文章。
     - 例如，了解 **AI 伦理** 和 **公平性问题**，比如如何避免模型的偏见和不公平性（bias），以及如何在设计 AI 系统时考虑这些因素。

3. **AI 基础的数学和编程概念**
   - **编程语言**：
     - 尽管你已经决定使用 Python，但在第一阶段，建议你快速浏览一下 Python 的基础概念，确保对基础语法、数据结构有一个清晰的认识。可以通过《Python编程快速上手》（Eric Matthes）等教材来学习。
   - **数学概念**：
     - 在学习机器学习的基础时，理解一些基本的数学概念（线性代数、微积分、概率统计等）是很有帮助的。虽然深入数学内容可以放到后期，但通过简单的例子和直观的图示理解基本概念是非常重要的。
     - 推荐查看 **Khan Academy** 的相关课程，或 [3Blue1Brown](https://www.youtube.com/c/3blue1brown) 的视频系列，帮助你更直观地理解线性代数和概率论。

4. **机器学习的类型和常见算法**
   - **学习机器学习的三种主要类型**：
     - **监督学习**（Supervised Learning）：学习如何从标注数据中建立模型，常见算法有线性回归、决策树、SVM 等。
     - **无监督学习**（Unsupervised Learning）：学习如何从无标签数据中发现模式，常见算法有 K-means、PCA 等。
     - **强化学习**（Reinforcement Learning）：学习如何通过与环境交互来最大化奖励，典型应用为自动驾驶、游戏等。
   - **学习常见算法的直观理解**：
     - 对每种类型的算法，试着理解其背后的核心思想，而不仅仅是数学推导。例如，理解什么是模型的训练、验证、测试，如何评估模型的表现（准确率、召回率、F1 分数等）。
     - 在学习每个算法时，尽量结合实际的案例和代码实现，例如从 Kaggle 获取相关数据集，动手实践回归、分类、聚类问题。

5. **机器学习工具的基础了解**
   - **Python 的数据科学工具链**：
     - 学习和实践 **NumPy**、**Pandas** 和 **Matplotlib**，这些工具对数据预处理、数据分析以及结果可视化至关重要。你可以通过在线教程快速掌握这些工具的基本操作。
     - 学习如何使用 **Jupyter Notebook** 进行交互式编程，并解决实际问题。
   - **了解 scikit-learn**：
     - 学习如何在 scikit-learn 中实现常见的机器学习模型，并应用于简单的分类或回归任务。了解如何使用 scikit-learn 来处理数据、训练模型、评估模型效果。

6. **建立 AI 的全局认知框架**
   - **广泛接触 AI 领域的最新进展**：
     - 关注 **AI 领域的最新发展**，可以通过订阅博客、新闻网站（如 **MIT Technology Review** 或 **TechCrunch**）和学术期刊（如 **arXiv**）来跟踪前沿研究。
     - 通过参加线上或线下的讲座、研讨会等活动，与行业专家和同学交流，扩大你的视野。
   - **听播客**：例如，[**Talking Machines**](https://www.thetalkingmachines.com/) 或 [**The Data Skeptic**](https://dataskeptic.com/) 等播客可以帮助你在日常通勤或锻炼时轻松了解 AI 的热点话题。


- **学习机器学习基础**：
  - 阅读《统计学习简介》或《统计学习要素》，了解统计学习的基础。
  - 学习 [scikit-learn](https://scikit-learn.org/stable/index.html) 文档，掌握回归、分类、聚类等基本算法。
  - 熟悉 Jupyter Notebook 和 pandas，进行一些简单的数据分析。
  - 观看 YouTube 上相关的机器学习入门课程（例如，Andrew Ng 的 [机器学习课程](https://www.coursera.org/learn/machine-learning)）。
  - 尝试解决一些 Kaggle 的基础问题，练习回归和分类问题。
  
- **学习深度学习基础**：
  - 阅读 [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/) 这本书，理解神经网络的基本原理。
  - 初步接触 [TensorFlow](https://www.tensorflow.org/) 或 [PyTorch](https://pytorch.org/)，学习基本的深度学习框架。
  - 学习 [fast.ai](http://course.fast.ai) 的课程，快速了解深度学习的核心技术，并进行实践。

#### 第二阶段：深入学习神经网络与深度学习（2-3个月）
目标：掌握深度学习的核心技术，并开始研究前沿应用。

- **学习深度学习的细节**：
  - 阅读 [Goodfellow, Bengio, Courville](https://www.deeplearningbook.org/) 的《深度学习》一书，系统掌握深度学习的理论。
  - 学习计算机视觉或自然语言处理等具体领域的深度学习技术。可以选修斯坦福的 [CS231n](https://cs231n.stanford.edu/) 或 [CS224n](https://web.stanford.edu/class/cs224n/)。
  
- **深入理解神经网络的优化与训练**：
  - 学习如何使用神经网络解决实际问题，如图像分类、对象检测等。
  - 学习损失函数、梯度下降、反向传播等优化技术。
  - 在 [Kaggle](https://www.kaggle.com/) 上尝试一些中等难度的深度学习项目，如图像分类和文本分类等。

#### 第三阶段：研究前沿技术和论文阅读（3-4个月）
目标：提升对前沿技术的理解，并深入研究经典与最新的研究论文。

- **阅读经典和前沿的研究论文**：
  - 学习如何使用 [Mendeley](https://www.mendeley.com/) 管理论文。
  - 阅读斯坦福课程推荐的论文，特别是在计算机视觉和自然语言处理方面的经典论文。
  - 关注前沿的 AI 论文和技术，访问 [arXiv](https://arxiv.org/)，了解最新的研究进展。

- **关注顶尖研究人员**：
  - 在 Twitter 上关注 [Richard Socher](https://twitter.com/richardsocher)、[Andrej Karpathy](https://twitter.com/karpathy) 等顶尖研究人员，保持对 AI 最新发展的了解。

#### 第四阶段：实践项目与技能提升（4-6个月）
目标：将所学知识应用于实际项目，提升问题解决能力。

- **进行 Kaggle 竞赛**：
  - 选择你感兴趣的领域，参加 Kaggle 上的深度学习相关比赛，学习如何处理现实世界的数据，提升实战能力。
  
- **进行独立项目**：
  - 自己选择一个感兴趣的问题领域，找数据集并进行建模。例如，计算机视觉的图像识别，NLP 的情感分析等。
  - 可以尝试 [GitHub](https://github.com/) 上的开源项目，贡献代码，向实际应用场景迈进。

#### 补充学习资源
- **书籍**：深入阅读经典书籍，如《感知器》了解神经网络的历史。
- **播客**：收听 [Talking Machines](https://www.thetalkingmachines.com/) 和 [O'Reilly Data Show](https://www.oreilly.com/radar/topics/oreilly-data-show-podcast/) 了解最新的 AI 技术讨论。
  
