# Industry Multi-Agent

基于 LangChain 的工业软件文档多智能体生成系统。通过多个协作智能体，自动化生成符合行业规范的需求分析文档和详细设计文档。

## 项目结构

```
├── Multi-Agent-Framework/     # 多智能体核心框架
├── Multi-Agent-Requirement/   # 需求分析文档生成智能体
├── Multi-Agent-DetailedDesign/# 详细设计文档生成智能体
└── binary-tools/              # Rust 工具链（工作区初始化、文档构建）
```

### Multi-Agent-Framework

多智能体管理框架，提供：
- 智能体生命周期管理（配置、调度、会话）
- 工具系统（文件 I/O、HTTP API、二进制工具调用）
- 技能系统（Typst 排版、文档操作等可复用技能）
- 会话持久化与恢复
- WebUI 交互界面

### Multi-Agent-Requirement

需求分析文档生成，包含多层级智能体协作：
- 协调智能体：创建工作区，调度各章节智能体
- 业务描述智能体：生成业务描述章节
- 功能性需求智能体：生成功能范围、架构设计、功能点
- 非功能性需求智能体：按维度生成非功能性需求
- 绘图工具智能体：生成 Mermaid / PlantUML 图

### Multi-Agent-DetailedDesign

详细设计文档生成，包含：
- 概述智能体、结构设计智能体
- 子系统/模块设计智能体：生成模块级详细设计（业务说明、画面设计、数据库表、逻辑处理）
- 附录智能体

### binary-tools

Rust 编写的辅助工具：
- `init-workspace`：初始化文档工作区
- `build-doc`：构建 Typst 文档

## 技术栈

- Python 3.13+, LangChain, FastAPI
- Rust (binary-tools)
- Typst（文档排版）
- DeepSeek API（LLM 提供者）

## 快速开始

### 环境准备

```bash
# 克隆仓库（含子模块）
git clone --recursive https://github.com/cxz52351-sketch/Industry_multi_agent.git
cd Industry_multi_agent
```

### 安装依赖

```bash
# 安装框架（推荐使用 uv）
cd Multi-Agent-Framework
uv pip install -e .

# 安装需求分析模块
cd ../Multi-Agent-Requirement
uv pip install -e .

# 安装详细设计模块
cd ../Multi-Agent-DetailedDesign
uv pip install -e .
```

### 配置 API 密钥

复制模板并填入你的 API Key：

```bash
# 需求分析模块
cp Multi-Agent-Requirement/config/provider.toml.example Multi-Agent-Requirement/config/provider.toml

# 详细设计模块
cp Multi-Agent-DetailedDesign/config/provider.toml.example Multi-Agent-DetailedDesign/config/provider.toml
```

编辑 `provider.toml`，填入你的 API Key。

### 运行

```bash
# 命令行模式
multi-agent --config config.yaml

# WebUI 模式
multi-agent-webui
```

## 构建二进制工具（可选）

```bash
cd binary-tools
cargo build --release
```
