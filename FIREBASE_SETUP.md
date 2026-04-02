# 🎮 Game Arcade - Firebase Setup Guide

## 📋 Firebase 配置步骤

### 第一步：创建 Firebase 项目

1. 访问 https://console.firebase.google.com/
2. 点击"添加项目"或"Create a project"
3. 输入项目名称（如：`game-arcade`）
4. 按照向导完成创建（可以禁用 Google Analytics）

### 第二步：启用认证 (Authentication)

1. 在 Firebase 控制台左侧菜单，点击"Authentication"（构建 → Authentication）
2. 点击"Get started"（开始使用）
3. 启用以下登录方式：
   - **Email/Password**：点击启用，保存
   - **Google**：点击启用，配置项目名称和邮箱，保存

### 第三步：创建 Web 应用并获取配置

1. 点击项目设置（齿轮图标 ⚙️）→ 项目设置
2. 在"您的应用"部分，点击 Web 图标 `</>`
3. 输入应用昵称（如：`Game Arcade Web`）
4. 点击"注册应用"
5. 复制显示的配置信息：

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyC...",           // 你的 API Key
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

### 第四步：设置 Firestore 数据库

1. 在 Firebase 控制台左侧菜单，点击"Firestore Database"（构建 → Firestore Database）
2. 点击"Create database"（创建数据库）
3. 选择"Start in test mode"（以测试模式启动）
   - 注意：测试模式允许所有读写，适合开发。生产环境需要设置安全规则
4. 选择数据库位置（建议选择离用户最近的区域）
5. 点击"Enable"（启用）

### 第五步：更新配置

打开 `index.html` 文件，找到以下部分并替换配置：

```javascript
// ========================================
// TODO: 替换为你的 Firebase 配置
// ========================================
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",                    // 替换
  authDomain: "YOUR_PROJECT.firebaseapp.com", // 替换
  projectId: "YOUR_PROJECT_ID",              // 替换
  storageBucket: "YOUR_PROJECT.appspot.com", // 替换
  messagingSenderId: "YOUR_SENDER_ID",       // 替换
  appId: "YOUR_APP_ID"                       // 替换
};
// ========================================
```

### 第六步：部署和测试

1. 提交并推送更改到 GitHub
2. 访问你的网站
3. 点击"登录 / 注册"按钮
4. 测试注册和登录功能

## 🔒 生产环境安全规则（可选）

如果你计划公开发布，建议设置 Firestore 安全规则：

```javascript
// Firestore Rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      // 用户只能读写自己的数据
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## 📊 功能列表

### ✅ 已实现
- 用户注册（邮箱 + 密码）
- 用户登录（邮箱 + 密码）
- Google 登录
- 用户资料管理
- 分数云端存储
- 跨设备同步

### 🚧 即将添加
- 分数排行榜
- 成就系统
- 用户头像上传
- 好友系统

## 🆘 常见问题

### Q: 为什么要用 Firebase？
A: Firebase 提供免费的后端服务，包括：
- 用户认证
- 实时数据库
- 云端存储
- 托管服务

对于小型游戏平台，Firebase 免费套餐完全够用！

### Q: 测试模式安全吗？
A: 测试模式允许所有人读写数据库，适合开发和测试。
对于公开生产环境，请设置适当的安全规则。

### Q: 如何查看用户数据？
A: 在 Firebase 控制台的 Firestore Database 部分，
可以看到所有用户的数据。

### Q: 支持其他登录方式吗？
A: Firebase 支持多种登录方式：
- Email/Password ✅
- Google ✅
- Facebook
- Twitter
- GitHub
- 手机号码
- 匿名登录

如需添加其他登录方式，参考 Firebase 文档。

## 📝 更新日志

### 2026-04-01
- ✅ 添加 Firebase Authentication
- ✅ 添加 Firestore 数据库
- ✅ 支持 Email/Password 登录
- ✅ 支持 Google 登录
- ✅ 云端分数保存
- ✅ 跨设备同步

---

**需要帮助？**
- Firebase 文档: https://firebase.google.com/docs
- 项目 GitHub: https://github.com/jz/sokoban
