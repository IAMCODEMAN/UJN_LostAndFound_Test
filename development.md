# 🚀 技术架构与开发规范文档

## 1. 技术栈选型 (Technology Stack)

| 维度 | 推荐方案 | 理由 |
| :--- | :--- | :--- |
| **前端框架** | **React (Vite)** | 现代化的开发体验，极速的热更新。 |
| **UI 组件库** | **Ant Design (Antd)** | 国内最成熟的 UI 库，内置完整的表单、上传、模态框等组件。 |
| **样式处理** | **Tailwind CSS** | 原子化 CSS，极大减少 CSS 文件体积，易于微调 UI 细节。 |
| **后端框架** | **Node.js (Express)** | 轻量级、生态丰富，非常适合处理失物招领这种 I/O 密集型应用。 |
| **数据库 ORM** | **Sequelize** | 支持多种数据库，通过模型定义生成 SQL，防止 SQL 注入。 |
| **数据库** | **MySQL 8.0** | 成熟的关系型数据库，支持复杂的关联查询（如用户与贴子）。 |
| **文件存储** | **Multer (本地) / OSS (云端)** | 前期使用 Multer 存储在服务器 `uploads` 目录，后期易迁移。 |

---

## 2. 数据库逻辑模型 (Data Model)
使用 **Sequelize** 定义以下模型，并利用 `sync()` 自动创建表。

*   **User Model:** 包含 `id`, `username`, `password` (需使用 `bcrypt` 加密), `avatar`, `contact`, `role` (admin/user)。
*   **Item Model:** 包含 `id`, `title`, `description`, `type` (ENUM: 'lost', 'found'), `category`, `image_url`, `location`, `contact_info`, `status` (0: 活跃, 1: 已解决), `userId` (关联外键)。

---

## 3. 核心 API 规范
所有接口需遵循 RESTful 规范，返回格式统一为：`{ "code": 200, "data": {}, "msg": "success" }`。

*   **Auth:** `/api/auth/register`, `/api/auth/login` (返回 JWT)。
*   **Items:** 
    *   `GET /api/items`: 支持分页 (`page`, `limit`) 和搜索过滤 (`keyword`, `type`, `category`)。
    *   `POST /api/items`: 发布（需 JWT 验证）。
    *   `PUT /api/items/:id`: 修改状态或内容（仅所有者或管理员）。
*   **Users:** `/api/users/profile` (获取/更新个人资料)。
*   **Admin:** `/api/admin/items/:id` (管理员强制删除)。

---

## 4. 部署方案 (Cloud Deployment)

### 4.1 环境配置
*   **环境变量：** 使用 `.env` 文件管理敏感信息（数据库密码、JWT Secret、云端存储密钥）。
*   **跨域处理：** 后端必须集成 `cors` 中间件，允许前端域名的访问。

### 4.2 云端迁移路径
1.  **数据库：** 本地运行使用 `localhost`，部署时通过环境变量切换至云数据库（如腾讯云/阿里云 RDS）。
2.  **静态资源：** 
    *   **开发环境：** 存放在后端 `public/uploads` 目录下。
    *   **生产环境：** Claude 需预留接口地址前缀配置，以便后续切换到 CDN 或云存储。

---