## 前言
1. Obsidian提供本地知识库管理功能（配合git插件实现云端保存）
2. Ollama 提供本地大模型服务功能（提供repl和service环境）
## RAG能力

文档多起来之后，搜索和总结提纯是一件头疼的事情，但是大模型+RAG使这件事变得简单起来。
实现RAG的前提是，需要利用对应工具将我的文档转换成词向量导入到相应向量库中，方便大模型检索，对于Obsidian来说，这个工具就是[# Smart Connections](https://github.com/brianpetro/obsidian-smart-connections)。


