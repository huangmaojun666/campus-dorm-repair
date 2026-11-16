# 校园宿舍报修与维修服务管理系统

面向住宿学生、宿舍管理员和维修人员，提供报修提交、审核派单、维修跟踪、完工验收和返修服务，使每张工单的处理过程可查询、可追溯。

## 项目目标与角色

以一个校区的宿舍维修业务为范围，管理房间及公共区域的水电、门锁、设施故障，记录处理人、处理时间和维修结果。

| 角色 | 主要功能 |
| --- | --- |
| 学生 | 提交故障描述及照片、查看进度、确认维修结果、申请返修、评价 |
| 宿舍管理员 | 管理楼栋与房间、审核报修、派单和改派、跟踪超时工单、查看统计 |
| 维修人员 | 查看分配的工单、接单、更新维修进度、上传维修结果 |

业务流程初稿为“提交报修 → 管理员受理与派单 → 维修人员接单与处理 → 学生验收 → 完成”。验收未通过时记录原因并进入返修流程。权限同时按角色、所管楼栋和工单归属限制。

## 技术栈

采用前后端分离架构，一个 GitHub 仓库管理全部项目资料。后端采用单体应用，前后端通过 REST API 交换 JSON 数据。

| 部分 | 技术选择 |
| --- | --- |
| 后端 | Java 21、Spring Boot 4.0.x、Maven 3.9.x |
| 数据访问 | MyBatis-Plus 3.5.x，使用 Spring Boot 4 专用 Starter |
| 数据库 | MySQL 8.4 |
| 登录与权限 | Spring Security，基于 Session 的登录认证和角色权限控制 |
| 前端 | Vue 3、TypeScript、Vite |
| 前端配套 | Element Plus、Vue Router、Pinia、Axios |
| 前端环境 | Node.js 24 LTS（24.12 或更高的 24.x 版本）、npm |
| 文件与通知 | 报修照片存储在后端可配置目录，通过第三方邮件服务发送派单和完工通知 |
| 测试与协作 | Spring Boot Test、Vitest、GitHub Issues、Pull Requests、GitHub Actions |

Spring Boot 提供接口、校验和权限支持，MySQL 保存工单及处理记录。Vue 和 Element Plus 支撑表单、工单列表和管理页面。工程初始化时在 `pom.xml` 和 `package-lock.json` 中锁定具体依赖版本。

技术依据见 [Spring Boot 环境要求](https://docs.spring.io/spring-boot/4.0/system-requirements.html)、[MyBatis-Plus 安装说明](https://baomidou.com/getting-started/)和 [Vue 项目创建指南](https://vuejs.org/guide/quick-start)。

## 仓库结构

```text
campus-dorm-repair/
├── .github/
│   ├── ISSUE_TEMPLATE/       # 用户故事、缺陷和任务模板
│   ├── workflows/            # 后续添加构建、测试与部署流程
│   └── pull_request_template.md
├── backend/                  # Java 后端工程及后端测试
├── frontend/                 # Vue 前端工程及前端测试
├── database/                 # 建表、变更和演示数据 SQL
├── docs/
│   ├── research/             # 调研计划、访谈纪要、问卷、竞品分析和调研报告
│   ├── requirements/         # 用户故事汇总、SRS、需求追溯矩阵和变更记录
│   ├── design/               # 概要/详细设计、API 文档、架构决策和评审记录
│   ├── testing/              # 测试计划、验收用例和测试报告
│   ├── iterations/           # 团队分工、迭代计划和回顾
│   ├── deployment/           # 部署与演示说明
│   └── ai/                   # AI 使用记录和使用报告
├── models/                   # 用例图、类图、状态图等模型源文件与导出图
├── .gitignore
└── README.md
```

空目录中的 `.gitkeep` 用于保留目录结构。第一周的调研计划放在 `docs/research/`，团队成员与分工放在 `docs/iterations/`，选题说明提交为 GitHub Issue。

工程初始化后，后端按 `controller`、`service`、`mapper`、`entity`、`dto`、`config` 分层，测试放在 `src/test/`。前端按 `views`、`components`、`api`、`router`、`stores`、`types` 组织，页面按报修、派单、维修等业务模块划分。

## GitHub 协作

需求、缺陷和任务先建 Issue，再从 `main` 创建工作分支。完成后 push 工作分支，提交关联 Issue 的 PR。每个 Issue 分配负责人并归入对应 Milestone。

GitHub 分支保护应配置为 `main` 通过 PR 合并，至少一位成员评审通过。工程初始化时配置 Actions 构建与测试，并将检查通过设为合并条件。

本地配置使用环境变量或被忽略的本地配置文件，仓库保留配置示例。AI 辅助产出在 PR 中说明用途、涉及文件和人工验证情况，并汇总到 `docs/ai/`。
