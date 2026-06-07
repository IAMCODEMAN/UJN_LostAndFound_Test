# 🚀 UJN - Lost & Found

---

>  UJN - Lost & Found——
> 
> 一个济南大学校园失物招领项目
>
## 项目结构

```
UJN - Lost & Found/
├─ client/                 前端 Vite + React 项目
│  ├─ public/              静态资源：logo、背景图、favicon
│  ├─ src/
│  │  ├─ api/              axios 请求封装和接口模块
│  │  ├─ assets/           前端资源
│  │  ├─ components/       通用组件
│  │  ├─ contexts/         Auth / Theme 等全局状态
│  │  ├─ pages/            页面：主页、登录、注册、发布、用户中心、管理页
│  │  ├─ App.jsx           路由和应用主体
│  │  └─ main.jsx          React 入口
│  ├─ package.json
│  └─ vite.config.js
│
├─ server/                 后端 Express API
│  ├─ config/              数据库配置
│  ├─ middleware/          auth/admin 中间件
│  ├─ models/              Sequelize 模型：User、Item
│  ├─ routes/              API 路由：auth、items、users、admin
│  ├─ utils/               响应工具
│  ├─ app.js               后端入口
│  ├─ .env.example         环境变量模板
│  └─ package.json
│
├─ package.json            根目录依赖文件，但没有启动脚本
├─ development.md          技术方案文档
├─ PRDs.md / UI*.md        产品和 UI 设计文档
└─ logo.png / backUjnImg.jpg
```

>
|             | 技术栈                        | 简介                                     |
|:------------|:---------------------------|:---------------------------------------|
| **前端框架**    | **React (Vite)**           | 实现现代化的开发体验，极速的热更新。                     |
| **UI 组件库**  | **Ant Design (Antd)**      | 使用成熟的 UI 库，内置完整的表单、上传、模态框等组件。          |
| **样式处理**    | **Tailwind CSS**           | 原子化 CSS，极大减少 CSS 文件体积，易于微调 UI 细节。      |
| **后端框架**    | **Node.js (Express)**      | 轻量级、生态丰富，非常适合处理失物招领这种 I/O 密集型应用。       |
| **数据库 ORM** | **Sequelize**              | 支持多种数据库，通过模型定义生成 SQL，防止 SQL 注入。        |
| **数据库**     | **MySQL 8.0**              | 成熟的关系型数据库，支持复杂的关联查询（如用户与贴子）。           |
| **文件存储**    | **Multer (本地) / OSS (云端)** | 前期使用 Multer 存储在服务器 `uploads` 目录，后期易迁移。 |

---

## 本地开发运行方式：

> 1. 安装环境：
> MySQL 8.0
> 
> Node.js
>
> 3. 配置数据库:
> 登录 MySQL：
> ```powershell
> mysql -u root -p
> ```
> 创建数据库：
> ```sql
> CREATE DATABASE lost_found CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
> ```
> 
> 3. 配置后端环境变量：
> ```powershell
> cd server
> ```
> 
>   复制 .env.example文件, 配置 server/.env
> 
> 如：
>```env
> DB_HOST=localhost
> DB_PORT=3306
> DB_USER=root
> DB_PASS=你的MySQL密码
> DB_NAME=lost_found
> JWT_SECRET=your_jwt_secret
> JWT_EXPIRES_IN=7d
> PORT=3001
> UPLOAD_DIR=public/uploads
> CORS_ORIGIN=http://localhost:5173
>```
>
> 4. 安装并启动后端
> ```powershell
> cd server
> npm install
> npm run dev
> ```
> 后端默认运行在 http://localhost:3001
> 
> 5. 安装并启动前端
> 另开一个终端，从项目根目录执行
> ```powershell
> cd client
> npm install
> npm run dev
> ```
> // 前端默认运行在 http://localhost:5173 
> // 前端代理配置于 client/vite.config.js
> 
