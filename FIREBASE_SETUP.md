# Firebase 同步配置指南

## 快速开始（3 分钟完成）

### 第一步：创建 Firebase 项目

1. 访问 [Firebase Console](https://console.firebase.google.com/)
2. 点击「创建项目」
3. 输入项目名称，例如：`time-assistant-sync`
4. 关闭 Google Analytics，点击「创建项目」

### 第二步：创建数据库

1. 点击左侧菜单「Realtime Database」
2. 点击「创建数据库」
3. 选择位置：选离你最近的，如 `asia-southeast1`（新加坡）
4. 安全规则选择「以测试模式开始」
5. 点击「启用」

### 第三步：启用匿名登录

1. 点击左侧菜单「Authentication」→「开始使用」
2. 选择「匿名」登录方式
3. 打开开关，点击「保存」

### 第四步：获取配置信息

1. 点击左上角齿轮图标 ⚙️ →「项目设置」
2. 在「常规」标签页，点击「添加应用」→「</>」（Web 图标）
3. 输入应用昵称：`time-assistant`
4. 点击「注册应用」
5. 复制 `firebaseConfig` 代码块

### 第五步：填入配置

打开 `index.html`，找到第 782-790 行：

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

替换为你刚才复制的配置。

### 第六步：保存并刷新页面

保存文件，刷新浏览器，你会看到提示「已连接云端，数据将自动同步」。

---

## 多设备同步

配置完成后：
1. 在手机浏览器打开同一个网页
2. 填入相同的 Firebase 配置
3. 两个设备的数据会自动同步

---

## 常见问题

### 配置后没有同步？

1. 打开浏览器控制台（按 F12）
2. 查看是否有红色错误信息
3. 确认 `apiKey` 不是 `YOUR_API_KEY`

### 不想用云端了？

将配置改回：
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    // ... 其他保持不变
};
```

应用会自动切换到本地模式。

---

## 安全提醒

**不要**将填好真实 API Key 的代码提交到公开 GitHub 仓库！

建议：
- 使用 `.gitignore` 忽略配置文件
- 或使用环境变量（需要构建工具）
