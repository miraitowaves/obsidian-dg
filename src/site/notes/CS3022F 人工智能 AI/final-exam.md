---
{"dg-publish":true,"permalink":"/CS3022F 人工智能 AI/final-exam/","dgPassFrontmatter":true,"noteIcon":""}
---


## 00 考试说明

历年各章的题型和分数分布：
![Pasted image 20250613112753.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250613112753.png)


---
## 01 知识表达与推理

- 什么是逻辑：进行正确推理和充分论证的研究
- 符号主义人工智能 (symbolic AI) 就是脱胎于**逻辑推理**

逻辑关心的问题：
- 从**前提**出发，是否存在一个**有效的论证或推理**来支持所得到的**结论**
- 逻辑是一门研究**推理**的科学
- **逻辑和推理**是人工智能的核心问题：通过**归纳**和**演绎**等手段对现有观测现象由果溯因 (归纳) 或由因溯果 (演绎)

规范化的逻辑知识：
- 人类认识世界的途径源于**学习技能**和**解释已得知识**
- 认知最重要的一种表现是**分类**
- **知识树/科学树** 👉 对知识进行规范化描述
- **人类思想字母表** 👉 按照规则组合，构造思想机器

知识表达方法
- 命题逻辑
- 谓词逻辑
- **产生式规则**
- **框架表示法**
- 知识图谱
- ...

### 1.1 命题逻辑
#### 命题

命题：一个能确定为真或为假的陈述句
- 用小写符号来表示，如 p 或者 q
- 总有一个“值”，称为真值：为真 True 或为假 False
- 无法判断真假的描述性句子都不能作为命题

> [!example]-
> ![Pasted image 20250604185605.png|475](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604185605.png)


分类
- 原子命题：简单命题，不包含其他命题作为其组成部分的命题
- 符合命题：包含其他命题作为其组成部分的命题
- 可通过命题联结词 (connectives）对已有命题进行组合，得到新命题

| 命题连接符号               | 表示形式  | 意义                                   |
| -------------------- | ----- | ------------------------------------ |
| 与 (and)               | $p∧q$ | 命题合取 (conjunction)，即“$p$ 且 $q$”         |
| 或 (or)                | $p∨q$ | 命题析取 (disjunction)，即“$p$ 或 $q$”         |
| 非（not）               | $¬p$  | 命题否定 (negation)，即“非 $p$”               |
| 条件 (conditional)      | $p→q$ | 命题蕴含 (implication)，即“如果 $p$ 则 $q$”       |
| 双向条件 (bi-conditional) | $p⟷q$ | 命题双向蕴含 (bi-implication)，即“$p$ 当且仅当 $q$” |

> [!NOTE] 条件命题联结词中前件为假时，无论后件取值如何，复合命题恒为真

逻辑等价：给定命题 $p$ 和命题 $q$, 如果 $p$ 和 $q$ 在所有情况下都具有同样真假结果，那么 $p$ 和 $q$ 在逻辑上等价，一般用 $\equiv$ 来表示，即 $p\equiv q$

| 逻辑等价的例子                                                                    |                                                                                                  |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| $\alpha\land\beta\equiv\beta\land\alpha$ (Λ的交互律)                           | $(\alpha\rightarrow\beta)\equiv\neg\alpha\lor\beta$ (蕴涵消除)                                       |
| $\alpha\lor\beta\equiv\beta\lor\alpha$ (∨的交互律)                             | $(\alpha\leftrightarrow\beta)\equiv(\alpha\rightarrow\beta)\land(\beta\rightarrow\alpha)$ (双向消除) |
| $(\alpha\land\beta)\land\gamma\equiv\alpha\land(\beta\land\gamma)$ (Λ的结合律) | $\neg(\alpha\land\beta)\equiv(\neg\alpha\lor\neg\beta)$ (德摩根定律)                                  |
| $(\alpha\lor\beta)\lor\gamma\equiv\alpha\lor(\beta\lor\gamma)$ (∨的结合律)     | $\neg(\alpha\lor\beta)\equiv(\neg\alpha\land\neg\beta)$ (德摩根定律)                                  |
| $\neg(\neg\alpha)\equiv\alpha$ (双重否定)                                      | $(\alpha\land(\beta\lor\gamma))\equiv(\alpha\land\beta)\lor(\alpha\land\gamma)$ (Λ对∨的分配律)        |
| $(\alpha\rightarrow\beta)\equiv\neg\beta\rightarrow\neg\alpha$ (逆否命题)      | $(\alpha\lor(\beta\land\gamma))\equiv(\alpha\lor\beta)\land(\alpha\lor\gamma)$ (∨对Λ的分配律)         |

#### 推理规则

推理是按照某种策略从前提出发推出结论的过程
- 用符号 $\Rightarrow$ 来表示推理过程

| 推理规则的例子                            |                                                                                                                                                                                                                       |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 假言推理<br>(Modus Ponens)             | $\frac{\alpha\rightarrow\beta,\ \alpha}{\beta}$                                                                                                                                                                       |
| 与消解<br>(And-Elimination)           | $\frac{\alpha_{1}\land\alpha_{2}\land\cdots\land\alpha_{n}}{\alpha_{i}(1\leq i\leq n)}$                                                                                                                               |
| 与导入<br>(And-Introduction)          | $\frac{\alpha_{1},\alpha_{2},...,\alpha_{n}}{\alpha_{1}\land\alpha_{2}\land\cdots\land\alpha_{n}}$                                                                                                                    |
| 双重否定 (Double-Negation Elimination) | $\frac{\neg\neg\alpha}{\alpha}$                                                                                                                                                                                       |
| 单项消解或单项归结 (Unit Resolution)        | $\frac{\alpha\lor\beta,\neg\beta}{\alpha}$                                                                                                                                                                            |
| 消解或归结 (Resolution)                 | $\frac{\alpha\lor\beta,\neg\beta\lor\gamma}{\alpha\lor\gamma}$ $\frac{\alpha_1\lor\alpha_2\lor\cdots\lor\alpha_m,\neg\alpha_k}{\alpha_1\lor\alpha_2\lor\cdots\lor\alpha_{k-1}\lor\alpha_{k+1}\lor\cdots\lor\alpha_m}$ |

> [!example]- 用推理规则解决问题
> ![Pasted image 20250613115504.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250613115504.png)
> ![Pasted image 20250613115543.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250613115543.png)


### 1.2 谓词逻辑

命题逻辑的局限性：在命题逻辑中，每个陈述句是最基本的单位 (即原子命题)，无法对原子命题进行分解
- 不能表达**局部与整体、一般与个别**的关系

谓词逻辑：将原子命题进一步细化，分解出个体、谓词 predicate 和量词 quantifier
- 个体：所研究领域中可以独立存在的具体或抽象的概念
- 谓词：刻画个体属性或者描述个体之间关系存在性的元素，其值为真或为假

#### 个体与谓词

例如，𝑃(𝑥) 表示：$𝑥<𝑥^2$ 
- 𝑃是谓词， 𝑥是个体，𝑥被称为变量，其具体取值叫个体常项

> [!NOTE] 函数与谓词的区别
> - 函数是从定义域到值域的映射
> - 谓词是从定义域到{True, False}的映射

> [!NOTE] 事实符号化
> 1. Richard 是国王。 
> 	- King (Richard)
> 	- 其中，Richard 是一个**个体常量**，King 是一个描述“国王”这个一元关系的谓词
> 2. Lucy 和 Lily 是姐妹
> 	- Sister (Lucy, Lily)
> 	- 其中，Lucy 和 Lily 是两个个体常量，Sitter 是一个描述“姐妹” 这个二元关系的谓词

#### 量词

量词
- 全称量词 (universalquantifier, ∀)
	- ∀𝑥表示定义域中的所有个体，∀𝑥𝑃(𝑥) 表示定义域中的所有个体具有性质 P
- 存在量词 (existentialquantifier, ∃)
	- ∃𝑥表示定义域中存在一个或若干个个体，∃𝑥𝑃(𝑥) 表示定义域中存在一个个体或若干个体具有性质 P

量词之间的逻辑等价关系
$$\forall xP(x)\equiv\neg\exists x\neg P(x)$$
$$\forall x\neg P(x)\equiv\neg\exists xP(x)$$
$$\neg\forall xP(x)\equiv\exists x\neg P(x)$$
$$\exists xP(x)\equiv\neg\forall x\neg P(x)$$


变元
- 约束变元在全称量词或存在量词的约束条件下的变量符号
- 自由变元：不受全称量词或存在量词约束的变量符号

相关的逻辑等价关系：
- A (x) 是包含变元 x 的公式，B 是不包含变元 x 的谓词公式
$$(\forall x)(A(x)\lor B)\equiv(\forall x)A(x)\lor B$$
$$
(\forall x)(A(x)\land B)\equiv(\forall x)A(x)\land B$$
$$(\exists x)(A(x)\lor B)\equiv(\exists x)A(x)\lor B$$
$$
(\exists x)(A(x)\land B)\equiv(\exists x)A(x)\land B$$
- A (x) 和 B (x) 是包含变元 x 的谓词公式
$$\left(\forall x\right)\left(A(x)\lor B(x)\right)\equiv\left(\forall x\right)A(x)\lor\left(\forall x\right)B(x)\text{（不成立）}$$
$$
\left(\forall x\right)\left(A(x)\land B(x)\right)\equiv\left(\forall x\right)A(x)\land\left(\forall x\right)B(x)$$
$$\left(\exists x\right)\left(A(x)\lor B(x)\right)\equiv\left(\exists x\right)A(x)\lor\left(\exists x\right)B(x)$$
$$
\left(\exists x\right)\left(A(x)\land B(x)\right)\equiv\left(\exists x\right)A(x)\land\left(\exists x\right)B(x)\text{（不成立）}$$
- 若多个量词都是全称量词或者都是存在量词，则量词的位置可以互换；若多个量词中既有全称量词又有存在量词，则量词的位置不可以随意互换
	设 A (x, y) 是包含变元 x y 的谓词公式：
$$(\forall x)(\forall y)A(x,y)\Leftrightarrow(\forall y)(\forall x)A(x,y)$$
$$
(\exists x)(\exists y)A(x,y)\Leftrightarrow(\exists y)(\exists x)A(x,y)$$
$$(\forall x)(\forall y)A(x,y)\Rightarrow(\exists y)(\forall x)A(x,y)$$
$$
(\forall x)(\forall y)A(x,y)\Rightarrow(\exists x)(\forall y)A(x,y)$$
$$(\exists y)(\forall x)A(x,y)\Leftrightarrow(\forall x)(\exists y)A(x,y)$$
$$
(\forall x)(\forall y)A(x,y)\Leftrightarrow(\forall y)(\exists x)A(x,y)$$
$$(\forall x)(\exists y)A(x,y)\Rightarrow(\exists y)(\exists x)A(x,y)$$
$$
(\forall y)(\exists x)A(x,y)\Rightarrow(\exists x)(\exists y)A(x,y)$$

设 $A (x)$ 是谓词公式，$x$ 和 $y$ 是变元，$a$ 是常量符号，则存在如下谓词逻辑中的推理规则：
- 全称量词消去 (Universal Instantiation, UI): $(\forall x) A (x)\to A (y)$
- 全称量词引入 (Universal Generalization, UG) $: A (y)\to (\forall x) A (x)$ 
- 存在量词消去 (Existential Instantiation, EI): $(\exists x) A (x)\to A (a)$ 
- 存在量词引入 (Existential Generalization, EG): $A (a)\to (\exists x) A (x)$


> [!EXAMPLE]- 谓词逻辑推理
> 例 2.12 已知：
> - $( \forall x) ( F ( x) \to ( G ( x) \wedge H ( x) )$
> - $( \exists x) ( F ( x) \wedge P ( x) )$
> 试证明：($\exists x)(P (x)\land H (x))$
> 
> 证明过程:
> 1. $(∀x)(F (x)→(G (x)∧H (x))$ (已知)
> 2. $(∃x)(F (x)∧P (x))$ (已知)
> 3. $F (a)∧P (a)$ (2 的 EI)
> 4. $F (a)→(G (a)∧H (a))$ (1 的 UI)
> 5. $F (a)$ (由 3 知)
> 6. $G (a)∧H (a)$ (4 和 5 的假言推理)
> 7. $P (a)$ (由 3 知)
> 8. $H (a)$ (由 6 知)
> 9. $P (a)∧H (a)$ (7 和 8 的合取)
> 10. $(∃x)(P (x)∧H (x))$ (9 的 EG)

> [!example]- 自然语言形式化
> 例 2.14 前提：1) 每驾飞机或者停在地面或者飞在天空；2) 并非每驾飞机都飞在天空
> 结论：有些飞机停在地面
> 形式化：plane $(x){:}x$ 是飞机；in\_ground $(x){:}x$ 停在地面；on\_fly $(x){:}x$ 飞在天空
> 已知：$(\forall x)(plane (x)\to in\_ground (x)$ V on fly $( x) )$, $( \neg \forall x) ( plane ( x) \to on\_ fly ( x) )$
> 请证明：($\exists x)(plane (x)\land in\_ground (x))$
> 
> 证明：
> 1. $~(\neg\forall x)(plane (x)\to on\_fly (x))$
> 2. $( \exists x) \neg ( plane ( x) \to on\_ fly ( x) )$
> 3. $( \exists x) \neg ( \neg plane ( x) \vee on\_ fly ( x) )$
> 4. $( \exists x) ( plane ( x) \land \neg on\_ fly ( x) )$
> 5. $plane ( a) \wedge \neg on\_ fly ( a)$
> 6. $plane ( a)$
> 7. $\neg on\_ fly ( a)$
> 8. $( \forall x) ( plane ( x) \to in\_ ground ( x)$ von\_fly $(x))$ (已知)
> 9. $plane ( a) \to in\_ ground ( a)$ V on\_fly $(a)$
> 10. $in\_ground (a)$ von\_fly $(a)$
> 11. $in\_ ground ( a)$
> 12. $plane (a)\wedge in\_ground (a)$
> 13. $( \exists x) ( plane ( x) \wedge in\_ ground ( x) )$


### 1.3 知识图谱推理

#### 基本概念

知识图谱
- 由**有向图**构成
- 每个节点是一个**实体**，如人名、地名、事件和活动等
- 任意两个节点之间的边表示这两个**节点之间存在的关系**
- 任意两个相连节点及其连接边表示成一个三元组（triplet）, 即 (left_node, relation, right_node)
	- 也可以表示为一阶逻辑 (first order logic, FOL) 的形式
	  relation (left_node, right_node)
![Pasted image 20250613120448.png|300](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250613120448.png)

**关系推理**是统计关系学习研究的基本问题：从现有知识发掘新的知识


现在面临一个问题，如何从知识图谱中推理得到：father (David, Ann) ？
- 从具体例子中学习如下规则
$$\begin{aligned}&(\forall x)(\forall y)(\forall z)\big(Mother(z,y)\wedge\:Couple(x,z)\\&\to Father(x,y)\big)\end{aligned}$$

#### 归纳逻辑程序设计 (inductive logic programming，ILP) 算法

ILP：使用**一阶谓词逻辑**进行知识表示，通过修改和扩充逻辑表达式对现有知识归纳，完成推理任务
- 代表性方法：一阶归纳学习 FOIL（First Order Inductive Learner）
	- 通过**序贯覆盖**实现规则推理


对于：
$$(\forall x)(\forall y)(\forall z)\big(Mother(z,y) \land Couple(x,z) \rightarrow Father(x,y)\big)$$
- 前提约束谓词：我们通过学习得到
- 目标谓词：已知

> [!NOTE] FOIL 算法
> - 输入：目标谓词 P, P 的训练样例（正例集合 E+和反例集合 E-），其他背景知识
> - 输出：推导得到目标谓词 $P$ 的推理规则
> ---
> - 流程
> 	1. 将目标谓词作为所学习推理规则的结论
> 	2. 将其他谓词逐一作为前提约束谓词加入推理规则，计算所得到推理规则的 FOIL 信息增益值，选取最优前提约束谓词以生成新推理规则，并将训练样例集合中与该推理规则不符的样例去掉
> 	3. 重复 2 过程，直到所得到的推理规则不覆盖任意反例


从一般到特殊，逐步添加目标谓词的前提约束谓词，直到所构成的推理规则不覆盖任何反例
- 从一般到特殊指的是对目标谓词或前提约束谓词中的变量赋予具体值，如将 
	$$(\forall x)(\forall y)(\forall z)(Mother(z,y)\land Couple(x,z)\to Father (x, y))$$
- 这一推理规则中目标谓词 Father (x, y) 所包含的 x 和 y 分别赋值为 David 和 Ann，进而进行推理


哪些谓词好呢？ 可以作为目标谓词的前提约束谓词？
- 通过 FOIL 中的**信息增益值**来衡量
$$FOIL_{Gain}=\widehat{m_{+}}\cdot\left(\log_{2}\frac{\widehat{m_{+}}}{\widehat{m_{+}}+\widehat{m_{-}}}-\log_{2}\frac{m_{+}}{m_{+}+m_{-}}\right)$$
- 其中，$\widehat{m_{+}}$ 和 $\widehat{m_{-}}$ 是增加前提约束谓词后所得新推理规则覆盖的正例和反例的数量，$m_+$ 和 $m_-$ 是原推理规则所覆盖的正例和反例数量

> [!example]-
> 
> ![Pasted image 20250604204059.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204059.png)
> ![Pasted image 20250604204113.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204113.png)
> ![Pasted image 20250604204150.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204150.png)
> ![Pasted image 20250604204214.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204214.png)
> ![Pasted image 20250604204451.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204451.png)
> ![Pasted image 20250604204554.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204554.png)
> ![Pasted image 20250604204705.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604204705.png)


#### 路径排序算法（path ranking algorithm, PRA）

路径排序推理算法（PRA）的基本思想：**将实体之间的关联路径作为特征，来学习目标关系的分类器**
可以分为如下三步：
- **特征抽取**：生成并选择路径特征 $\pi$ 的集合
	- 生成路径的方式有随机游走 (random walk)、广度优先搜索、深度优先搜索等
- **特征计算**：计算每个训练样例的特征值 $P (s\to t;\pi_j)$
	- 特征值表示从实体节点 s 出发，通过关系路径 $\pi_j$ 到达实体节点 $t$ 的概率
	- 也可以表示为布尔值，表示实体 s 到实体 $t$ 之间是否存在路径 $\pi_j$
	- 还可以是实体 s 和实体 $t$ 之间路径出现频次、频率等
- **分类器训练**：根据训练样例的特征值，为目标关系训练分类器。当训练好分类器后，即可将该分类器用于推理两个实体之间是否存在目标关系

> [!example]-
> ![Pasted image 20250604205110.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604205110.png)


### 1.4 概率图谱推理

概率图（probabilistic graph）
- 如果两个节点之间存在连边，则可视为这两个节点之间具有概率依赖关系而相互影响。
- 在这类图中，可用概率描述两个相连节点之间的关联，而不是假设节点之间的影响一定会百分之百发生。
- **基于概率图进行的推理被称为概率推理**

概率图模型一般分为贝叶斯网络（Bayesian Network）和马尔可夫网络（Markov Network）两大类
- 贝叶斯网络
	- 用一个**有向无环图**（directed acyclic graph）来表示，其用有向边来表示节点和节点之间的**单向概率依赖**
- 马尔可夫网络
	- 表示成一个无向图的网络结构，其用**无向边**来表示节点和节点之间的**相互概率依赖**


#### 贝叶斯网络

贝叶斯网络满足**局部马尔可夫性**（local Markov property）：在给定一个节点的父节点的情况下，该父亲节点有条件地独立于它的非后代节点（non-descendant）

> [!NOTE]- 贝叶斯网络中所有因素的联合分布等于所有节点的 P (节点|父节点) 的乘积
> 例如，对于如下网络：
> ![Pasted image 20250604221344.png|450](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604221344.png)
> 我们有：
> $$\mathbb{P}(\text{多云、下雨、洒水车、路湿})==P (多云) P (洒水车|多云) P (下雨|多云) P (路湿|洒水车，下雨)$$
> 
> ![Pasted image 20250604221434.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604221434.png)


#### 马尔可夫逻辑网络

从概率统计的角度：
- 简明描述马尔可夫网中所存在的信息之间的关联
- 引入谓词逻辑，融入结构化知识

从一阶谓词逻辑角度：
- 添加不确定性 👉 对严格推理进行松绑

**马尔可夫逻辑网络是一种将概率图模型与一阶逻辑结合的工具**

给定一个由若干规则构成的集合，集合中每条推理规则赋予一定权重，则可如下计算某个断言 x 成立的概率:
$$P(X=x)=\frac{1}{Z}\exp\left(\sum_{i}w_{i}n_{i}(x)\right)=\frac{1}{Z}\prod_{i}\phi_{i}(x_{\{i\}})^{n_{i}(x)}$$
其中 $n_i (x)$ 是在推导 $x$ 中所涉及第 $i$ 条规则的逻辑取值 (为 1 或 0)、$w_i$ 是该规则对应的权重，$z$ 是一个固定的常量，可由下式计算：
$$Z=\sum_{x\in\mathcal{X}}\exp\left(\sum_iw_in_i(x)\right)$$

> [!EXAMPLE]- 马尔可夫逻辑网络的简要例子
> 
> ![Pasted image 20250604221731.png|375](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604221731.png)
> ![Pasted image 20250604221723.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604221723.png)
> ![Pasted image 20250604221741.png|475](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250604221741.png)

### 1.5 因果推理

#todo 

---

## 02 搜索探寻与问题求解

### 2.1 搜索算法基础

#### 形式化描述

状态、动作、状态转移、路径/代价、目标测试

![Pasted image 20250605094330.png|350](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605094330.png)
- 状态：对智能体和环境当前情形的描述
	- 在最短路径问题中，**每个城市即为一个状态**
	- 刚开始所在状态 (图中为 A ) 称为**初始状态**
	- 完成任务时所在的状态 (图中为 K ) 称为**终止状态**
- 动作：从当前时刻所处状态转移到下一时刻所处状态所进行操作
- 状态转移：智能体选择了一个动作之后，其所处状态的相应变化
	- 有边的两点之间才能转移
- 路径/代价：一个状态序列
	- 状态序列被一系列动作所连接，如从 A 到 K 所形成的路径
	- 单步代价：状态序列长度为 2
- 目标测试：评估当前状态是否为所求解的目标状态

我们用一棵树来记录算法探索过的路径
- 在搜索树中，同一个标号一定表示相同的状态
- 但是一个标号可能有多个的结点与之对应，即**不同的节点对应了从初始状态出发的不同路径**

搜索算法可以被看成是一个构建搜索树的过程，从**根结点**（初始状态）开始，不断展开每个结点的**后继结点**，直到某个结点通过了**目标测试**

搜索算法具备如下的评价指标：
- 完备性和最优性：解的质量、找到解的能力
- 时间复杂度和空间复杂度：算法的资源消耗

| 评价指标  |                                         |
| ----- | --------------------------------------- |
| 完备性   | 当问题存在解时，算法是否能保证找到一个解                    |
| 最优性   | 搜索算法是否能保证找到的第一个解是最优解                    |
| 时间复杂度 | 找到一个解所需时间<br>(通过拓展的节点数量来衡量)             |
| 空间复杂度 | 在算法的运行过程中需要消耗的内存量<br>(通过算法同时记录的节点数量来衡量) |

而在搜索树中，我们通常使用如下变量，估计复杂度：

| 符号 | 含义 |
| --- | --- |
| $b$ | 分支因子，即搜索树中每个节点最大的分支数目 |
| $d$ | 根节点到最浅的目标结点的路径长度 |
| $m$ | 搜索树中路径的最大可能长度 |
| $n$ | 状态空间中状态的数量 |



#### 搜索算法框架

##### 树搜索

边缘 (fringe) 集合: 集合ℱ用于保存搜索树中可用于下一步探索的所有候选结点，也叫做开表 (openlist)

> [!NOTE] TreeSearch
> - 输入：节点选择函数 (决定拓展顺序) pick_from，后继节点计算函数 (决定待拓展节点) successor_nodes
> - 输出：从初始状态到终止状态的路径
> ---
> - 算法流程
> 	- $\mathcal{F} \gets \{ \text{根节点} \}$
> 	- $\text{while } \mathcal{F} \neq \emptyset \text{ do}$
> 		- $\text{ } \text{ } n \gets \text{pick\_from}(\mathcal{F})$
> 		- $\text{ } \text{ } \mathcal{F} \gets \mathcal{F} - \{ n \}$
> 		- $\text{ } \text{ } \text{if } \text{goal\_test}(n) \text{ then}$
> 			- $\text{ } \text{ } \text{ } \text{ } \text{return } n.\text{path}$
> 		- $\text{ } \text{ } \text{end}$
> 		- $\text{ } \text{ } \mathcal{F} \gets \mathcal{F} \cup \text{successor\_nodes}(n)$
> 	- $\text{end}$


#### 剪枝搜索

树搜索算法存在问题：并不是其所有的后继节点都值得被探索
- 在某些情况下，主动放弃一些后继结点能够提高搜索效率而不会影响最终搜索结果，甚至能解决无限循环（即算法不停机）问题
![Pasted image 20250605100647.png|300](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605100647.png)

#### 图搜索

在图搜索策略下，在边缘集合中所有产生环路的节点都要被剪枝，但不会排除所有潜在的可行解。因此在状态数量有限情况下，采用图搜索策略的算法也是完备的

> [!NOTE] GraphSearch
> - 输入：节点选择函数 pick_from，后继节点计算函数 successor_nodes
> - 输出：从初始状态到终止状态的路径
> ---
> - 算法流程
> 	- $F\leftarrow\text{根节点}$
> 	- $\mathcal{C}\leftarrow\emptyset$  C 用于标记已经访问过的节点
> 	- while F ≠ $\emptyset$ do
> 		- n ← pick_from (F)
> 		- F ← F = {n}
> 		- if goal_test (n) then
> 			- return n.path
> 		- end
> 		- if n.state $\notin$ C then (**删除引起环路的节点**)
> 			- C ← C $\cup$ {n.state}
> 			- F ← F $\cup$ successor_nodes (n)
> 		- end
> 	- end

### 2.2 启发式搜索 (有信息搜索)

| 辅助信息                           | 所求解问题之外、与所求解问题相关的特定信息或知识。                     |              |
| ------------------------------ | --------------------------------------------- | ------------ |
| 评价函数（evaluation function）f (n) | 从当前节点 n 出发，根据评价函数来选择后续结点                      | 下一个结点是谁?     |
| 启发函数（heuristic function）h (n)  | 计算从结点 n 到目标结点之间所形成路径的最小代价值，这里将两点之间的直线距离作为启发函数 | 完成任务还需要多少代价? |

#### 贪婪最佳优先搜索

 评价函数 $f (n)$ =启发函数 $h (n)$

如下图所示
- $f(E)=h(E)=7$ 最小，选择 E
- $f(H)=3$ 最小，选择 H
- 以此类推...
![Pasted image 20250605113026.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605113026.png)

贪婪最佳优先搜索采用了**排除环路的剪枝算法**，但未考虑**从初始节点到达该节点所需的代价**


#### A\* 算法

$$\underbrace{{\boldsymbol{f(n)}}}_{{\text{评价函数}}}=\underbrace{{\boldsymbol{g(n)}}}_{{\text{起始结点到结点}\boldsymbol{n}\text{代价} (当前最小代价)}}+\underbrace{{\boldsymbol{h(n)}}}_{{\text{结点}\boldsymbol{n}\text{到目标结点代价}(后续估计最小代价)}}$$


![Pasted image 20250605113346.png|500](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605113346.png)

##### 性能分析

| 符号          | 含义                         |
| ----------- | -------------------------- |
| $h(n)$      | 节点 $n$ 的启发函数取值               |
| $g(n)$      | 从起始节点到节点 $n$ 所对应路径的实际代价      |
| $f(n)$      | 节点 $n$ 的评价函数取值               |
| $c(n,a,n')$ | 从节点 $n$ 执行动作 $a$ 到达节点 $n'$ 的单步代价 |
| $h^*(n)$    | 从节点 $n$ 出发到达终止节点的最小代价        |
一个良好的启发函数需要满足如下两种性质：
- 可容性 (admissible): 对于任意结点 $n$, 有 $h(n)\leq h^*(n)$, 如果 $n$ 是目标结点，则有 $h(n)=0$
	- $h^{*}(n)$ 是从结点 $n$ 出发到达终止结点所付出的（实际）最小代价
	- 即估计代价 ≤ 实际代价
- 一致性 (consistency): 启发函数的一致性指满足条件 $h(n)\leq c(n,a,n^{\prime})+h(n^{\prime})$
	- 三角不等式原则

> [!NOTE]- 满足一致性条件的启发函数一定满足可容性条件
> $$\begin{aligned}h(n_{1})&\leq h(n_{2})+c(n_{1},a_{1},n_{2})\\&\leq h(n_{3})+c(n_{2},a_{2},n_{3})+c(n_{1},a_{1},n_{2})\\&\leq\cdots\\&\leq c(n_{1},a_{1},n_{2})+c(n_{2},a_{2},n_{3})+\cdots+c(n_{t},a_{t},\mathrm{K})\\&=h^{*}(n_{1})\end{aligned}$$
> 
> 

> [!NOTE]- 完备性：如果在起始点和目标点间有路径解存在，那么一定可以得到解，如果得不到解那么一定说明没有解存在
> - 在一些常见的搜索问题中，状态数量是有限的，此时图搜索 A\*算法和排除环路的树搜索 A\*均是完备的，即一定能够找到一个解
> - 在更普遍的情况下，如果所求解问题和启发函数满足以下条件，则 A\*算法是完备的
> 	- 搜索树中分支数量是有限的，即每个节点的后继结点数量是有限的
> 	- 单步代价的下界是一个正数
> 	- 启发函数有下界

> [!NOTE]- 如果启发函数是可容的，那么树搜索的 A\*算法满足最优性
> 启发函数满足可容性时，假设树搜索的 A\*算法找到的第一个终止结点为 $n$
> 
> 对于此时边缘集合中任意结点 $n^\prime$, 根据算法每次扩展时的策略，即选择评价函数取值最小的边缘节点，有 $f(n)\leq f(n^\prime)$
> 
> 由于 A\*算法对评价函数定义为 $f(n)=g(n)+h(n)$, 且 $h(n)=0$, 有 $f(n)=g(n)$ + $h( n) = g( n)$ , $f( n^{\prime }) = g( n^{\prime }) + h( n^{\prime })$, 综合可得 $g( n) \leq$ $g( n^{\prime }) + h( n^{\prime })$ $\leq$ $g( n^{\prime })$ + $h^*(n^{\prime})$。(可容性：$h( n^\prime ) \leq h^* ( n^{\prime }) ;$ $g( n)$ 表示到终止节点的代价)
> 
> 此时扩展其他任何一个边缘结点都不可能找到比结点 $n$ 所对应路径代价更小的路径, 因此结点 $n$ 对应的是一条最短路径，即算法满足最优性

> [!NOTE]- 如果 A\*算法采用的是图搜索策略，那么即使启发函数满足可容性条件，也不能保证算法最优性
> 
> 最优性，对于任意一个状态𝑡，它第一次被加入搜索树时的路径必然是最短路径
> 
> 因为存在环路：如果有多个结点对应同一个状态 (即存在多条到达同一个城市的路径), 图搜索算法只会扩展其中的一个结点，而剪枝其余的结点
> 
> 解决方案
> - 方法 1：当算法从不同路径扩展同一结点时，不保留最先探索的那条路径，而是保留代价最小的那条路径
> - 方法 2：要求启发函数满足一致性
> 	- 由于图中存在环路，所以 $f(n)<=f(n^{\prime})$ 并不总是成立
> 	- 当启发函数满足一致性时，若结点𝑛′是结点𝑛的后继节点，则有 $f(n)<=f(n^{\prime})$ 成立
> 	- 假设状态𝑡加入搜索树时对应的结点为𝑛，在结点𝑛被加入搜索树后，若对应状态𝑡的任何结点𝑛′出现在边缘集合中，那么必然有𝑔(𝑛)≤𝑔(𝑛′)

### 2.3 对抗搜索

对抗搜索 (Adversarial Search) 也称为博弈搜索 (Game Search)

智能体 (agents) 之间通过竞争实现相反的利益，一方最大化这个利益，另外一方最小化这个利益：
![Pasted image 20250605121008.png|275](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605121008.png)


两人对决游戏 (MAX and MIN, MAX 先走) 可如下形式化描述：

| 形式化描述  |                                                                       |
| ------ | --------------------------------------------------------------------- |
| 状态     | 状态 s 包括当前的游戏局面和当前行动的智能体<br>函数 player (s) 给出状态 s 下行动的智能体               |
| 动作     | 给定状态 s，动作指的是 player (s) 在当前局面下可以采取的操作 a<br>记动作集合为 actions (s)         |
| 状态转移   | 给定状态 s 和动作 a∈actions (s)，状态转移函数 result (s, a) 决定了在 s 状态采取 a 动作后所得后继状态 |
| 终局状态检测 | 终止状态检测函数 terminal_test (s) 用于测试游戏是否在状态 s 结束。                          |
| 终局得分   | 终局得分 utility (s, p) 表示在终局状态 s 时玩家 p 的得分。                              |

本次讨论中，主要讨论在**确定的、全局可观察的、竞争对手轮流行动、零和游戏（zero-sum）**下的对抗搜索

#### 最小最大搜索 (Minimax Search)

> [!tip] 看 Alpha-Beat 剪枝的例子理解即可


![Pasted image 20250605130032.png|450](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605130032.png)
![Pasted image 20250605131208.png|275](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605131208.png)


给定一个游戏搜索树，minimax 算法通过每个节点的 minimax 值来决定最优策略
- MAX 希望最大化 minimax 值，
- MIN 则相反
$$minimax(s)=\begin{cases}\text{utility}(s),\text{if terminal\_test(s)}\\\max_{a\in\text{actions}(s)}\text{minimax}(\text{result}(s,a)),\text{if player(s)=MAX}\\\min_{a\in\text{actions}(s)}\text{minimax}(\text{result}(s,a)),\text{if player(s)=MIN}&\end{cases}$$

#### 性能分析

- 完备性: Yes (if the tree is finite)
- **最优性**: Yes (against an optimal opponent)
- 时间复杂度: $O (b^m)$
	- Depth-first exploration
	  执行了一个完整的深度优先搜索
- 空间复杂度: $O (bm)$
	- Depth-first exploration

#### Alpha-Beta 剪枝搜索 (Pruning Search)

Alpha-Beta 剪枝搜索算法在 Minimax 算法中可减少被搜索的结点数，即在保证得到与原 Minimax 算法同样的搜索结果时，剪去了不影响最终结果的搜索分枝

![Pasted image 20250605131541.png|450](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605131541.png)

##### Alpha 剪枝

- 假设有一个位于 MIN 层的结点 $m$, 已知该结点能够向其上 MAX 结点反馈的收益为 $\alpha$
- $n$ 是与结点 $m$ 位于同一层的某个兄弟 (sibling) 结点的后代结点
- 如果在结点 $n$ 的后代结点被访问一部分后，知道结点 $n$ 能够向其上一层 MAX 结点反馈**收益小于 $\alpha$**, 则结点 $n$ 的**未被访问孩子结点将被剪枝**

![Pasted image 20250605131815.png|300](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605131815.png)

##### Beta 剪枝

- 考虑位于 MAX 层的结点 $m$, 已知结果点 $m$ 能够从其下 MIN 层结点收到的收益为 $\beta$ 
- 结点 $n$ 是结点 $m$ 上层结点 $m^{\prime}$ 的位于 MAX 层的后代结果点
- 如果目前已知结点 $n$ 能够收到的**收益大于 $\beta$**, 则不再扩展结点 $n$ 的**未被访问后继结点**，因为位于 MIN 层的结点 $m^{\prime}$ 只会选择收益小于或等于 $\beta$ 的结点来采取行动

![Pasted image 20250605132043.png|300](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605132043.png)

#### 算法流程

> [!NOTE] Pseudo Code
> 1. 根结点（MAX 结点）的𝛼值和𝛽值分别被初始化为−∞和+∞
> 2. 子节点继承父节点的𝛼值和𝛽值，再按照以下规则进行更新
> 	1. 对于 MAX 节点，如果其孩子结点（MIN 结点）的收益大于当前的𝛼值（极大层的下界），则将𝛼值更新为该收益
> 	2. 对于 MIN 结点，如果其孩子结点（MAX 结点）的收益小于当前的𝛽值（极小层的上界），则将𝛽值更新为该收益
> 3. 如果一个结点的𝛼值和𝛽值满足𝛼>𝛽的条件，则该结点尚未被访问的后续结点就可以被剪枝

> [!example]- 搞懂例子就可以了
> 原本 Minimax 搜索树中有 26 个结点，经过 alpha-beta 剪枝后只扩展（访问）了其中 15 个结点，可见 alpha-beta 剪枝技术能够有效地减少搜索树中结点的数目
> ![Pasted image 20250605132604.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605132604.png)
> ![Pasted image 20250605132613.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605132613.png)
> ![Pasted image 20250605132620.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605132620.png)
> ![Pasted image 20250605132624.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605132624.png)


### 2.4 蒙特卡洛搜索

#### 引入：多臂赌博机问题

问题描述：
- 假设智能体面前有𝑲个赌博机，每个赌博机有一个臂膀
- 每次转动一个赌博机臂膀，随机吐出一些硬币或不吐出硬币，将所吐出的硬币的币值用收益分数来表示
- 现在假设给智能体 𝝉 (𝛕 > 𝐊) 次转动臂膀的机会
- 智能体如何选择赌博机、转动 𝝉 次赌博机臂膀，能够获得更多的收益分数

形式化分析
- 状态：每个被摇动的臂膀即为一个状态，记 $K$ 个状态分别为 $\{s_1, s_2,\cdotp\cdotp\cdotp, s_K\}$, 没有摇动任何臂膀的初始状态记为 $s_0$
- 动作: 动作对应着摇动一个赌博机的臂膀，在多臂赌博机问题中，任意状态下的动作集合都为 $\{a_1, a_2$ ..., $a_K\}$
- 状态转移：选择动作 $a_i (1\leq i\leq K)$ 后，将相应的改变为 $s_i$
- 奖励 (reward) 
	- 假设从第 $i$ 个赌博机获得收益分数的分布为 $D_i$, 其均值为 $\mu_i$
	- 如果智能体在第 $t$ 次行动中选择转动了第 $l_t$ 个赌博机臂膀，那么智能体在第 $t$ 次行动中所得收益分数 $\hat{r}_t$ 服从分布 $D_{l_t},\hat{r}_t$ 被称为第 $t$ 次行动的奖励
	- 一般假定奖励是有界的，进一步可假设奖励的取值范围为\[0,1\]
- 悔值 (regret) 函数。根据智能体前 $T$ 次动作，可以如下定义悔值函数：
	$$\rho_T=T\mu^*-\sum_{t=1}^T\hat{r}_t\quad (3.4.1)$$
	其中 $\mu^*=\max_{\mathrm{i}\equiv 1....\mathrm{K}}\mu_i$。


因此，问题求解的目标为最小化悔值函数的期望，该悔值函数的取值取决于智能体所采取的策略

**智能体不能预先计算好最优策略，然后实行，而是需要一边探索一边调整自己的策略，争取获得更好的收益**

##### 贪心算法策略

贪心算法策略如下：
- 给定第 $i (1\leq i\leq K)$ 个赌博机，记在过去 $t-1$ 次摇动赌博机臂膀的行动中，一共摇动第 $i$ 个赌博机臂膀的次数为第 $T_{(i, t-1)}$
- 第 $i$ 个赌博机在过去 $T_{(i, t-1)}$ 次被摇动过程中的收益分数平均值 $\bar{x}_{i, T_{(i, t-1)}}$
- 在第 $t$ 步，只要选择 $\bar{x}_{i, T_{(i, t-1)}}$ 值最大的赌博机臂膀进行摇动

不足：忽略了其他从未摇动或很少摇动的赌博机，而失去了可能的机会 👇 **探索与利用结合**

𝝐-贪心算法
$$l_t=\begin{cases}\quad\mathrm{argmax}_i\:\bar{x}_{i,T_{(i,t-1)}},以1-\epsilon的概率\\\text{随机的}i\in\{1,2,\cdots,K\},以\epsilon的概率&\end{cases}$$

不足：与被探索的次数无关 👉 需要**对那些探索次数少或几乎没有被探索过的动作赋予更高的优先级**

##### 上限置信区间算法（Upper Confidence Bounds, UCB 1）

在第 $t$ 次时选择使得如下式子取值最大的动作 $a_{l_t}$：
$$l_t=\operatorname{argmax}_i\bar{x}_{i,T_{(i,t-1)}}+C\sqrt{\frac{2\ln t}{T_{(i,t-1)}}}$$
**优先采用探索估计值不确定度高的动作**

#### 算法流程

如何高效地拓展搜索树：
- **优先拓展哪些节点**
- **放弃拓展哪些节点**

目标降低，改为求解一个近似最优解：
- 每一步动作为**选择**(在非叶子节点) 或**拓展**(在叶子节点) 一个孩子节点
- 通过**采样式探索来得到计算奖励的样本**



> [!NOTE] Pseudo Code
> - 选择 (selection)
> 	- 算法从搜索树的根节点开始，向下递归选择子节点，直至到达叶子节点或者到达具有还未被扩展过的子节点的节点 L
> 	- 这个向下递归选择过程可由 UCB 1 算法来实现，在递归选择过程中记录下每个节点被选择次数和每个节点得到的奖励均值
> - 扩展 (expansion)
> 	- 如果节点 L 不是一个终止节点 (或对抗搜索的终局节点), 则随机扩展它的一个未被扩展过的后继边缘节点 M
> - 模拟 (simulation)
> 	- 从节点 M 出发，模拟扩展搜索树，直到找到一个终止节点
> 	- 模拟过程使用的策略和采用 UCB 1 算法实现的选择过程并不相同
> 		- 模拟过程通常会使用比较简单的策略，例如使用**随机策略**
> - 反向传播 (Back Propagation)
> 	- 用模拟所得结果 (终止节点的代价或游戏终局分数) 回溯更新模拟路径中 M 以上 (含 M) 节点的奖励均值和被访问次数

> [!example]- 能看懂例子就可以了
> 
> ![Pasted image 20250605142632.png|450](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250605142632.png)
> 
> 选择阶段
> - 计算第二层节点的 UCB 值：左侧结点为 $\frac{10}{1}+\sqrt{\frac{2\ln 2}{1}}=11.18$, 右侧结点为 $\frac 51+$ $\sqrt{\frac{2\ln 2}{1}}=6.18$
> - 因此算法选择第二层左侧的结点 L，由于该节点有尚未扩展的子结点，因此选择阶段结束
> 
> 拓展阶段
> - 在图 3.25 (b) 中，算法随机扩展了 L 的子结点 C，将其总分数和被访问次数均初始化为 0
> - 图 3.25 (b) 画出了 L 的其他未被扩展的子结点，并标记其 UCB 值为正无穷
> 	- 表示算法下次访问到 L 时必然扩展这些未被扩展的结点
> 
> 模拟阶段
> - 采用随机策略模拟游戏直至完成游戏。当游戏完成时，终局得分为 3
> 
> 反向传播阶段
> - 更新策略为：MIN 层结点现有总分加上终局得分分数，MAX 层结点现有总分减去终局得分分数
> - 在图 (d) 中
> 	- C 结点的总分被更新为-3，被访问次数被更新为 1
> 	- L 结点的总分被更新为 13，被访问次数被更新为 2
> 	- 根结点的总分被更新为-18，被访问次数被更新为 3

---
## 03 机器学习

### 3.1 机器学习基本概念

通过对数据的优化学习，**建立能够刻画数据中所蕴含语义概念或分布结构等信息的模型**

数据利用的角度分类：
- 监督学习
- 无监督学习
- 半监督学习

#### 监督学习

监督学习：带有**标签**信息数据的训练集
- 从假设空间学习得到一个**最优映射函数 f (决策函数)**

数据集可分为：
- 训练集：模型训练 👉 学生的练习册
- 验证集：评估模型，调整参数 👉 模拟考
- 测试集：得到模型的优劣水平 👉 真正考试


> [!tip] 没有免费午餐定理
> 任何一个机器学习模型如果在一些训练集以外的样本上误差小（off-training set error），那么必然在另外一些训练集以外的样本上表现欠佳，任何模型在平均意义上而言其性能都是一样的，即没有放之四海而皆准的最好算法
> 
> 实践经验：在机器学习中合理引入已有先验假设对模型进行约束，以提升模型效果

泛化能力
- 模型在训练集上的性能和测试集一致

**在训练过程中，映射函数 f（学习模型）的主要目标是最小化整个训练数据集上的累积“损失”。** 这可以表示为：
$$min∑_{i=1}^n​Loss(f(x_i​),y_i​)$$



经验风险 empirical risk 与期望风险 expected risk
- 经验风险是训练集中数据产生的损失
- 期望风险是当测试集中存在**无穷多**数据时产生的损失
![Pasted image 20250529174836.png|450](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250529174836.png)

期望风险（即真实风险）$\mathfrak{R}$ 与经验风险 $\mathfrak{R}_{emp}$ 之间是有差别的，这个差别项被称为**置信风险**
- err 与训练样本个数和模型复杂度都有密切的关系


“过学习 (over-fitting)”与“欠学习 (under-fitting)”
- Over-fitting：经验风险小而期望风险大
- Under-fitting：经验风险大且期望风险大

结构风险最小化 structural risk minimization
- 经验风险最小化：仅反映了局部数据 
- 期望风险最小化：无法得到全量数据
- 为了防止过拟合，在经验风险上加上表示模型复杂度的**正则化项** (regulatizer) 或惩罚项 (penalty term ) 
	在最小化经验风险与降低模型复杂度之间寻找平衡
$$\min_{f\in\Phi}\frac1n\sum_{i=1}^nLoss(y_i,f(x_i))+\lambda J(f)$$

#### 模型度量方法

以二分类问题为例：n 为训练样例总数，正例为 P，负例为 N；
TP 真正例 👉 模型预测为正，实际为正
FP 假正例 👉 模型预测为正，实际为负
TN 真负例 👉 模型预测为负，实际为负
FN 假负例 👉 模型预测为负，实际为正
- 准确性 (accuracy): $ACC = \frac{TP+TN}{P+N}$
	- 很显然，如果正负样本比例不平衡，ACC 不是一个度量模型好的方法。比如，某一种恶性疾病很罕见（如 1 万个疑似患者中仅有 1 人罹患该疾病），机器学习模型可将所有患者均识别为负类，从而保证 ACC 取值极高，但这就忽略了这一模型应该关注的问题。
- 错误率 (error rate): $errorRate = \frac{FP+FN}{P+N}$
	- 显然有 $errorRate = 1 - ACC$
- 精确率 (precision): $precision = \frac{TP}{TP+FP}$
	- 也叫查准率，表示被模型预测为正例的样本中实际为正例的比例
- 召回率 (Recall): $recall = \frac{TP}{TP+FN}$
	- 也叫查全率，表示所有正例样本中被模型预测为正例的比例

在实际应用中，精确率和召回率之间是相互矛盾的，比如可以将所有样本分类为正例使得召回率为 100%而精确率极低。因此为了综合考虑精确率和召回率，可采用综合分类率 F1-score：

$$综合分类率（F1-score）= \frac{2}{\frac{1}{Precision}+\frac{1}{Recall}}=2\times\frac{Precision\times Recall}{Precision+Recall}$$

F1-score 是精确率和召回率的调和平均数，在尽可能提高精确率和召回率同时，也希望两者之间的差异尽可能小

### 3.2 回归分析

分析不同变量之间存在关系的研究叫回归分析，刻画不同变量之间关系的模型被称为回归模型

![Pasted image 20250520100548.png|375](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250520100548.png)

#### 一元线性回归

回归模型参数求取: $y_{i} = ax_{i} + b \ (1 \leq i \leq n)$

- 记在当前参数下第 $i$ 个训练样本 $x_{i}$ 的预测值为 $\widehat{y}_{i}$
- $x_{i}$ 的标注值（实际值）$y_{i}$ 与预测值 $\widehat{y}_{i}$ 之差记为 $(y_{i} - \widehat{y}_{i})^{2}$
- 训练集中 $n$ 个样本所产生误差总和为: $L(a, b) = \sum_{i=1}^{n}(y_{i} - a \times x_{i} - b)^{2}$

目标: 寻找一组 $a$ 和 $b$，使得误差总和 $L(a, b)$ 值最小。在线性回归中，解决如此目标的方法叫最小二乘法
- 一般而言，要使函数具有最小值，可对 $L(a, b)$ 参数 $a$ 和 $b$ 分别求导，令其导数值为零，再求取参数 $a$ 和 $b$ 的取值

#### 多元线性回归

多维数据特征中线性回归的问题定义如下：假设总共有 $m$ 个训练数据 $\{(x_i,y_i)\}_{i=1}^m$, 其中 $x_i=[x_{i,1},x_{i,2},...,x_{i,D}]\in\mathbb{R}^D$, $D$ 为数据特征的维度，线性回归就是要找到一组参数 $a=[a_0,a_1,...,a_D]$, 使得线性函数：
$$f(x_i)=a_0+\sum_{j=1}^Da_j\:x_{i,j}=a_0+a^Tx_i$$
最小化均方误差函数:
$$J_{m}=\frac{1}{m} \sum_{i=1}^{m}\left(y_{i}-f\left(x_{i}\right)\right)^{2}$$
为了方便，使用矩阵来表示所有的训练数据和数据标签。
$$
X=\left[x_{1}, \ldots, x_{m}\right], \quad \quad y=\left[y_{1}, \ldots, y_{m}\right]$$
其中每一个数据 $x_{i}$ 会扩展一个维度，其值为 1，对应参数 $a_{0}$

> [!NOTE]- 均方误差函数
> 均方误差函数可以表示为:
> $$J_{m}(\boldsymbol{a})=(\boldsymbol{y}-X^{T} \boldsymbol{a})^{T}(\boldsymbol{y}-X^{T} \boldsymbol{a})$$
> 均方误差函数 $J_{n}(\boldsymbol{a})$ 对所有参数 $\boldsymbol{a}$ 求导可得:
> $$
> \nabla J(\boldsymbol{a})=-2 X(\boldsymbol{y}-X^{T} \boldsymbol{a})$$
> 因为均方误差函数 $J_{n}(\boldsymbol{a})$ 是一个二次的凸函数，所以函数只存在一个极小值点，也同样是最小值点，所以令 $\nabla J(\boldsymbol{a})=0$ 可得
> $$X X^{T} \boldsymbol{a}=X \boldsymbol{y}$$
> $$
> \boldsymbol{a}=\left(X X^{T}\right)^{-1} X \boldsymbol{y}$$
> 


#### 逻辑斯蒂回归/对数几率回归

线性回归一个明显的问题是对**离群点**非常敏感，导致模型建模不稳定，使结果有偏

逻辑斯蒂回归 (logistic regression) 就是在回归模型中引入 sigmoid 函数的一种非线性回归模型。Logistic 回归模型可如下表示：
$$y=\frac1{1+e^{-z}}=\frac1{1+e^{-(w^Tx+b)}}\quad,\quad\text{其中}y\in(0,1),z=w^Tx+b$$

这里 $\frac1{1+e^{-z}}$ 是 sigmoid 函数、$x\in\mathbb{R}^d$ 是输入数据、$w\in\mathbb{R}^d$ 和 $b\in\mathbb{R}$ 是回归函数的参数

![Pasted image 20250523130546.png|227](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250523130546.png)


logistic 回归只能用于解决二分类问题，将它推广为多项逻辑斯蒂回归模型 (multi-nominal
logistic model, 即 **softmax 函数**), 用于处理多类分类问题，可以得到处理多类分类问题的 softmax 回归

### 3.3 决策树

- 非叶子节点：对分类目标某一属性的判断
- 叶子节点：分类结果

![Pasted image 20250409094237.png|450](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250409094237.png)

**建立决策树的过程，就是不断选择属性值对样本集进行划分，直至每个子样本为同一个类别**

构建决策树时划分属性的顺序选择是重要的。性能好的决策树随着划分不断进行，决策树分支结点样本集的“纯度”会越来越高，即其所包含样本尽可能属于相同类别

#### 信息增益

信息熵（entropy）是度量**样本集合纯度**最常用的一种指标：如果我们计算选择不同属性划分后样本集的“纯度”, 那么就可以比较和选择属性。信息熵越大，说明该集合的不确定性越大，“纯度”越低

假设有 $K$ 个信息 (类别), 其组成了集合样本 $D$, 记第 $k$ 个信息 (类别) 发生的概率为 $p_k (1\leq k\leq K)$。如下定义这 $K$ 个信息的信息熵：
$$Ent(D)=-\sum_{k=1}^Kp_k\log_2p_k$$
- $Ent (D)$ 值越小，表示 $D$ 包含的信息越确定，也称 $D$ 的纯度越高
- 所有 $p_k$ 累加起来的和为 1
- 约定：若 $p_k=0$, 则 $p_k\log_2 p_k=0$

选择属性划分样本集前后**信息熵的减少量**被称为**信息增益** (information gain), 也就是说信息增益被用来衡量样本集合复杂度 (不确定性) 所减少的程度

信息增益的计算：
$$Gain(D,A)=Ent(D)-\sum_{i=1}^n\frac{|D_i|}{|D|}Ent(D_i)$$

- 通过**比较样本的属性信息增益的高低来选择最佳属性**（信息增益最大的属性）对原样本集进行划分，得到最大的“纯度”
- 如果划分后的不同子样本集都只存在同类样本 (类别标签一致)，那么停止划分

> [!example]-
> ![Pasted image 20250613224652.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250613224652.png)
> ![Pasted image 20250613224717.png](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250613224717.png)


> [!NOTE] 一般而言，信息增益偏向选择分支多的属性 (比如年龄), 这在一些场合容易导致模型过拟合

#### 信息增益率和基尼系数

信息增益率：新的指标 👉 对分支过多进行惩罚

Info 和 Gain-ratio（增益率）计算公式如下：
$$info = -\sum_{i=1}^{n}{\frac{|D_i|}{|D|}\log_2{\frac{|D_i|}{|D|}}}$$

$$Gain-ratio = Gain(D,A)/info$$



> [!NOTE] 增益率准则对可取数目较少的属性有所偏好

一个启发式：
- 先从候选划分属性中找出信息增益高于平均水平的属性
- 再从中选取增益率最高的

更简的度量指标是如下的 Gini 指数（基尼指数）：
$$Gini(D) = 1 - \sum_{k=1}^{K} p_k^2$$
- 相对于信息熵的计算 $E (D) = -\sum_{k=1}^{K} p_k \log_2 p_k$，不用计算对数 log，计算更为简易


### 3.4 K-means



- 若干定义:
	- n 个 m-维数据 $\{x_{1},x_{2},...,x_{n}\}$，$x_{i}\in R^{m}$ (1≤i≤n)
	- 两个 m 维数据之间的欧氏距离为
		$$d(x_{i},x_{j})=\sqrt{(x_{i1}-x_{j1})^{2}+(x_{i2}-x_{j2})^{2}+...+(x_{im}-x_{jm})^{2}}$$
		$d(x_{i},x_{j})$ 值越小，表示 $x_{i}$ 和 $x_{j}$ 越相似；反之越不相似
- 聚类集合数目 k
- 问题: 如何将 n 个数据依据其相似度大小将它们分别聚类到 k 个集合，使得每个数据仅属于一个聚类集合

#### 算法流程

- 初始化聚类质心
	- 初始化 $k$ 个聚类质心 $c=\{c_1,c_2,...,c_k\},c_j\in R^m(1\leq j\leq k)$
	- 每个聚类质心 $c_j$ 所在集合记为 $G_j$
- 将每个待聚类的数据放入唯一一个聚类集合中
	- 计算待聚类数据 $\chi_i$ 和质心 $c_j$ 之间的欧氏距离 $d\left(x_i,c_j\right)(1\leq i\leq n,1\leq j\leq k)$
	- 将每个 $x_i$ 放入与之距离最近聚类质心所在聚类集合中，即 $\underset{c\in C}{\operatorname*{\operatorname*{argmin}}}d(x_i,c_j)$
- 更新聚类质心
	- 根据每个聚类集合中所包含的数据，更新该聚类集合质心值，即：$c_j=\frac1{|G_j|}\sum_{x_i\in G_j}x_i$
- 算法迭代，直至满足条件
	- 迭代次数上限
	- 质心基本不变

聚类算法的目标都是得到一个聚类结果，最小化类内距离（或最大化类内相似度），而最大化类间距离（或最小化类间相似度）

$k$ -means 聚类就是通过**最小化聚簇内的数据方差**来实现**最大化类内相似度**的，即最小化每个类簇方差，
使得最终聚类结果中每个聚类集合所包含的数据呈现出的差异性最小


### 3.5 监督学习与非监督学习下的特征降维

#### 线性判别分析

线性判别分析 (linear discriminant analysis， LDA)
也称为 Fisher 线性判别分析（fisher'sdiscriminant analysis，FDA) \[Fisher 1936\]

在低维空间中同一类别样本尽可能靠近，不同类别样本尽可能彼此远离

![Pasted image 20250409104720.png|425](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250409104720.png)

符号定义：
- 样本集为 $D = {(x₁, y₁), (x₂, y₂), (x₃, y₃), ..., (xₙ, yₙ)}$
- 样本 $x_i ∈ ℝ^d$ 的类别标签为 $y_i$
- $y_i$ 的取值范围是 ${C₁, C₂, ..., C_K}$，即一共有 K 类样本

定义 X 为所有样本构成集合、$N_i$ 为第 i 个类别所包含样本个数、$X_i$ 为第 i 类样本的集合、m 为所有样本的均值向量、$m_i$ 为第 i 类样本的均值向量。$Σ_i$ 为第 i 类样本的协方差矩阵，其定义为：

$$Σ_i = \sum_{x ∈ X_i} (x - m_i)(x - m_i)^T$$
$$
\Sigma_i = \sum_{x \in X_i}
\begin{pmatrix}
(x_1 - m_{i1})^2 & (x_1 - m_{i1})(x_2 - m_{i2}) & \dots & (x_1 - m_{i1})(x_d - m_{id}) \\
(x_2 - m_{i2})(x_1 - m_{i1}) & (x_2 - m_{i2})^2 & \dots & (x_2 - m_{i2})(x_d - m_{id}) \\
\vdots & \vdots & \ddots & \vdots \\
(x_d - m_{id})(x_1 - m_{i1}) & (x_d - m_{id})(x_2 - m_{i2}) & \dots & (x_d - m_{id})^2
\end{pmatrix}$$
- 协方差矩阵，衡量的是原始 $x=(x_1, x_2,..., x_d)$ 各个维度 $x_1,..., x_d$ 之间的关联性

我们考虑二分类问题，即 K = 2 的情况

在二分类问题中，训练样本归属于 $C_1$ 或 $C_2$ 两个类别，并通过如下的线性函数投影到一维空间上：
$$y(x)=w^Tx\:(w\in\mathbb{R}^d)$$
- 通过一个 d 维的参数，将原始数据 x 降到一维空间

投影之后类别 $\mathcal{C}_1$ 的协方差矩阵 $s_1$ 为：
$$s_1=\sum_{x\in\mathcal{C}_1}\left(w^Tx-w^Tm_1\right)^2=w^T\sum_{x\in\mathcal{C}_1}[(x-m_1)(x-m_1)^T]w$$
- 为了使得归属于同一类别的样本数据在投影后的空间中尽可能靠近，需要最小化 s1+s2 取值（类内方差小）
- 为了使得归属于不同类别的样本数据在投影后空间中尽可能彼此远离，需要最大化过 $\|m_2-m_1\|_2^2$ 取值 (类间间隔大)

同时考虑上面两点，就得到了需要最大化的目标 $J (w)$, 定义如下：
$$J(w)=\frac{\|m_2-m_1\|_2^2}{s_1+s_2}$$

$$J(\mathbf{w}) = \frac{\left\|\mathbf{w}^T (\mathbf{m}_2 - \mathbf{m}_1)\right\|^2}{\mathbf{w}^T \Sigma_1 \mathbf{w} + \mathbf{w}^T \Sigma_2 \mathbf{w}} = \frac{\mathbf{w}^T (\mathbf{m}_2 - \mathbf{m}_1) (\mathbf{m}_2 - \mathbf{m}_1)^T \mathbf{w}}{\mathbf{w}^T (\Sigma_1 + \Sigma_2) \mathbf{w}} = \frac{\mathbf{w}^T \mathbf{S}_b \mathbf{w}}{\mathbf{w}^T \mathbf{S}_w \mathbf{w}}$$
- $\mathbf{S}_b$ 称为**类间散度矩阵** (between-class scatter matrix)，衡量**两个类别均值点之间的“分离”程度**，可定义如下：
$$
\mathbf{S}_b = (\mathbf{m}_2 - \mathbf{m}_1) (\mathbf{m}_2 - \mathbf{m}_1)^T$$
- $\mathbf{S}_w$ 则称为**类内散度矩阵** (within-class scatter matrix)，衡量**每个类别中数据点的“分离”程度**，可定义如下：
$$\mathbf{S}_w = \Sigma_1 + \Sigma_2$$

> [!tip]- 矩阵求导
> - [机器学习中的数学理论1：三步搞定矩阵求导 - 知乎](https://zhuanlan.zhihu.com/p/262751195)
> - [矩阵求导法则与性质 · Convex Optimization](https://zealscott.com/notes/convexoptimization/matrix.html)
> 
> 向量化矩阵：按列将矩阵表示为向量，展开

> [!tip]- 如何求解 $J (w)$ ？
> 由于 $J (\mathbf{w})$ 的分子和分母都是关于 $\mathbf{w}$ 的二项式，因此最后的解只与 $\mathbf{w}$ 的方向有关，与 $\mathbf{w}$ 的长度无关，因此可令分母 $\mathbf{w}^T \mathbf{S}_w \mathbf{w} = 1$，然后用拉格朗日乘子法来求解这个问题。
> 
> 对应拉格朗日函数为:
> $$L (\mathbf{w}) = \mathbf{w}^T \mathbf{S}_b \mathbf{w} - \lambda (\mathbf{w}^T \mathbf{S}_w \mathbf{w} - 1)$$
> $$
> 2 \mathbf{S}_b \mathbf{w} = 2 \lambda \mathbf{S}_w \mathbf{w} \quad \Rightarrow \quad \mathbf{S}_w^{-1} \mathbf{S}_b \mathbf{w} = \lambda \mathbf{w}$$
> 对 $\mathbf{w}$ 求偏导并使其求导结果为零，可得 $\mathbf{S}_w^{-1} \mathbf{S}_b \mathbf{w} = \lambda \mathbf{w}$。由此可见，$\lambda$ 和 $\mathbf{w}$ 分别是 $\mathbf{S}_w^{-1} \mathbf{S}_b$ 的特征根和特征向量， $\mathbf{S}_w^{-1} \mathbf{S}_b \mathbf{w} = \lambda \mathbf{w}$ 也被称为 Fisher 线性判别（Fisher linear discrimination）。
> 因为 $\mathbf{S}_b \mathbf{w} = (\mathbf{m}_2 - \mathbf{m}_1)(\mathbf{m}_2 - \mathbf{m}_1)^T \mathbf{w}$，其中 $(\mathbf{m}_2 - \mathbf{m}_1)^T \mathbf{w}$ 是个实数，不妨令 $(\mathbf{m}_2 - \mathbf{m}_1)^T \mathbf{w} = \lambda_w$，则:
> $$\mathbf{S}_w^{-1} \mathbf{S}_b \mathbf{w} = \mathbf{S}_w^{-1} (\mathbf{m}_2 - \mathbf{m}_1) \times \lambda_w = \lambda \mathbf{w}$$
> 由于对 $\mathbf{w}$ 的放大和缩小操作不影响结果，因此可约去上式中的未知数 $\lambda$ 和 $\lambda_w$，得到: $\mathbf{w} = \mathbf{S}_w^{-1} (\mathbf{m}_2 - \mathbf{m}_1)$
> $\mathbf{w} \propto \mathbf{S}_w^{-1} (\mathbf{m}_2 - \mathbf{m}_1)$
> 
> 

为了获得“类内汇聚、类间间隔”的最佳投影结果，只需要分别**求出待投影数据的均值和方差**，就可以设**计得到最佳投影方向 $w$**, 这就是线性判别分析的做法
**将原始数据通过 $w^Tx$ 进行投影，实现了从高维到低维的映射**，因此也是一种降维操作，实现了数据约减，且这一降维结果保持了样本数据的“类内汇聚、类间间隔”结构分布


令投影矩阵 $W=(w_1,w_2,...,w_r)$, 可知 $W$ 是一个 $d\times r$ 矩阵
- 给定原始 $d$ 维空间中的数据样本 $x_i$, 通过 $x_iW$ 将其从 $d$ 维空间映射到 $r$ 维空间
- 在后续分类等操作中，只是使用 $x_i$ 降维后的结果，而不是 $x_i$ 的原始特征

降维步骤
1. 计算数据样本集中每个类别样本的均值
2. 计算类内散度矩阵 $S_w$ 和类间散度矩阵 $S_b$
3. 根据 $S_w^{-1}S_bW=\lambda W$ 来求解 $S_w^{-1}S_b$ 所对应前 $r$ 个最大特征值所对应特征向量 $(w_1, w_2,..., w_r)$，构成矩阵 $W$
4. 通过矩阵 $W$ 将每个样本映射到低维空间，实现特征降维


> [!NOTE]
> 通过 LDA 对原始 d 维数据进行降维后，所得维度 r 最大取值为 $min\{K-1, d\}$
> - 因为 $S_b$ 的秩为 $min\{K-1, d\}$
> - 说明二分类问题中，原始高维数据只能被投影到一维空间中

#### 主成分分析

也叫 KL 变换，霍林特变换、本征正交分解

**最大限度保持原始高维数据的总体方差结构**

> [!tip]- 皮尔逊相关系数
> - 协方差
> 	- 对象：n 个 2 维变量数据 $(X,Y)=\{(x_i,y_i)\}$
> 	- 衡量两个变量之间的相关度
> 		$$\mathrm{cov(X,Y)}=\frac1n\sum_{i=1}^n(x_i-E(X))(y_i-E(Y))$$
> - Pearson Correlation coefficient
> 	- 将两组变量的关联度规整到一定的范围内
> 		$$\mathrm{corr}(\mathrm{X},\mathrm{Y})=\frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}=\frac{Cov(X,Y)}{\sigma_x\sigma_y}$$
> 	- 性质：
> 		- $|corr(X,Y)|\leq1$
> 		- **$|corr(X,Y)|=1$ 的充要条件是存在常数 $a$ 和 $b$, 使得 $Y=aX+b$** 
> 		- 皮尔逊相关系数是对称的，即 corr $(X,Y)=corr(Y,X)$
> 	- 作用：刻画两个变量之间的线性相关度
> 		- **如果 $|corr(X,Y)|$ 的取值越大，则两者在线性相关的意义下相关程度越大**
> 		- $|corr(X,Y)|=0$ 表示两者不存在线性相关关系 (可能存在其他非线性相关的关系)
> - 相关性 correlation 与独立性 independence
> 	- 如果 X 和 Y 的线性不相关，则 $|corr(X,Y)|=0$
> 	- 如果 $X$ 和 $Y$ 的彼此独立，则一定 $|corr(X,Y)|=0$, 且 $X$ 和 Y 不存在任何线性或非线性关系
> 	- **“线性无关” 比 “独立” 弱**

主成分分析：特征降维的方法，但要保证降维后的结果要保持原始数据固有结构
- 需要尽可能将数据**向方差最大方向进行投影**，使得数据所蕴含信息没有丢失，彰显个性
- 将𝒅维特征数据映射到𝒍维空间（𝒅≫𝒍），去除原始数据之间的冗余性（通过去除相关性手段达到这一目的）
- 将原始数据向这些数据方差最大的方向进行投影。一旦发现了方差最大的投影方向，则继续寻找保持方差第二的方向且进行投影（保证方向的正交性）
![Pasted image 20250415120341.png|400](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250415120341.png)

|          | 线性判别分析                                       | 主成分分析                      |
| -------- | -------------------------------------------- | -------------------------- |
| 是否需要样本标签 | 监督学习                                         | 无监督学习                      |
| 降维方法     | 优化寻找特征向量 $\mathbf{w}$                         | 优化寻找特征向量 $\mathbf{w}$       |
| 目标       | 类内方差小、类间距离大                                  | 寻找投影后数据之间方差最大的投影方向         |
| 维度       | LDA 降维后所得到维度是与数据样本的类别个数 $K$ 有关 ($S_b$ 的秩最多为 K-1) | PCA 对高维数据降维后的维数是与原始数据特征维度相关 |

> [!NOTE] Pseudo-Code
> - 输入：n 个 d 维样本数据所构成的矩阵 X，降维后的维数为 l
> - 输出：映射矩阵 $W = \{w_1,w_2,...,w_l\}$
> ---
> 1. 对于每个样本数据 $\boldsymbol{x}_i$ 进行中心化处理：$x_i=\boldsymbol{x}_i-\mu,\mu=\frac1n\sum_{j=1}^nx_j$
> 2. 计算原始样本数据的协方差矩阵：$\Sigma=\frac1{n-1}\mathbf{X}^\mathrm{T}X$
> 3. 对协方差矩阵 $\Sigma$ 进行特征值分解，对所得特征根按其值大到小排序 $\lambda_1\geq\lambda_2\geq\cdots\geq\lambda_d$
> 4. 取前 $\iota$ 个最大特征根所对应特征向量 $w_1,w_2,...,w_l$ 组成映射矩阵 W 
> 5. 将每个样本数据 $x_i$ 按照如下方法降维：$(x_i)_{1\times d}(\mathbf{W})_{d\times l}=1\times l$


#### 特征人脸

**使用一组特征向量的线性组合来表示原始人脸**
- 用（特征）人脸表示人脸，而非用像素点表示人脸
- 将每幅人脸图像转换成列向量
	- 如将一幅 32 × 32 的人脸图像转成 1024 × 1 的列向量
- 每幅人脸分别与每个特征人脸做矩阵乘法，得到相关系数
	- l 个相关系数

> [!NOTE] 特征人脸算法
> - 输入：$n$ 个 1024 维人脸样本数据所构成的矩阵 X，降维后的维数 $l$
> - 输出：映射矩阵 W $=\left\{w_1, w_2,..., w_l\right\}($ 其中每个 $w_j ( 1\leq$ j $\leq l)$ 是一个特征人脸)
> ---
> 算法步骤：
> 1. 对于每个人脸样本数据 $x_i$ 进行中心化处理：$x_i=x_i-\mu,\mu=\frac1n\sum_{j=1}^nx_j$
> 2. 计算原始人脸样本数据的协方差矩阵：$\Sigma=\frac1{n-1}X^\mathrm{T}X$
> 	用 $L=XX^T$ 代替大的协方差矩阵计算，避免 d 维度过高计算复杂
> 3. 对协方差矩阵 $\Sigma$ 进行特征值分解，对所得特征根从到小排序 $\lambda_1\geq\lambda_2\geq\cdotp\cdotp\cdotp\geq\lambda_d$
> 4. 取前 $l$ 个最大特征根所对应特征向量 $w_1, w_2,..., w_l$ 组成映射矩阵 W 
> 5. 将每个人脸图像 $x_i$ 按照如下方法降维：$(x_i)_1\times d (\mathbf{W})_{d\times l}=1\times l$


![Pasted image 20250427152237.png|475](/img/user/CS3022F%20%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%20AI/public/Pasted%20image%2020250427152237.png)


在特征维度较高的情况下，主成分分析算法暴力求解特征向量是一个耗时操作。可以使用一种矩阵分解方法——奇异值分解（singular value decomposition, SVD）来实现主成分分析，对原始数据进行降维
- 用 $L=XX^T$ 代替大的协方差矩阵计算，避免 d 维度过高计算复杂

### 3.6 演化算法

#todo 

---
## 05 神经网络与深度学习










