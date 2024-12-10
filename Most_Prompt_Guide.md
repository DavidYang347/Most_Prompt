# Most Prompt Guide

---
- Author: DavidYng347
- Date: 2024.11 
- Usage: LLM Prompt
- Test in: GPT-4o


## Table of Contents

---

- [Most Prompt Guide](#Most-Prompt-Guide)
  - [1. Structure Prompt](#1-Structure-Prompt)
    - [Why Structure Prompt?](#Why-Structure-Prompt)
    - [How to Structure Prompt?](#How-to-Structure-Prompt)
  - [2. Chain of Thought (COT)](#2-Chain-of-Thought-COT)
    - [Why COT?](#Why-COT)
    - [How to apply COT?](#How-to-apply-COT)
    - [Automatic Chain-of-Thought (Auto-CoT)](#Automatic-Chain-of-Thought-Auto-CoT)
    - [Tree of Thoughts (TOT)](#Tree-of-Thoughts-TOT)
  - [3. Other Techniques](#3-Other-Techniques)
    - [Personification](#Personification)
    - [Few-shot Prompt](#Few-shot-Prompt)
  - [4. Prompt Framework](#4-Prompt-Framework)
    - [CO-STAR]()
  - [5. Prompt Tutorial Collection](#5-Prompt-Tutorial-Collection)



## 1. Structure Prompt

---
### Why Structure Prompt?
>- Structured: Organizing information to follow specific patterns and 
rules, making it easier and more efficient to understand.

The advance of structured prompt:
1. Clear Structure: Unity of Content and Form
2. Enhance Semantic Cognition
3. Directed Awakening of Deep Capabilities in Large Models
4. Build Production-Grade Prompts Like Code Development

Quoted from the project by [LangGPT](https://github.com/langgptai/LangGPT/blob/main/Docs/HowToWritestructuredPrompts.md).

### How to Structure Prompt?

1. Prompt Grammar:
<br> **_markdown_**: Markdown is easy to learn and use, which is the 
most common format in prompt. Almost all LLMs support Markdown format.
<br> **_lisp_**: Lisp is an old programming language, only can be used in Claud.
So far, Gpt-4o don't support lisp. But there are some cases for Cloud Prompt 
based on lisp showed interesting result,such as example provided by
[Li Jigang](https://web.okjike.com/u/752D3103-1107-43A0-BA49-20EC29D09E36).
<br> **_json_**, **_yaml_**, **_toml_**...

2. Maintain contextual semantic consistency:
<br> **_format semantic consistency_**: Ensure the identifier's function remains 
consistent throughout. Avoid mixed usage, such as using `#` to indicate both headers 
and variables, as this creates inconsistency. Such practices can disrupt the 
model's ability to recognize the hierarchical structure of prompts. 
<br> **_content semantic consistency_**: Ensure the semantic appropriateness of
attribute terms in the chain of thought.

3. Maintain contextual semantic consistency:
<br> **_Build a global Chain of Thought_**: A well-structured prompt template, 
in a sense, establishes a robust global chain of thought.COT will be explained in 
the next chapter. For instance, the template design demonstrated in LangGPT 
considers the following chain of thought:
> Role -> Profile (intro of role) -> Skills under Profile (skills of role) -> 
> Rules (riles of role) -> Workflow (workflow for the role meeting the above conditions) 
> -> Initialization (initial preparation for starting work) -> Begin actual usage.

```python
# python code example
prompt ='''
Role: 指定角色会让 GPT 聚焦在对应领域进行信息输出
Profile author/version/description : Credit 和 迭代版本记录
Goals: 一句话描述 Prompt 目标, 让 GPT Attention 聚焦起来
Constrains: 描述限制条件, 其实是在帮 GPT 进行剪枝, 减少不必要分支的计算
Skills: 描述技能项, 强化对应领域的信息权重
Workflow: 重点中的重点, 你希望 Prompt 按什么方式来对话和输出
Initialization: 冷启动时的对白, 也是一个强调需注意重点的机会
'''
```

## 2. Chain of Thought (COT)

---
>- ***Chain of Thought***: a series of intermediate reasoning steps.

Introduced in [Wei et al. (2022)](https://arxiv.org/abs/2201.11903), 
chain-of-thought (CoT) prompting enables 
complex reasoning capabilities through intermediate reasoning steps. You can 
combine it with few-shot prompting to get better results on more complex 
tasks that require reasoning before responding.


### Why COT?

significantly improves the ability of large language models to perform complex 
reasoning. In particular, we show how such reasoning abilities emerge naturally 
in sufficiently large language models via a simple method called chain of thought 
prompting, where a few chain of thought demonstrations are provided as exemplars 
in prompting.

Quoted from the paper [_Chain-of-Thought Prompting Elicits Reasoning in Large Language Models_](https://arxiv.org/abs/2201.11903)


### How to apply COT?

- Tell LLMs `Think step by step`.
- Output thinking process in answer.
  - Notes: LLMs answer your question based on generating the last word, during this 
process, LLMs will consider the generated context before. Therefore, if the previous
context of answer contain the thinking process, LLMs more like to give a reasonable
answer for complete query.

One recent idea that came out more recently is the idea of 
zero-shot CoT (Kojima et al. 2022) that essentially involves adding "Let's think 
step by step" to the original prompt. Let's try a simple problem and see how the 
model performs:

_Naive Prompt:_
```
I went to the market and bought 10 apples. I gave 2 apples to the neighbor and 2 to 
the repairman. I then went and bought 5 more apples and ate 1. How many apples did 
I remain with?
```

_Naive Output:_
```
11 apples
```

The answer is incorrect! Now Let's try with the special prompt.

_COT Prompt:_
```
I went to the market and bought 10 apples. I gave 2 apples to the neighbor and 2 to the repairman. I then went and bought 5 more apples and ate 1. How many apples did I remain with?
Let's think step by step.
```

_COT Output:_
```
First, you started with 10 apples.
You gave away 2 apples to the neighbor and 2 to the repairman, so you had 6 apples left.
Then you bought 5 more apples, so now you had 11 apples.
Finally, you ate 1 apple, so you would remain with 10 apples.
```

### Automatic Chain-of-Thought (Auto-CoT)
Auto-CoT consists of two main stages:

- Stage 1): **question clustering**: partition questions of a given dataset into 
a few clusters
- Stage 2): **demonstration sampling**: select a representative question from each 
cluster and generate its reasoning chain using Zero-Shot-CoT with simple heuristics


### Tree of Thoughts (TOT)

- Tree of Thoughts (ToT), a framework that generalizes over chain-of-thought prompting
and encourages exploration over thoughts that serve as intermediate steps for 
general problem-solving with language models.

Hulbert (2023) has proposed Tree-of-Thought Prompting, which applies the main concept
from ToT frameworks as a simple prompting technique, getting the LLM to evaluate
intermediate thoughts in a single prompt. A sample ToT prompt is:
```
Imagine three different experts are answering this question.
All experts will write down 1 step of their thinking,
then share it with the group.
Then all experts will go on to the next step, etc.
If any expert realises they're wrong at any point then they leave.
The question is...
```

## 3. Other Techniques

---
### Personification

Personification: Treat LLM like a human being.

- Put pressure on the LLM
```
I urgently need to achieve this requirement to keep my job. 
If you cannot complete the task I've given you properly, I will lose my job.
```

- Reward the LLM
```
If you can complete the task excellently, I will reward you with $10
```

### Few-shot Prompt


## 4. Prompt Framework

---



## 5. Prompt Tutorial Collection

---

- [Prompt Engineering Guide](https://www.promptingguide.ai/)
- [通往AGI之路](https://waytoagi.feishu.cn/wiki/QPe5w5g7UisbEkkow8XcDmOpn8e)
- [langgptai/wonderful-prompts](https://github.com/langgptai/wonderful-prompts)
- [如何写好Prompt: 结构化 @lijigang](https://www.lijigang.com/posts/chatgpt-prompt-structure/)
- [李继刚 github案例](https://github.com/lijigang/prompts)