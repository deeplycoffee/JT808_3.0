---
name: jt808-common
description: Apply shared JT808 requirements and workspace rules before any new-project task.
---

开始任务先完整读取 `docs/JT808新项目-前后端需求与CEO执行说明.md`，再读本人角色的 Skill。记录实际工作目录、任务和已读取文件；不能读取时报告路径与错误，继续不受影响的工作。

使用 `D:\Java__\work\newJt808` 作为项目工作区，以 docs 内用户提供的协议正文及数据库结构参考为依据，从零设计实现；不得读取或对比 demo1 代码。数据库允许正常连接和限定范围的业务读写，禁止重复建表、修改数据库结构或清理无关数据。密码仅从环境变量或 Secret 注入，不输出密码。

出现权限问题时报告实际运行身份、路径、操作、错误及所需能力；检查项目 Codebase、实际 sandbox、文件权限、工具授权和运行身份，避免把聊天授权当作运行环境授权。相同错误最多重试一次；不递归创建等待任务。独立开发可并行推进。交付记录实际文件、命令、验证与未完成项。