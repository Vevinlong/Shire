---
id: dakewe-java-test-2026
title: 达科威Java笔试题2026
description: |
  面向Java开发候选人的技术能力测评，覆盖Spring Boot、Redis、Docker、Spring Cloud、MySQL、Elasticsearch、RabbitMQ、MongoDB、JVM等核心技术栈。
  本试卷共 24 题，其中单选 11 题、多选 4 题、简答 9 题，预计 36 分钟完成。
tags: [java, spring-boot, redis, docker, spring-cloud, mysql, elasticsearch, rabbitmq, mongodb, recruitment]
schema_version: 2
format: qml-v2
question_count: 24
question_counts:
  single: 11
  multiple: 4
  short: 9
estimated_duration_minutes: 60
llm:
  model: gpt-5
  temperature: 0.0
  prompt_template: |
    请根据评分标准对考生答案打分，允许部分得分。
    只输出 JSON，不要解释，不要 Markdown。
    JSON 必须包含字段：score、reason、relevance、contradiction。
    - score：0 到 {{max_points}} 的整数
    - reason：1 到 3 句，说明得分点和失分点
    - relevance：0 到 3 的整数
    - contradiction：true 或 false

    题目：{{question}}
    评分标准：{{rubric}}
    考生回答：{{answer}}
---

## Q1 [single] (5) {answer_time=1m}

以下哪项是 Spring Boot 自动配置的核心注解？

- A) `@Configuration`
- B*) `@EnableAutoConfiguration`
- C) `@ComponentScan`
- D) `@SpringBootApplication`

[rubric]
`@EnableAutoConfiguration` 是 Spring Boot 自动配置的核心注解，它通过 `@Import` 导入 `AutoConfigurationImportSelector`，实现根据类路径中的依赖自动配置 Bean。`@SpringBootApplication` 是组合注解，包含 `@EnableAutoConfiguration`，但其本身不是一个单一职责的自动配置注解。
[/rubric]

## Q2 [single] (5) {answer_time=1m15s}

高并发场景下，Redis 的哪种数据结构适合实现分布式锁？

- A*) String
- B) Hash
- C) Set
- D) ZSet

[rubric]
Redis 的 String 类型配合 `SET key value NX EX timeout` 命令可实现原子性的分布式锁。`NX` 保证只在键不存在时设置，`EX` 设置过期时间防止死锁。Hash、Set、ZSet 不具备这种原子性锁机制。
[/rubric]

## Q3 [single] (5) {answer_time=1m}

Docker Compose 中用于定义服务依赖的关键字是？

- A*) `depends_on`
- B) `links`
- C) `volumes`
- D) `environment`

[rubric]
`depends_on` 用于声明服务之间的启动依赖关系，控制服务启动顺序。`links` 是旧版 Legacy 网络的容器链接方式，`volumes` 用于数据卷挂载，`environment` 用于设置环境变量。
[/rubric]

## Q4 [single] (5) {answer_time=2m}

以下哪种设计模式适合在 Spring Cloud 中实现服务熔断？

- A) 策略模式
- B) 观察者模式
- C*) 代理模式
- D) 责任链模式

[rubric]
Spring Cloud 中的熔断器（如 Hystrix、Resilience4j）通过代理模式实现：为服务调用生成代理对象，在代理中注入熔断逻辑（如统计失败率、打开/半开/关闭状态切换），从而实现故障隔离和快速失败。
[/rubric]

## Q5 [single] (5) {answer_time=1m15s}

MySQL 主从复制中，从库通过什么机制同步主库数据？

- A) Binlog
- B) Redo Log
- C) Undo Log
- D*) Relay Log

[rubric]
MySQL 主从复制流程：主库将数据变更写入 Binlog → 从库的 I/O 线程拉取 Binlog 并写入 Relay Log → 从库的 SQL 线程读取 Relay Log 并重放。因此从库通过 Relay Log 来同步主库数据，而非直接使用 Binlog。
[/rubric]

## Q6 [single] (5) {answer_time=1m}

医院系统中，Elasticsearch 最可能用于以下哪种场景？

- A) 患者挂号记录存储
- B) 药品库存实时更新
- C*) 病历全文检索
- D) 财务数据统计

[rubric]
Elasticsearch 基于倒排索引，擅长全文检索和模糊搜索，适合非结构化的病历文本搜索场景。挂号记录适合关系型数据库，库存更新需要事务保障，财务统计更适合 OLAP 引擎。
[/rubric]

## Q7 [multiple] (5) {answer_time=2m}

以下哪些是保证 RabbitMQ 消息可靠性的手段？

- A*) 持久化队列
- B*) 手动ACK机制
- C) 消息过期时间
- D*) 生产者确认机制

[rubric]
保证 RabbitMQ 消息可靠性的核心手段：持久化队列（Queue 和 Message 设置为 durable，防止 Broker 重启丢失）、手动 ACK（消费者处理完成后显式确认，避免消息丢失）、生产者确认（Publisher Confirm 机制，确保消息成功写入 Broker）。消息过期时间（TTL）用于消息的生命周期管理，不是可靠性保障手段。
[/rubric]

## Q8 [multiple] (5) {answer_time=2m}

Spring Cloud 中可用于服务发现的组件有哪些？

- A*) Nacos
- B*) Eureka
- C*) Consul
- D*) ZooKeeper

[rubric]
以上选项均为常见的服务发现组件。Nacos 是阿里巴巴开源的服务发现与配置中心；Eureka 是 Netflix 的服务发现组件；Consul 是 HashiCorp 的分布式服务发现和配置工具；ZooKeeper 也可用作服务注册中心（通过临时节点实现）。
[/rubric]

## Q9 [multiple] (5) {answer_time=2m}

哪些场景适合使用 MongoDB？

- A*) 医院设备日志存储
- B*) 患者结构化电子病历
- C) 药品实时库存管理
- D) 医生排班关系型数据

[rubric]
MongoDB 适合存储半结构化/非结构化的文档数据。设备日志数据量大、结构灵活，适合 MongoDB 的文档模型；电子病历字段不固定、嵌套多，也适合文档存储。药品库存需要事务和一致性保障，医生排班属于强关系数据，更适合关系型数据库。
[/rubric]

## Q10 [multiple] (5) {answer_time=2m}

以下哪些是 Docker 镜像优化策略？

- A*) 使用多阶段构建
- B*) 合并RUN指令减少层数
- C*) 使用Alpine基础镜像
- D) 将日志文件挂载到宿主机

[rubric]
多阶段构建可分离构建环境和运行环境，减小最终镜像体积；合并 RUN 指令能减少镜像层数；Alpine 是极简 Linux 发行版，基础镜像仅约 5MB。将日志挂载到宿主机是运行时的运维策略，不是镜像本身的优化。
[/rubric]


## Q11 [single] (2) {answer_time=45s}

`@Transactional` 注解的 `readOnly=true` 属性可以优化 MySQL 写操作性能。

- A) 正确
- B*) 错误

[rubric]
`readOnly=true` 用于提示数据库该事务只读，MySQL 可以利用该 Hint 优化读操作（如避免行锁升级），但不能优化写操作性能。写操作受限于磁盘 I/O、索引维护等，与 `readOnly` 无关。
[/rubric]

## Q12 [single] (2) {answer_time=45s}

Redis 的 `LRU` 淘汰策略适合缓存患者高频查询数据。

- A*) 正确
- B) 错误

[rubric]
LRU（Least Recently Used）策略会淘汰最近最少使用的键，保留热点数据。患者高频查询数据正符合 LRU 的适用场景：常用数据常驻缓存，冷数据被自动淘汰。
[/rubric]

## Q13 [single] (2) {answer_time=45s}

`Dockerfile` 中的 `COPY` 指令会自动解压 tar 文件到镜像中。

- A) 正确
- B*) 错误

[rubric]
`COPY` 指令不会自动解压文件，会将源路径的文件原样复制到镜像中。需要自动解压 tar 文件应使用 `ADD` 指令，`ADD` 会自动解压 tar 归档。实际使用中推荐优先使用 `COPY`，仅在需要自动解压时才使用 `ADD`。
[/rubric]

## Q14 [single] (2) {answer_time=45s}

Elasticsearch 的倒排索引适合处理非结构化文本数据。

- A*) 正确
- B) 错误

[rubric]
倒排索引是 Elasticsearch 的核心数据结构，它将文档中的词汇映射到包含该词的文档列表，非常适合全文检索和文本搜索场景。非结构化文本数据（如日志、病历、文章）正是倒排索引的标准应用场景。
[/rubric]

## Q15 [single] (2) {answer_time=45s}

Feign 客户端默认支持服务发现和负载均衡。

- A*) 正确
- B) 错误

[rubric]
Spring Cloud OpenFeign 默认集成了 Ribbon（或 Spring Cloud LoadBalancer），配合服务注册中心（如 Nacos、Eureka），可以自动完成服务发现和客户端负载均衡，无需手动配置。
[/rubric]

## Q16 [short] {max=2, answer_time=1m15s}

Spring Boot 中读取配置文件的注解有哪些？（写出至少一个）

[rubric]
1. 维度: 正确答案
   - 满分描述: 正确写出 `@Value` 或 `@ConfigurationProperties` 中的至少一个
   - 部分得分: 写出其他相关注解但非标准配置读取注解
2. 维度: 完整性
   - 满分描述: 同时写出两个注解并简要说明区别（`@Value` 用于单个属性注入，`@ConfigurationProperties` 用于批量绑定）
[/rubric]

## Q17 [short] {max=2, answer_time=1m15s}

防止缓存穿透的 Redis 方案是什么？

[rubric]
1. 维度: 正确答案
   - 满分描述: 回答"布隆过滤器"，能简要说明其原理（通过多个哈希函数判断键是否存在，过滤掉不存在的键请求）
   - 部分得分: 提到其他方案（缓存空值、互斥锁等）但未提及布隆过滤器
[/rubric]

## Q18 [short] {max=2, answer_time=1m15s}

Docker 中跨主机容器通信的网络解决方案是什么？

[rubric]
1. 维度: 正确答案
   - 满分描述: 回答"Overlay 网络"，能说明其通过 VXLAN 隧道在不同宿主机的 Docker 守护进程之间创建虚拟网络
   - 部分得分: 提到其他方案（如 Macvlan、Weave、Calico 等）但未提及 Overlay
[/rubric]

## Q19 [short] {max=2, answer_time=1m15s}

医院系统接口幂等性设计的常用方案有哪些？（写出至少一个）

[rubric]
1. 维度: 正确答案
   - 满分描述: 回答"Token 机制"或"唯一索引"中的至少一个，并能简要说明原理
   - 部分得分: 提出其他幂等方案（如乐观锁、状态机等）但非核心方案
[/rubric]

## Q20 [short] {max=2, answer_time=1m15s}

JVM 调优参数 `-Xmx` 表示什么？

[rubric]
1. 维度: 正确答案
   - 满分描述: 回答"最大堆内存"或"JVM 堆的最大大小"，并能简要说明其作用（控制 Java 应用可使用的最大堆内存，防止内存溢出）
[/rubric]

## Q21 [short] {max=5, answer_time=6m}

如何设计医院患者数据的 MySQL 分表方案？

[rubric]
1. 维度: 分表策略
   - 满分描述: 提出按患者 ID 哈希分表，说明能避免热点问题，并给出具体分片数或哈希算法
   - 部分得分: 提到分表但未明确分片键或策略
2. 维度: 冷热数据分离
   - 满分描述: 明确提到冷热数据分离，历史数据归档到独立表，说明分离依据（如就诊时间）
   - 部分得分: 提到数据归档但未区分冷热
3. 维度: 中间件选型
   - 满分描述: 提到 ShardingSphere 或其他分库分表中间件，说明其管理分片逻辑的作用
   - 部分得分: 仅提到手动分表，未涉及中间件
4. 维度: 扩展性
   - 满分描述: 考虑到二次分表、数据迁移或扩容策略
   - 部分得分: 未提及扩展性
[/rubric]

## Q22 [short] {max=5, answer_time=6m}

简述 Spring Cloud Gateway 如何实现医院系统的接口鉴权。

[rubric]
1. 维度: 全局过滤器
   - 满分描述: 提出定义 GlobalFilter，说明其拦截所有请求，验证 JWT Token 的完整流程（解析、验签、过期检查）
   - 部分得分: 提到过滤器但未说明 JWT 验证细节
2. 维度: 白名单机制
   - 满分描述: 明确提到白名单放行公开接口（如登录、注册），给出具体实现方式（路径匹配或注解标记）
   - 部分得分: 提到白名单但无具体实现方式
3. 维度: 权限缓存
   - 满分描述: 结合 Redis 缓存用户权限规则，减少数据库查询，提升网关吞吐量
   - 部分得分: 提到缓存但未结合 Redis
4. 维度: 安全性
   - 满分描述: 考虑 Token 刷新、黑名单、接口级别权限控制等安全增强措施
   - 部分得分: 仅描述基本流程
[/rubric]

## Q23 [short] {max=5, answer_time=6m}

为什么医院私有化部署推荐使用 Docker Compose？至少列出 3 点原因。

[rubric]
1. 维度: 一键部署
   - 满分描述: 说明 Docker Compose 可一键启动多服务（数据库、缓存、应用等），降低部署复杂度
2. 维度: 环境隔离
   - 满分描述: 提到容器化隔离医院内网环境与宿主机配置差异，避免依赖冲突和环境污染
3. 维度: 简化运维
   - 满分描述: 说明 Compose 文件即为部署文档，版本控制方便，简化运维流程和交接
4. 维度: 扩展性
   - 满分描述: 额外提到水平扩展（scale）、滚动更新、或与 Kubernetes 的衔接等高级特性
[/rubric]

## Q24 [short] {max=15, answer_time=16m}

在多线程环境下，设计实现一个医院药品库存管理类，满足以下要求：

1. 支持并发场景下的药品入库（增加库存）和出库（减少库存）
2. 出库时库存不足需抛出异常

```java
public class DrugInventoryManager {
    private final Map<String, AtomicInteger> inventory = new ConcurrentHashMap<>();

    public void addStock(String drugId, int quantity) {
        inventory.computeIfAbsent(drugId, k -> new AtomicInteger(0)).addAndGet(quantity);
    }

    public void reduceStock(String drugId, int quantity) throws InventoryNotEnoughException {
        AtomicInteger stock = inventory.getOrDefault(drugId, new AtomicInteger(0));
        int current = stock.get();
        if (current < quantity) {
            throw new InventoryNotEnoughException("药品" + drugId + "库存不足");
        }
        stock.addAndGet(-quantity);
    }

    public static class InventoryNotEnoughException extends Exception {
        public InventoryNotEnoughException(String message) { super(message); }
    }
}
```

[rubric]
1. 维度: 线程安全实现（7分）
   - 满分描述: 使用 `ConcurrentHashMap` + `AtomicInteger` 或等效的线程安全数据结构，并发控制正确
   - 部分得分: 使用 `synchronized` 或 `ReentrantLock` 等锁机制但实现基本正确
2. 维度: 异常处理与边界条件（4分）
   - 满分描述: 正确判断库存不足并抛出异常，处理了空键情况（`computeIfAbsent` / `getOrDefault`），考虑了负数入库等边界
   - 部分得分: 只实现了基本的库存不足检查
3. 维度: 代码可读性与设计（4分）
   - 满分描述: 自定义异常类清晰，代码有适当注释或命名规范，考虑事务回滚或补偿机制等高级设计
   - 部分得分: 代码可运行但缺少规范性
[/rubric]
