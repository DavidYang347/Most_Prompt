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
  - [3. Other Tricks](#3-Other-Tricks)
    - [Personification](#Personification)
    - Prompt Framework
      - CO-START



## 1. Structure Prompt
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
consistent throughout. Avoid mixed usage, such as using # to indicate both headers 
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


>- ***Chain of Thought***: a series of intermediate reasoning steps.

### Why COT?

significantly improves the ability of large language models to perform complex 
reasoning. In particular, we show how such reasoning abilities emerge naturally 
in sufficiently large language models via a simple method called chain of thought 
prompting, where a few chain of thought demonstrations are provided as exemplars 
in prompting.

Quoted from the paper [_Chain-of-Thought Prompting Elicits Reasoning in Large Language Models_](https://arxiv.org/abs/2201.11903)


### How to apply COT?

- Think step by step
- Output thinking process in answer.
  - Notes: LLMs answer your question based on generating the last word.

## 3. Other Tricks
### Personification

Personification: Treat LLM like a human being.



---

