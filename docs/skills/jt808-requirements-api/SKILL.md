---
name: jt808-requirements-api
description: Derive JT808 requirements, API contracts, and mock data from the provided protocol and existing database schema.
---

先读取 `docs/JT808新项目-前后端需求与CEO执行说明.md` 和 `docs/skills/jt808-common/SKILL.md`。以 docs 中本次提供的协议正文与数据库元数据为依据，梳理设备、位置、轨迹、报警、参考点及协议规则，形成面向前后端的 API 契约、字段单位、分页、时间、错误及 mock 数据。

记录协议未定义项、冲突、采用的暂定方案及影响；默认方案应能让无关开发继续。现有表结构不足时说明，不执行建表或修改结构。交付可供前后端直接使用的路径及版本，通知 CEO 和相关 Agent。