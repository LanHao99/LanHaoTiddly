# LanHaoTiddly

这是一个基于 TiddlyWiki5 (TW5) 的个人知识库项目。

项目使用 TidGi 的工作区模式，将传统单文件 wiki 拆分为大量可版本控制的 tiddler 文件，主要内容存放在 tiddlers 目录中。相比直接维护单个 HTML 文件，这种方式更适合长期写作、版本管理和结构化维护。

## 项目简介

LanHaoTiddly 是一个以个人知识整理为核心的 TiddlyWiki 仓库。

它保留了 TW5 的原生语法和字段模型，同时借助 TidGi 将 wiki 内容拆分为小粒度文件，使日常编辑、搜索、差异比对和批量维护都更加直接。

这个仓库更适合作为“知识库源码”维护，而不是直接把生成后的单文件 wiki 当作唯一来源。

## 为什么使用 TidGi 拆分模式

传统 TiddlyWiki 常见做法是维护一个单独的 HTML 文件。这样便于分发，但在以下场景下不够理想：

- 内容增多后，单文件读写和保存成本更高
- Git diff 不易阅读，历史追踪不够清晰
- 批量整理标签、字段、命名时不够方便
- 协作或长期维护时，结构化程度不足

本项目采用 TidGi 工作区模式后：

- 每个 tiddler 都能作为独立文件管理
- 更容易使用 Git 查看细粒度变更
- 更适合脚本化处理和自动化维护
- 知识库结构更清晰，可维护性更高

## 技术基础

- TiddlyWiki5
- TidGi 工作区配置
- Node.js 构建脚本
- 可生成在线版、离线版和插件库构建产物

仓库中的关键配置文件：

- tiddlywiki.info：TW5 项目入口配置
- tidgi.config.json：TidGi 工作区与本地服务配置
- scripts/build.js：在线版、离线版、插件库构建脚本

## 目录说明

- tiddlers/：知识内容、系统配置和自定义 tiddler 的主要存放位置
- files/：附件或额外文件资源
- public/：构建时需要复制的静态资源
- scripts/：构建脚本和辅助脚本
- public/service-worker.js：PWA 相关资源
- public/manifest.webmanifest：站点 manifest

## 常用命令

安装依赖：

```bash
pnpm install
```

如果你不使用 pnpm，也可以：

```bash
npm install
```

启动本地 TW5 服务：

```bash
npm run server
```

当前脚本会以监听模式启动本地服务，默认端口为 8080。

构建在线版：

```bash
npm run buildonline
```

构建离线单文件版：

```bash
npm run buildoffline
```

构建插件库：

```bash
npm run buildlibrary
```

清理构建产物：

```bash
npm run clean
```

## 推荐维护流程

1. 使用 TidGi 或本地 TW5 服务编辑 tiddler。
2. 将内容以小粒度文件形式保存在 tiddlers 目录中。
3. 使用 Git 检查改动是否合理。
4. 在需要发布时执行构建脚本，生成在线版或离线版 HTML。

这种流程将“内容维护”和“发布产物”分离，适合长期积累型知识库。

## tiddler 编写约定

建议遵循以下原则：

- title 保持唯一且有语义
- 正文默认使用 text/vnd.tiddlywiki
- created、modified、tags、type 等字段保持完整
- 长内容优先按主题拆分，而不是持续堆在单一 tiddler 中
- 系统级 tiddler（如 $:/ 开头）与普通内容分开看待，避免误改

一个典型的 tid 文件通常由“字段区 + 空行 + 正文”组成。

示例：

```tid
created: 20260312000000000
modified: 20260312000000000
tags: [[知识库]] [[示例]]
title: 示例条目
type: text/vnd.tiddlywiki

这里是正文内容。
```

## 适合 AI 辅助的场景

由于本项目采用拆分式 tiddler 结构，因此非常适合借助 AI 完成以下工作：

- 新建和整理条目
- 统一标签体系
- 拆分长文为多个 tiddler
- 修复字段格式问题
- 建立条目之间的引用与导航关系

这也是为什么仓库中适合额外配置面向 TW5 tiddler 维护的 agent skill。

## 许可证

本项目的许可证以仓库中的 LICENSE 文件为准。
