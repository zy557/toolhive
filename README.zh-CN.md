<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/images/toolhive-byline-white.svg">
  <img src="docs/images/toolhive-byline-black.svg" alt="ToolHive logo" width="500"/>
</picture>

<br>

[![Release][release-img]][release] [![Build status][ci-img]][ci]
[![Coverage Status][coveralls-img]][coveralls]
[![License: Apache 2.0][license-img]][license]
[![Star on GitHub][stars-img]][stars] [![Discord][discord-img]][discord]

[English](./README.md) | 简体中文

# ToolHive —— 简化并保护 MCP 服务器

**安全、即时、随处运行任何 Model Context Protocol (MCP) 服务器。**

ToolHive 提供了在生产环境中使用 MCP 服务器所需的一切工具。无需自行构建或整合各种组件，直接使用 ToolHive 的注册服务器、运行时、网关和门户，即可快速、安全地启动运行。

ToolHive 让您完全掌控 MCP 服务器生态。只需一次点击或一条命令，即可在锁定的容器中部署预审核的 MCP 服务器，并在数秒内与主流 AI 客户端完成集成。ToolHive 提供桌面应用、Web 应用、CLI 命令行工具和 Kubernetes Operator 等多种使用方式。

---

## 项目概述

ToolHive 是一款用 **Go** 语言编写的轻量级、安全的 [MCP（Model Context Protocol）](https://modelcontextprotocol.io)服务器管理平台。

MCP 是 Anthropic 提出的一种开放协议，允许 AI 客户端（如 Claude Desktop、Cursor、VS Code 等）通过统一接口调用外部工具和数据源。ToolHive 的核心价值在于：**让 MCP 服务器的部署、管理和安全访问变得简单可靠**。

---

## 为什么选择 ToolHive？

- **即刻部署**：通过 Docker 或 Kubernetes，一键或一条命令启动任意 MCP 服务器。
- **默认安全**：每个服务器均在隔离容器中运行，仅拥有所需的最小权限；密钥安全管理，永不以明文存储。
- **随处可用**：本地开发使用 UI 或 CLI，生产和大规模场景使用 Kubernetes Operator。
- **无缝集成**：自动配置 GitHub Copilot、Cursor、VS Code Server 等主流 AI 客户端。

---

## 核心架构

ToolHive 由四大核心组件构成：**网关（Gateway）**、**注册服务器（Registry Server）**、**运行时（Runtime）** 和 **门户（Portal）**。

### 🔌 网关（Gateway）

为团队定义安全高效访问工具的专属端点。

- 将多个工具编排为虚拟 MCP，支持确定性工作流引擎
- 定义访问策略和网络端点
- 集中管理安全策略、身份认证、授权、审计等
- 支持通过 OIDC/OAuth 与身份提供商（IdP）集成实现 SSO
- 自定义和过滤工具及描述，提升性能、降低 Token 消耗
- 与 Claude Desktop、Cursor、VS Code、VS Code Server 等本地客户端无缝连接

### 📦 注册服务器（Registry Server）

管理并维护团队可快速发现和部署的可信服务器目录。

- 与官方 MCP 注册表集成
- 支持添加自定义 MCP 服务器
- 按角色或用途对服务器分组
- 通过 API 驱动界面管理注册表，可嵌入现有工作流
- 内置安全控制：验证来源、签名服务器
- 预设配置和权限，提供顺畅的用户体验

### ⚙️ 运行时（Runtime）

在本地或 Kubernetes 集群中安全地部署、运行和管理 MCP 服务器。

- 通过 Kubernetes 在云端部署，实现企业级可扩展性
- 通过 Docker 或 Podman 在本地运行
- 安全代理远程 MCP 服务器，实现统一管理
- Kubernetes Operator 支持集群和资源管理
- 集成 OpenTelemetry 和 Prometheus 实现监控和审计日志

### 💻 门户（Portal）

简化企业开发者和知识工作者对 MCP 的使用。

- 跨平台桌面应用和基于浏览器的云端 UI
- 方便管理员策划 MCP 服务器和工具
- 自动化服务器发现
- 一键安装 MCP 服务器
- 兼容数百种 AI 客户端

---

## 三大主要组件

ToolHive 代码仓库包含以下三个核心可执行程序：

| 组件 | 说明 |
|------|------|
| `thv`（CLI） | 本地管理 MCP 服务器的主命令行工具 |
| `thv-operator`（K8s Operator） | 在 Kubernetes 集群中管理 MCP 服务器 |
| `thv-proxyrunner`（代理运行器） | 处理 MCP 服务器通信的代理功能 |

---

## 工作原理

1. **管理员** 在 **注册中心** 中整理和组织 MCP 服务器，配置访问权限和策略。
2. **用户** 通过 **门户** 发现并申请 MCP 服务器，ToolHive 自动编排安装和访问。
3. **运行时** 在本地和云端环境中安全地部署和管理 MCP 服务器，无缝集成现有 SDLC 工作流，导出分析数据，并执行细粒度访问控制。
4. **网关** 处理所有入站流量，保护上下文和凭据，优化工具选择，并应用组织策略。

---

## 支持的传输协议

ToolHive 支持多种 MCP 传输协议：

- **stdio**：标准输入/输出
- **HTTP**：传统 HTTP 请求
- **SSE**：Server-Sent Events 流式传输
- **Streamable HTTP**：自定义流式 HTTP 协议

---

## 部署方式

### 桌面/本地环境

个人开发者可在几分钟内通过桌面 UI 或 CLI 快速上手，并将相同的概念应用于企业环境。

**主要特性：**
- 从容器镜像运行任意 MCP 服务器，或从常见包管理器动态构建
- 使用简单的本地工具管理加密密钥并控制网络隔离
- 使用内置工具（如官方 MCP Inspector）测试和验证 MCP 服务器
- 通过 MCP Optimizer 优化 Token 使用和工具执行

### Kubernetes Operator

团队和组织通过熟悉的 Kubernetes 工作流集中管理 MCP 服务器和注册表。

**主要特性：**
- 为 MCP 服务器、注册表等 ToolHive 组件提供自定义资源定义（CRD）
- 基于容器的隔离和多命名空间支持的安全执行
- 自动化服务创建和发现，集成 Ingress 实现安全访问
- 企业级安全和可观测性：OIDC/OAuth SSO、安全令牌交换、审计日志、OpenTelemetry、Prometheus 指标
- 混合注册服务器：从上游注册表策划，动态注册本地 MCP 服务器，或代理可信的远程服务

---

## 安全模型

- **容器隔离**：所有 MCP 服务器均在独立容器中运行
- **Cedar 授权策略**：基于 Cedar 策略语言的细粒度授权控制
- **密钥管理**：支持多种后端（1Password、加密存储）
- **镜像验证**：容器镜像的证书验证
- **OIDC/OAuth2 认证**：企业级身份认证支持

---

## 快速链接

- 📥 [下载](https://toolhive.dev/download/)
- 📚 [文档](https://docs.stacklok.com/toolhive/)
- 🚀 快速入门指南：
  - [桌面应用](https://docs.stacklok.com/toolhive/tutorials/quickstart-ui)
  - [CLI](https://docs.stacklok.com/toolhive/tutorials/quickstart-cli)
  - [Kubernetes Operator](https://docs.stacklok.com/toolhive/tutorials/quickstart-k8s)
- 💬 [Discord 社区](https://discord.gg/stacklok)

---

## 技术栈

- **语言**：Go
- **CLI 框架**：Cobra
- **配置管理**：Viper
- **测试框架**：Ginkgo / Gomega
- **Kubernetes**：controller-runtime
- **可观测性**：OpenTelemetry
- **Web 路由**：Chi router
- **授权策略**：Cedar

---

## 许可证

本项目基于 [Apache 2.0 许可证](./LICENSE) 开源。

<!-- Badge links -->
<!-- prettier-ignore-start -->
[release-img]: https://img.shields.io/github/v/release/stacklok/toolhive?style=flat&label=Latest%20version
[release]: https://github.com/stacklok/toolhive/releases/latest
[ci-img]: https://img.shields.io/github/actions/workflow/status/stacklok/toolhive/run-on-main.yml?style=flat&logo=github&label=Build
[ci]: https://github.com/stacklok/toolhive/actions/workflows/run-on-main.yml
[coveralls-img]: https://coveralls.io/repos/github/stacklok/toolhive/badge.svg?branch=main
[coveralls]: https://coveralls.io/github/stacklok/toolhive?branch=main
[license-img]: https://img.shields.io/badge/License-Apache2.0-blue.svg?style=flat
[license]: https://opensource.org/licenses/Apache-2.0
[stars-img]: https://img.shields.io/github/stars/stacklok/toolhive.svg?style=flat&logo=github&label=Stars
[stars]: https://github.com/stacklok/toolhive
[discord-img]: https://img.shields.io/discord/1184987096302239844?style=flat&logo=discord&logoColor=white&label=Discord
[discord]: https://discord.gg/stacklok
<!-- prettier-ignore-end -->

<!-- markdownlint-disable-file first-line-heading no-inline-html no-emphasis-as-heading -->
