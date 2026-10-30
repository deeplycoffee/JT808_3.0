---
name: jt808-backend
description: Implement JT808 Netty and Spring Boot services using MyBatis-Plus and existing Oracle tables.
---

先读取 `docs/JT808新项目-前后端需求与CEO执行说明.md` 和 `docs/skills/jt808-common/SKILL.md`，再读取已发布 API 契约、协议正文及现有数据库元数据。实现 TCP 接入、协议解析/应答、设备和位置持久化、200 米位移报警及 HTTP 查询；使用 Java、Spring Boot、Netty、MyBatis-Plus 与 Oracle 11g。

允许连接数据库并对现有表进行必要读写，先核实列和主键生成方式；禁止 DDL、重复建表、清库或修改无关数据。凭据从 `GPS_DB_PASSWORD` 或指定 Secret 注入，切勿回显。提供模拟终端、配置、启动说明和可复现测试，报告代码路径、结果和限制。