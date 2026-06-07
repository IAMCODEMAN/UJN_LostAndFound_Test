## 🛠️ 失物招领网站 UI 重构技术规范

### 1. 全局样式变量 (Global Design Tokens)
*   **Color System:**
    *   `--primary`: `#6366F1` (Indigo 500 - 现代感)
    *   `--accent`: `#F59E0B` (Amber 500 - 暖色调提示)
    *   `--bg-gradient`: `linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%)`
    *   `--glass-bg`: `rgba(255, 255, 255, 0.7)`
*   **Border Radius:** 全局统一使用 `12px` 或 `16px` 的大圆角。
*   **Shadows:** 使用三层阴影（Soft Shadows）增加层级感：`0 10px 15px -3px rgba(0,0,0,0.1)`。

---

### 2. 登录页重构指令 (Login Page Refactor)
*   **布局逻辑：** 将容器改为 `display: grid; grid-template-columns: 1fr 1fr;`。
*   **左侧装饰区：** 增加一个带 `background-color: var(--primary)` 的区块，中心放置一个“失物招领”主题的 SVG 矢量插画，并添加渐变叠加效果。
*   **表单卡片：** 
    *   应用 **Glassmorphism (玻璃拟态)**：`backdrop-filter: blur(12px)`。
    *   输入框添加 `transition: all 0.3s ease`，在 `focus` 状态下增加 `ring-offset` 效果。
    *   登录按钮改为宽度 100%，添加 `hover: translateY(-2px)` 的悬停动画。

---

### 3. 首页大厅重构指令 (Dashboard Refactor)
*   **Bento Grid (便当盒布局)：** 将“失物招领”和“寻物启事”两栏改为响应式栅格系统。在大屏下使用 `grid-template-columns: repeat(auto-fill, minmax(300px, 1fr))`。
*   **物品卡片 (Item Card) 升级：**
    *   **图片比例：** 固定 `aspect-ratio: 16 / 9`，图片设置 `object-fit: cover`。
    *   **标签系统：** 使用不同颜色的 Badge（徽章）区分物品类型（如：电子产品-蓝色，生活用品-橙色）。
    *   **信息层级：** 物品名称加粗 (`font-weight: 600`)，位置和时间使用小尺寸灰色字体，并配以微型 Icon (📍, 🕒)。
*   **搜索栏 (Search Bar)：** 将搜索栏从侧边移至顶部中央。改为药丸型（Pill-shaped）设计，背景半透明，鼠标点击后宽度平滑伸展。

---

### 4. 空状态 (Empty State) 与 动画
*   **空状态处理：** 当没有数据时，不要只显示文字。使用一个 `flex-direction: column` 居中的容器，展示一个轻量级的 SVG 动效插画。
*   **微交互：** 为所有交互元素（按钮、卡片）添加 `cursor: pointer` 和 `active: scale(0.95)`。

---
