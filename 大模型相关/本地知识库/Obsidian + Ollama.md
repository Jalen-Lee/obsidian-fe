## 前言
1. Obsidian提供本地知识库管理功能（配合git插件实现云端保存）
2. Ollama 提供本地大模型服务功能（提供repl和service环境）
## RAG能力

文档多起来之后，搜索和总结提纯是一件头疼的事情，但是大模型+RAG使这件事变得简单起来。
实现RAG的前提是，需要利用对应工具将我的文档转换成词向量导入到相应向量库中，方便大模型检索，对于Obsidian来说，这个工具就是[# Smart Connections](https://github.com/brianpetro/obsidian-smart-connections)插件。

这个插件负责将我们提供的文档生成Embedding，然后喂给我们提供的大模型服务，这个的大模型服务可以是Open AI、谷歌等厂商的云服务，也可以是我们本地部署的，本文以ollama本地部署的llama3 8b为例。

## Ollama

安装ollama后，可以通过pull 和 run 命令分别下载和启动大模型服务，启动后ollama提供一个repl的环境让我们直接与大模型交互。

要与Obsidian打通，我们需要用到serve命令起一个http服务器，然后在Obsidian的Smart Connections配置中配置



