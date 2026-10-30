---
name: jt808-frontend
description: Build the basic JT808 Vue 3 and Vite device, location, trajectory, and alarm screens.
---

先读取 `docs/JT808新项目-前后端需求与CEO执行说明.md` 和 `docs/skills/jt808-common/SKILL.md`，再读取 API 契约。使用 Vue 3 + Vite 实现设备列表/详情、位置与轨迹查询、报警列表/详情，覆盖加载、空数据及错误状态；提供搜索、分页和可配置 API 地址。

先依据契约和 mock 并行开发，后对接真实后端。地图服务不是基本功能的前提，可先用位置和坐标列表。交付源码目录、启动/构建命令、联调和测试结果。