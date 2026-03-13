# Firebase 同步配置说明

## 概述

应用已接入 Firebase Realtime Database 实现跨设备数据同步。手机版和网页版的数据会自动实时同步。

## 配置步骤

### 1. 创建 Firebase 项目

1. 访问 [Firebase Console](https://console.firebase.google.com/)
2. 点击「创建项目」
3. 输入项目名称（如 `time-assistant`）
4. 关闭 Google Analytics（可选）
5. 点击「创建项目」

### 2. 创建 Realtime Database

1. 在项目左侧菜单选择「Realtime Database」
2. 点击「创建数据库」
3. 选择数据库位置（选择离你近的，如 `asia-southeast1`）
4. 安全规则选择「以锁定模式开始」
5. 点击「启用」

### 3. 修改安全规则

1. 在数据库页面点击「规则」标签
2. 将规则修改为以下内容：

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "auth != null && auth.uid == $uid",
        ".write": "auth != null && auth.uid == $uid"
      }
    }
  }
}
```

3. 点击「发布」

### 4. 启用匿名登录

1. 在左侧菜单选择「Authentication」
2. 点击「开始使用」
3. 选择「匿名」登录方式
4. 启用开关
5. 点击「保存」

### 5. 获取配置信息

1. 在项目概览页面点击齿轮图标 ⚙️ → 「项目设置」
2. 在「常规」标签页下找到「您的应用」部分
3. 点击「添加应用」→ 「Web」图标 `</>`
4. 输入应用昵称（如 `time-assistant-web`）
5. 点击「注册应用」
6. 复制 firebaseConfig 对象中的值

### 6. 更新代码中的配置

打开 `index.html` 文件，找到第 782-790 行的 `firebaseConfig`，替换为你的配置：

```javascript
const firebaseConfig = {
    apiKey: "你的_apiKey",
    authDomain: "你的_projectId.firebaseapp.com",
    databaseURL: "https://你的_projectId-default-rtdb.firebaseio.com",
    projectId: "你的_projectId",
    storageBucket: "你的_projectId.appspot.com",
    messagingSenderId: "你的_messagingSenderId",
    appId: "你的_appId"
};
```

## 使用说明

### 首次使用

1. 在手机浏览器打开网页
2. 等待显示「同步服务已连接」提示
3. 添加一些任务或日程
4. 在电脑浏览器打开同一网页
5. 数据会自动同步显示

### 离线使用

- 没有网络时会自动切换到本地模式
- 联网后会自动将本地数据同步到云端
- 支持离线添加/修改数据

### 多设备同步

- 同一用户在不同设备上的数据会实时同步
- 在一台设备上添加任务，另一台设备会立即显示
- 使用匿名登录，不需要输入账号密码

## 注意事项

1. **浏览器隐私模式**：隐私模式下 localStorage 可能不可用，建议使用正常模式
2. **清除浏览器数据**：清除浏览数据会同时清除本地缓存，但云端数据不受影响
3. **不同浏览器**：每个浏览器会生成不同的匿名用户ID，数据不会自动互通
   - 解决方案：在常用浏览器之间选择同一个作为主要使用

## 费用说明

Firebase Spark 计划（免费）包含：
- Realtime Database: 1GB 存储，10GB/月 下载流量
- 匿名认证: 50,000 用户/月

对于个人使用完全足够。
