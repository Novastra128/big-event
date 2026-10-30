# Big-Event 文章管理系统

> 基于 SpringBoot3 + Vue3 的前后端分离实战项目（黑马程序员课程案例）
> 课程地址：https://www.bilibili.com/video/BV14z4y1N7pg

## 项目简介

Big-Event 是一个模拟"新闻发布系统"的企业级全栈项目，采用前后端分离架构，
后端提供 RESTful API，前端使用 Vue3 构建管理界面。项目覆盖了从需求分析、
接口设计、开发实现到部署上线的完整流程，是 Java 全栈入门的优质练手项目。

### 功能模块

| 模块     | 功能点                                                       |
| -------- | ------------------------------------------------------------ |
| 用户管理 | 注册、登录（JWT）、信息修改、头像上传（阿里云 OSS）、修改密码 |
| 文章分类 | 新增、编辑、删除、查询分类                                   |
| 文章管理 | 发布、编辑、删除、分页查询（PageHelper）、条件搜索           |
| 登录优化 | Redis 存储 Token，实现密码修改后旧 Token 主动失效            |

## 版本锁定（本课程环境基准，新环境按此对照）

### 基础环境
| 组件    | 版本          | 备注                                |
| ------- | ------------- | ----------------------------------- |
| JDK     | 17.0.x（LTS） | SpringBoot3 最低要求 17             |
| Maven   | 3.9.6         | 不要用 Maven 4.x，IDEA 导入器不兼容 |
| MySQL   | 8.x           |                                     |
| Redis   | 7.x           |                                     |
| Node.js | 16+           | 前端用                              |

### 后端依赖（big-event-backend）
| 依赖       | 坐标                                      | 版本         | 备注                              |
| ---------- | ----------------------------------------- | ------------ | --------------------------------- |
| SpringBoot | `spring-boot-starter-parent`              | **3.5.16**   | 3.x 收官版，勿用 4.x / 3.0.x      |
| MyBatis    | `mybatis-spring-boot-starter`             | **3.0.5**    | Boot3 必须配 3.x，勿用 2.x        |
| MySQL 驱动 | `mysql-connector-j`                       | 由 Boot 管理 | runtime scope                     |
| 分页       | `pagehelper-spring-boot-starter`          | **2.1.0**    | 对应 Boot3                        |
| JWT        | `jjwt-api` / `jjwt-impl` / `jjwt-jackson` | **0.12.6**   | 0.12 写法与 0.9 差异大            |
| 参数校验   | `spring-boot-starter-validation`          | 由 Boot 管理 |                                   |
| 缓存       | `spring-boot-starter-data-redis`          | 由 Boot 管理 |                                   |
| 工具       | `lombok`                                  | 由 Boot 管理 | IDEA 需装 Lombok 插件（新版内置） |

### 前端依赖（big-event-frontend）
| 依赖         | 版本                            |
| ------------ | ------------------------------- |
| Vue          | 3.4+                            |
| Vite         | 5.x                             |
| Vue Router   | 4.x                             |
| Pinia        | 2.x（+ pinia-persistence 插件） |
| Element Plus | 2.x                             |
| Axios        | 1.x                             |

> 更新原则：跟教程学习期间锁死上表版本；教程完结后再自行升级并单独验证。

## 技术栈

### 后端（big-event-backend）
- **框架**：SpringBoot 3.x（JDK 17）
- **构建工具**：Maven 3.8+
- **持久层**：MyBatis + MySQL 8
- **缓存**：Redis（登录 Token 管理）
- **认证**：JWT（jjwt）
- **参数校验**：Validation（@Validated）
- **工具**：Lombok、PageHelper 分页插件
- **对象存储**：阿里云 OSS（图片上传）

### 前端
- **框架**：Vue 3（组合式 API）
- **路由**：Vue Router
- **状态管理**：Pinia（+ 持久化插件）
- **UI 组件库**：Element Plus
- **HTTP 请求**：Axios
- **构建工具**：Vite

### 开发环境
- JDK 17 / Node.js 16+ / MySQL 8 / Redis 7
- IDE：IntelliJ IDEA（后端）/ VS Code（前端）
- 接口调试：Postman
- 版本控制：Git + GitHub

## 模块规划（目录结构）

```text
big-event/
├── big-event-backend/ # 后端工程
│ ├── src/main/java/
│ │ └── com.<你的包名>.bigevent/
│ │ ├── controller/ # 控制层（接口）
│ │ ├── service/ # 业务层
│ │ ├── mapper/ # 数据访问层
│ │ ├── pojo/ # 实体类
│ │ ├── utils/ # 工具类（JwtUtil、AliOssUtil 等）
│ │ ├── interceptor/ # 登录拦截器
│ │ ├── advice/ # 全局异常处理
│ │ └── config/ # 配置类
│ └── src/main/resources/
│ ├── application.yml # 核心配置
│ └── mapper/ # MyBatis XML（可选）
├── big-event-frontend/ # 前端工程（Vue3）
│ ├── src/
│ │ ├── api/ # 接口封装
│ │ ├── assets/ # 静态资源
│ │ ├── components/ # 公共组件
│ │ ├── views/ # 页面
│ │ ├── router/ # 路由
│ │ ├── stores/ # Pinia 仓库
│ │ └── main.js
│ └── …
├── resources/ # 资料（SQL 脚本、接口文档等）
└── README.md

```



## 快速开始

### 环境准备
1. 本地安装并启动 MySQL 8 和 Redis
2. 执行数据库脚本：`resources/big_event.sql`
3. 修改 `application.yml` 中的数据库 / Redis 连接信息

### 后端启动

```bash
cd big-event-backend
mvn spring-boot:run
```

默认端口：`8080`（可自行修改）

### 前端启动

```bash
cd big-event-frontend
npm install
npm run dev
```

## 学习路线 / 进度

- [x] 项目初始化、工程搭建
- [ ] 基础篇：配置读取、MyBatis 整合
- [ ] 实战篇：用户注册 / 登录（JWT + Redis）
- [ ] 文章分类管理
- [ ] 文章管理（分页 + 条件查询）
- [ ] 头像上传（阿里云 OSS）
- [ ] 前端整合、部署上线

## 作者

- 学员：Novastra（软件工程在读，目标方向：Java 全栈 + AI 应用）
- 课程来源：黑马程序员 SpringBoot3 + Vue3

> 本项目为个人学习项目，用于巩固 SpringBoot3 / Vue3 全栈开发技能。