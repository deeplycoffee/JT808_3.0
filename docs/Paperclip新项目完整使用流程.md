# JT808 新项目完整使用流程

## 现有文件与范围

工作区：`D:\Java__\work\newJt808`。本目录已初始化 Git；`docs` 内已有用户提供的协议 DOCX 和 `schema-oracle.sql`，以及 CEO 需求文档和六个 Skill。SQL 是现有表结构参考，不是要执行的建表脚本。项目可以连接 Oracle，允许必要业务读写；禁止重复建表、改变数据库结构、清库和覆盖无关业务数据。

## 1. 配置 Paperclip 新项目

1. 创建新项目，将 Project Configuration 的 **Codebase / Local folder** 指向 `D:\Java__\work\newJt808`。界面可能没有 Workspaces 标签，以实际版本的 Codebase 字段为准。
2. 为每个 Agent 选择可用的模型连接和工作目录；核实其执行器实际可读写项目目录、可运行所需构建命令。Paperclip 的任务权限、运行 sandbox、Windows 文件权限和 MCP 文件工具是不同的权限层。
3. 旧的 `jt808-documents-mcp.mjs` 默认根目录为 `D:\Java__\work\jt808`，不会自动适用于新项目。若使用该文件工具，给新项目配置单独连接/进程，并让其环境变量 `JT808_DOCUMENT_ROOT` 指向 `D:\Java__\work\newJt808`；不要直接更改旧连接的根目录。还须验证连接授权、Agent 工具权限与实际调用。文件 MCP 的能力不等于 shell、构建或数据库权限。
4. 确保每个 Agent 的项目目录在其运行环境的可写范围内；不要依赖默认只读环境，也不要为了方便关闭全部安全控制。若执行器显示 `read-only`，调整其实际运行配置为允许工作区写入；具体字段以当前版本为准。
5. 数据库凭据在运行服务的实际用户或 Paperclip Secret 中设置 `GPS_DB_PASSWORD`。已在 Windows 当前用户环境登记过此变量，新进程才可能继承；若 Paperclip 服务由其他用户启动，需在该运行身份下配置。不要把密码粘进任务或文档。URL 为 `jdbc:oracle:thin:@127.0.0.1:1521:XE`，本地用户名 `SYSTEM`；实际连接和读取现有表需要运行验证。

## 2. 创建五个 Agent 并配置 Skill

| Agent | 通用 Skill | 角色 Skill |
| --- | --- | --- |
| CEO / 制定者 | `docs/skills/jt808-common/SKILL.md` | `docs/skills/jt808-ceo/SKILL.md` |
| 需求文档 / API | 同上 | `docs/skills/jt808-requirements-api/SKILL.md` |
| 后端 | 同上 | `docs/skills/jt808-backend/SKILL.md` |
| 前端 | 同上 | `docs/skills/jt808-frontend/SKILL.md` |
| 测试 | 同上 | `docs/skills/jt808-qa/SKILL.md` |

这些文件是可供读取的 Skill 源文件，**放在 docs 中并不保证 Paperclip 自动发现或启用**。在你安装的 Paperclip 版本支持的 Skills 配置中导入或关联通用 Skill 和对应角色 Skill；若界面不能按路径导入，就把相应 `SKILL.md` 内容放入该 Agent 的 Instructions，并在任务中要求它读取文件。每个 Agent 同时必须读取完整需求文档 `docs/JT808新项目-前后端需求与CEO执行说明.md`。根目录 `AGENTS.md` 是补充入口，不能代替 Paperclip 中的实际关联和运行验证。

## 3. 在每个 Agent 的真实运行中做预检

分别给五个 Agent 一个一次性预检任务：报告实际工作目录和身份；读取 CEO 需求、通用 Skill、角色 Skill、协议/SQL 参考；在项目内创建并编辑属于自己的临时文本文件后删除该临时文件；尝试其角色需要的构建/命令；CEO 再验证名单与任务状态回写。确认结果在真实 run 日志中出现。

预检文件只放在项目下的临时预检目录，不能覆盖用户文件。若失败，记录 Agent 名称、运行 ID、绝对路径、操作及原始错误；先定位 Codebase、sandbox、工具授权、Windows ACL、执行器或模型连接中哪一层失败，再修复该层。两次相同失败停止自动重试；其他角色继续可独立开展的工作。主机自身能写不代表 Agent 有写权限。只有五个角色分别实跑成功，才能说这些角色的权限已验证。

## 4. 启动 CEO

将 `docs/CEO-启动任务.md` 的内容粘贴到新项目 CEO 的任务中，确认该任务属于新项目并由 CEO 接收。CEO 应先做简要计划及预检，随后安排需求/API、前端、后端和测试并行推进。不要把 CEO 协调入口设成必须等所有子任务完成才能启动。

## 5. 开发、数据库与测试

- 需求/API Agent 依据协议正文和实际表结构形成契约与 mock；前端按契约先开发设备、轨迹和报警的基本页面。
- 后端使用 Netty + Spring Boot + MyBatis-Plus；连接已有 Oracle 11g 表，业务读写获授权；严禁重复建表、DDL 或清库。
- 测试 Agent 使用专用测试终端和限定测试数据，执行协议、200 米边界、API、前端与数据库集成验证。连库故障只阻塞真实数据库验收，其余开发与测试继续。
- 旧密码已出现在聊天记录，环境变量登记不等于轮换。轮换作为单独待办，不强迫无关开发停止；不要把密码复制到代码、任务或日志。

## 6. 检查进度和完成

在 CEO 任务查看角色任务、代码实际位置、构建/测试输出和真实 Oracle 联调结果。最终应有前后端启动说明、源码、模拟终端、测试报告和未解决项；任务 Done 不等于项目完成。没有正式发布包时记录“尚未生成”，准备发布时再检查最终产物；不要等待不存在的包或虚构独立审核。

## 常见故障

- `blocked by unresolved blockers`：检查真正的前置关系，只阻塞受影响子任务；CEO 保持可协调。
- 预算 hard stop 但金额未到：检查待记账/未定价记录和 Agent 暂停原因，避免不断加额度或伪造记账。
- localhost 3100 不通：分别在主机与实际 Agent 环境诊断；协调 MCP 可用时优先使用，避免盲目换端口。
- `approval policy never`：检查实际工具审批与连接权限，不默认全局关闭 sandbox。
- 重复恢复或无进展：同一错误停止自动循环，记录唯一下一步并转给有能力的角色；其他任务继续。