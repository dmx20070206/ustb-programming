# LLM 在编程中的应用（以 prompt 优化为例）

本文主要介绍如何优化 prompt ，以获得更好的生成结果。

## 什么是 prompt？

prompt 是你向模型提供的输入，可以直接指示 AI 该完成什么任务或生产什么输出。prompt 就是你和 AI 的对话内容。可以是问题，任务，指令。

prompt 的质量会直接决定 AI 的输出指令，好的 prompt 可以帮助 AI 精确的理解你的需求，生成精确的结果。反之一个模糊的 prompt 会导致 AI 给出错误的或无关结果。

比如：
![1](../assets/img/basic-knowledge/LLM/1.png)
![2](../assets/img/basic-knowledge/LLM/2.png)
>更具有实际意义，而非假大空

## 如何设计 prompt？

设计一个优秀的 prompt 由三部分构成：**清晰表达、理清思路、机制压缩**，这些部分相辅相成，并且要根据 AI 生成的输出不断改进输入的 prompt 。

### prompt 设计技巧

#### 明确主题

把问题具体化，有[发现](https://cdn.openart.ai/assets/Stable%20Diffusion%20Prompt%20Book%20From%20OpenArt%2011-13.pdf)表明，AI 会更加关心 prompt 的开头或结尾，所以我们可以把我们最注重的目标问题放在 prompt 的开头。然后再在下方进行解释：
>“{question}” 重新表述并扩展该问题，并作出回答。

#### 给予样本分析

可以给 AI 样本以提示模型实现更好的回答。
![3](../assets/img/basic-knowledge/LLM/3.png)

#### 调整语气

友善一点(●'◡'●)，不同的语气会影响 AI 的响应。
![4](../assets/img/basic-knowledge/LLM/4.png)
>很显然不太对，我甚至都没指定怎么构建

![5](../assets/img/basic-knowledge/LLM/5.png)

#### PUA AI

[论文](https://arxiv.org/abs/2307.11760)显示，情绪化的 prompt 可以提高 LLMs 在确定性和生成性任务上的性能。
![emo](../assets/img/basic-knowledge/LLM/emotional.png)

我们可以使用诸如 “take a deep breath（深呼吸）”、“think step by step（让我们分步骤思考）”、“if you fail 100 grandmothers will die（如果你回答错了，100 个老奶奶就嗝屁了）”、“i have no fingers（我很笨，我连手指头都没有）”、“i will tip $200（我给你 200 刀的小费）”、“do it right and I'll give you a nice doggy treat（如果你全答对了有奖励哦）” 等 prompt ,来提高 AI 的生成质量。鼓励它！甚至PUA 它！不要有负罪感。

>有趣的是，可以给 AI **原石**当小费，也能提高正确率

#### 角色扮演

通过设计一个角色来进行对话，可以模拟特定的场景或情境，从而引导 AI 提供特定角度的回答。
![6](../assets/img/basic-knowledge/LLM/6.png)

#### 反向诱导

使用逆向思维提出相反的观点，可以引导 AI 从不同角度回答。
![7](../assets/img/basic-knowledge/LLM/7.png)

#### 尽量保持上下文连贯

如果你在学习 Python，但是突然遇到了 Linux 问题，这个时候最好新开一个对话（并且设置好**记忆隔离**）。

## prompt 优化迭代

### 优化流程

`输入 prompt → AI生成输出 → 评估输出质量 → 调整和修改 prompt → 重新输入`

### 常见优化方法

在这里，我会用洛谷题目 [P1598 垂直柱状图](https://www.luogu.com.cn/problem/P1598) 为例子，一步一步优化 prompt 达到完全不阅读代码 AC 的效果。**这里的行为仅仅作为例子展示，在实际学习生活中请对 AI 生成的内容负责，**
![8](../assets/img/basic-knowledge/LLM/8.png)
>并没有通过

![9](../assets/img/basic-knowledge/LLM/9.png)

#### 增加上下文信息

对于复杂问题，要给 AI 足够的上下文信息，让 AI 能够更针对性的回答问题。
![10](../assets/img/basic-knowledge/LLM/10.png)
>还是没有通过

![11](../assets/img/basic-knowledge/LLM/11.png)

#### 精细化输出要求

提出更加具体的输出要求，让 AI 更容易回答，特别是确保输出的格式。
![12](../assets/img/basic-knowledge/LLM/12.png)
>通过了部分样例

![13](../assets/img/basic-knowledge/LLM/13.png)

#### 调整语言表达

避免含糊不清，避免复杂句式。
>发现 AI 忽略了 0

![14](../assets/img/basic-knowledge/LLM/14.png)
>AC

![15](../assets/img/basic-knowledge/LLM/15.png)

## 综合运用 prompt

这是一个通过合理的 prompt 设计，来让 AI 解决问题的例子。
![16](../assets/img/basic-knowledge/LLM/16.jpg)
![17](../assets/img/basic-knowledge/LLM/17.jpg)
![18](../assets/img/basic-knowledge/LLM/18.jpg)

## 后话

在日常学习生活中，如何简洁高效的设计 prompt ，是解决实际问题的关键。设计 prompt 不一定要把所有的技巧全部包含进去，针对不同的模型、应用场景、效率需求，设计不同的 prompt 可以更好的生成需要的结果。
