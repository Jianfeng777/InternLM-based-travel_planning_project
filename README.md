# 旅游路线规划项目描述

## 项目背景

旅游作为一种广受欢迎的休闲方式，对于很多人来说，它不仅仅是从一个地方到另一个地方的简单移动，而是一种文化和经验的探索。随着技术的发展，人们越来越倾向于通过数字化手段来规划和优化他们的旅行体验。特别是在信息爆炸的时代，如何快速有效地从大量数据中提取出有用信息，成为了一项挑战。

本项目旨在利用先进的大语言模型（如InternLM-7B），为用户提供一个智能化的旅游规划工具。通过理解用户的具体需求，系统能够自动提取关键词，搜索相关信息，并从中总结出用户需求的旅游建议。

这一过程不仅减轻了用户在旅游计划过程中的负担，还提高了旅游规划的效率和质量。利用大语言模型的强大能力，结合特定的提示词模板、关键词提取、信息筛选和向量数据库技术，本项目旨在创造一个既实用又高效的旅游规划体验。


![image](https://github.com/InternLM/tutorial/assets/108343727/303cbc2a-89df-4256-8d9c-9de4edc5c1bf)

## 项目目标
本项目的目标是，当用户提出一个问题以后，比如说我要制定一个三天两夜的北京行程，那大语言模型就可以理解客户想要的是什么，然后提取部分的关键词，比如说北京旅游景点、三天两夜，然后在网络上搜索或者说是在特定的API里调用对应的信息。

调用完信息以后，还需要稍微的判断一下这个找到的信息是否是合适的，假如合适的话，就将这部分的信息存储在向量数据库当中。然后我们基于用户的问题再从向量数据库找到前几条最匹配的作为输入传递给大语言模型，最后就是设计一套提示词模板来将这部分内容整合从而能够输出一个还不错的旅游路线规划。

## 任务拆分

1. **设计关键词提取模块**：
   - 这部分其实可以考虑直接设计提示词来实现，也可以通过采集数据集微调的方式来实现。设计提示词的话其实就是告诉大语言模型按照什么样的格式进行输出，然后测试确保大语言模型能够做到。微调的话其实就是采集关键词提取的数据集，采集数据的方法其实可以通过ChatGPT或者手工实现，然后通过Xtuner微调实现。

2. **信息采集**：
   - 在获取到具体的关键词后，我们就可以考虑api或者搜索或者爬虫的方式来实现相关信息的采集工作。

3. **信息筛选**：
   - 采集到的信息我们还需要将其一条条的分开，并且判断这部分的内容是否合适。判断是否合适也可以考虑使用提示词工程或者是微调一个模型来实现。

4. **向量数据库存储**：
   - 确定了信息是合适的以后，我们可以将这部分信息存入到向量库当中直到完成搜索。

5. **信息检索与整合**：
   - 然后我们可以利用问题在向量数据库中找到最匹配的前n条信息作为信息传入到大语言模型当中作为背景。

6. **提示词模板设计**：
   - 最后我们还需要设计一套提示词，将向量数据库当中的信息、用户的提问、相关的一些案例演示等内容整合在一起，然后传给最终的大语言模型为我们生成一个完整的旅游路线规划。
  
7. **额外项目 - 语气微调**：
   - 除了上面基础的内容以外，我们其实还可以考虑去微调一个语气很像真正旅游客服的大语言模型，让其为我们进行回复。当然这个也可以通过提示工程完成，但是通过微调的方式或许能够更加真实的进行扮演。

8. **模型量化部署**：
   - 对微调好的模型进行量化部署，检验学习成果。

## 技术路线

- **关键词提取模块**：langchain设计提示词模板或使用xtuner对InternLM-7B模型进行指令微调。一般来说，只要我们把要求给到ChatGPT就能够帮助我们完成数据集的制作。
- **信息采集**：可以通过google_search的api调用实现（可以考虑用langchain里提供的工具进行获取，这部分的话比较复杂可以简化）
- **信息筛选**：判断是否合适的话也可以采用langchain调用大模型实现，或者也是使用xtuner来进行微调。
- **向量数据库存储**：向量数据库的存储和读取就是参照着第三节课里的方法，通过langchain提供的向量数据库接口来实现。
- **语气微调**：旅游客服的语气微调的话也是可以在提示词里写下或者用xtuner，然后这里的话也需要将所有的内容一并进行整合在一起实现。
- **模型部署**：使用LMDeploy进行模型部署量化即可。

## 项目成员
- 李剑锋
- 青岛龙腾四海
- PKCR
- Alisa Hu
- 留学森

欢迎感兴趣的朋友假如一起尝试呀！
