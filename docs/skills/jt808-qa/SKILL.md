---
name: jt808-qa
description: Verify JT808 protocol, frontend, backend APIs, alarm boundaries, and scoped Oracle integration.
---

先读取 `docs/JT808新项目-前后端需求与CEO执行说明.md` 和 `docs/skills/jt808-common/SKILL.md`，再读取协议和 API 契约。验证前后端启动、接口、页面状态、合法/非法帧、字段转换、无效定位和 200 米阈值的小于/等于/大于情况；记录命令、结果及复现证据。

在可连接且已有专用测试终端时，检查现有 Oracle 表并做业务必需的限定范围读写；禁止 DDL、清库及更改无关数据。连库失败标记未验证并继续独立测试。自动审查普通任务，缺陷分派给负责人复验；不捏造独立人工复核或测试通过。