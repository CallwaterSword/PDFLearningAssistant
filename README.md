# 📚 PDF 智能学习助手

> 基于 [HelloAgents](https://hello-agents.datawhale.cc/) 的智能文档问答系统（Hello-Agents 教程第 8 章《记忆与检索》实战复现）

上传 PDF 文档，即可基于 RAG 进行智能问答、记录学习笔记、回顾学习历程、生成学习报告。

## ✨ 核心功能

- 📄 **加载 PDF 文档**：MarkItDown 解析（支持 PDF/Word/Excel/图片/音频）→ 智能分块 → 向量化 → 存 Qdrant
- 💬 **智能问答**：RAG 检索增强 + MQE（多查询扩展）+ HyDE（假设文档嵌入）高级检索
- 🧠 **四类记忆**：WorkingMemory（工作）/ EpisodicMemory（情景）/ SemanticMemory（语义）/ PerceptualMemory（感知）
- 📝 **学习笔记**：重要概念存入语义记忆
- 📊 **学习统计与报告**：会话时长 / 提问次数 / 笔记数 / JSON 学习报告

## 🛠️ 技术栈

- **框架**：HelloAgents 0.2.0（MemoryTool + RAGTool）
- **Web UI**：Gradio 6.x（4 个 Tab）
- **RAG**：MarkItDown + 智能分块 + Qdrant 向量存储 + MQE/HyDE 检索
- **LLM**：DeepSeek（OpenAI 兼容 API）

## 🚀 快速开始

### 1. 环境要求

- Python 3.12+（3.13 需要额外 audioop-lts 兼容垫片，见 requirements.txt）

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

### 3. 配置密钥

```bash
cp .env.example .env   # 然后编辑 .env 填入 LLM_API_KEY
```

### 4. 启动

```bash
python PDFLearningAssistant.py
```

浏览器访问 **http://localhost:7860**

### 5. 使用流程

1. 🏠 **开始使用** Tab：输入用户 ID → 点「初始化助手」→ 上传 PDF → 点「加载文档」
2. 💬 **智能问答** Tab：提问（如"什么是 Transformer？"），或带"之前/学过/回顾"关键词触发学习历程回顾
3. 📝 **学习笔记** Tab：记录学习心得与相关概念
4. 📊 **学习统计** Tab：刷新统计 / 生成学习报告

## ⚡ 性能提示

- `EMBED_MODEL_TYPE=local` 使用本地 CPU 嵌入（all-MiniLM-L6-v2），加载大 PDF 较慢；**建议改为 `dashscope` 云端嵌入**（配 `EMBED_API_KEY`）速度提升明显
- 大 PDF 可调大 `chunk_size`（默认 4000）减少分块数量，加快加载
- `QDRANT_MODE=memory` 数据在进程内，重启后需重新上传文档；如需持久化可配 Qdrant 服务

## 📦 项目结构

```
PDFLearningAssistant/
├── PDFLearningAssistant.py   # 主程序（业务类 + Gradio UI）
├── requirements.txt          # 依赖
└── .env.example              # 环境变量模板
```

## 📄 许可证

MIT

## 🙏 致谢

- [Hello-Agents 教程](https://hello-agents.datawhale.cc/)（Datawhale 社区）
- [hello-agents](https://github.com/jjyaoao/HelloAgents) 开源框架
