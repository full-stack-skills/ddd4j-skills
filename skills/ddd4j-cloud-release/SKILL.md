---
name: ddd4j-cloud-release
description: Use when validating, publishing, or remotely consuming all ddd4j-cloud maintenance lines, including upstream Boot and ddd4j artifacts, Maven 3 or 4, private repository recovery, and clean-cache proof.
license: Apache-2.0
---

# ddd4j-cloud 发布

## Overview

统一介绍 八线串行构建、上游 Boot/ddd4j、Maven3/4、私服恢复、远端 metadata、空缓存消费，不按单个 artifact 拆技能。先选 Cloud→Boot→ddd4j 主组合，再读取当前分支。

## 核心范围

八线串行构建、上游 Boot/ddd4j、Maven3/4、私服恢复、远端 metadata、空缓存消费。

## 核心规则

1. 主组合与兼容备选分开，不从分支名猜 Boot/ddd4j。
2. 旧 cmpt 与新 extensions 命名不得混用。
3. Context/Tenant 在同步、异步、Reactor、Feign 终态恢复。
4. Binder、数据库、Nacos、Sentinel 等需真实外部行为证据。
5. 上游缺件、Cloud 失败、CI、发布和消费分别分类。

## 能力边界

### ✅ 擅长

- 发布的多实现选择与 Spring Cloud 集成。
- 上下游版本和跨服务边界。
- 八维护线差异。

### ⚠️ 需要素材

- 目标 Cloud 线、Boot parent 和 POM。
- 功能、外部服务与部署要求。
- 当前源码/测试/远端证据。

### ❌ 超范围

- 把 README 模块名当功能完成。
- 用配置存在替代外部服务行为。
- 未授权发布或生产操作。

## 工作流

1. 选择主版本组合。
2. 定位 extension、入口和上下游依赖。
3. 比较实现、传播、降级和生命周期。
4. 读取适当合同/验证 consumer 证据。
5. 输出版本、实现、外部依赖和风险。

## 输出与异常

缺少时输出“缺少：Cloud 线/上游/外部服务；补充方式：提供 POM 和验收行为”。

## 深度参考

- [功能矩阵](references/feature-matrix.md)
- [源码证据](references/source-evidence.md)
- [反模式](references/anti-patterns.md)
- [深度 FAQ](references/faq-deep.md)

## 隐私与安全

不得输出 Nacos/Redis/Broker/数据库/私服凭据或真实租户数据。

