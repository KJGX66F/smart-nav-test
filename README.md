# 🌐 Smart Nav - 智能多功能响应式导航

一款基于 **Cloudflare Pages + Pages Functions + Workers KV** 构建的免费 Serverless 智能导航网站。

无需服务器、无需 VPS、无需数据库服务器，部署完成后即可拥有属于自己的高颜值导航页，并支持后台动态管理、云端数据同步、自定义区域、批量导入/导出等功能。

---

## ✨ 项目特点

### ☁️ Cloudflare 云端同步

使用 Cloudflare Workers KV 保存网站配置。

管理员修改：

* 网站链接
* 导航区域
* 网站排序
* 自定义壁纸
* 管理员密码

均可保存到云端。

换浏览器、换电脑、换手机访问网站，也可以读取相同的导航数据。

---

### 🧩 自定义导航区域

后台支持自由管理导航区域：

* 新增区域
* 修改区域
* 删除区域
* 修改区域名称
* 设置英文名称
* 修改区域图标
* 修改主题颜色
* 普通卡片 / 整行宽卡片
* 图标模式 / 文字链接模式

无需修改 HTML 源代码。

---

### 🔗 网站动态管理

管理员可以直接在网页后台：

* 添加网站
* 修改网站
* 删除网站
* 调整导航内容
* 自动获取网站图标
* 设置自定义 Font Awesome 图标
* 自动处理 URL
* 自动去除重复网站

适合把网站作为自己的浏览器主页、个人导航站或公共导航页。

---

## 📦 批量导入 / 导出

新版增加完整的网站数据管理功能。

### 支持导入

支持：

* JSON
* CSV
* TSV
* TXT
* 浏览器书签 HTML

也支持直接粘贴：

```text
Google | https://google.com
GitHub | https://github.com
YouTube | https://youtube.com
```

CSV 推荐格式：

```csv
区域,网站名称,英文名称,网址
AI工具,ChatGPT,ChatGPT,https://chatgpt.com
开发工具,GitHub,GitHub,https://github.com
```

---

### 支持三种导入模式

#### 1. 追加并自动去重

将新网站追加到已有区域，并自动过滤重复网址。

#### 2. 替换目标区域

使用导入的网站替换指定区域。

#### 3. 完整恢复

使用 JSON 备份恢复所有导航区域、网站顺序和相关设置。

---

## 📤 数据导出

支持：

### JSON 完整备份

适合：

* 网站升级
* 网站迁移
* Cloudflare 项目迁移
* 数据备份

能够保存区域、网站、排序以及页面配置。

> 出于安全考虑，JSON 导出不会包含管理员密码。

### CSV 网站清单

方便使用 Excel / WPS / Google Sheets 批量整理网站。

### 浏览器书签 HTML

可以导入：

* Chrome
* Edge
* Firefox
* 其他兼容浏览器

---

# 🌍 中英文双语

网站内置中文 / English 双语言模式。

包括：

* 后台菜单
* 导航区域
* 搜索功能
* 网站管理
* 天气信息
* 操作提示

均支持语言切换。

---

# 🌤️ 时间、天气与搜索

首页集成：

* 实时时钟
* 日期
* 动态问候语
* 天气信息
* Google 搜索
* Bing 搜索
* 百度搜索
* GitHub 搜索

可作为浏览器主页或个人工作台使用。

---

# 🎨 个性化外观

支持：

* 日间模式
* 夜间模式
* 自定义全站壁纸
* 多种区域主题颜色
* 响应式布局

电脑、平板、手机均可使用。

---

# 🛡️ 本地容灾

如果 Cloudflare KV 暂时无法访问，前端仍会尝试使用浏览器本地存储保存数据。

因此即使云端同步失败，也不会因为 KV 暂时异常而导致整个导航页面无法使用。

---

# 📂 项目结构

```text
smart-nav-test/
│
├── index.html
├── ads.txt
├── README.md
│
└── functions/
    └── api/
        ├── config.js
        └── links.js
```

其中：

```text
index.html
```

负责导航网站前端。

```text
functions/api/config.js
```

负责读取和保存完整的网站配置。

对应 API：

```text
/api/config
```

KV 数据键：

```text
site_config
```

---

```text
functions/api/links.js
```

主要用于兼容旧版本网站数据。

对应 API：

```text
/api/links
```

KV 数据键：

```text
custom_links
```

---

# 🚀 Cloudflare Pages 部署教程

这是目前最推荐的部署方式。

整个过程不需要购买服务器。

---

## 第一阶段：Fork 或上传代码

可以直接 Fork 本项目，也可以将代码上传到自己的 GitHub 仓库。

⚠️ 文件结构非常重要。

必须保证：

```text
index.html
functions/
```

直接位于 GitHub 仓库根目录。

正确：

```text
/
├── index.html
└── functions/
```

错误：

```text
/
└── smart-nav/
    ├── index.html
    └── functions/
```

Cloudflare Pages Functions 要求 `functions` 位于 Pages 项目的根目录。

---

# 第二阶段：创建 Cloudflare KV 数据库

进入 Cloudflare 控制面板。

找到：

```text
Workers & Pages
```

进入 KV 管理页面并创建一个新的 KV Namespace。

例如命名为：

```text
NAV_DATABASE
```

注意：

> `NAV_DATABASE` 只是数据库名称，可以自行修改。

真正必须保持一致的是后面设置的 **变量名称 `NAV_DB`**。

---

# 第三阶段：创建 Cloudflare Pages 项目

Cloudflare 控制面板进入：

```text
Workers & Pages
```

选择创建新的 Pages 项目，并连接 GitHub。

选择刚刚 Fork 或上传代码的仓库。

生产分支：

```text
main
```

---

## ⚙️ 构建设置

本项目不需要 Node.js，也不需要 npm build。

推荐设置：

```text
Framework preset:
None
```

```text
Build command:
留空
```

```text
Root directory:
留空
```

Root directory 非常重要。

因为：

```text
/functions
```

就在仓库根目录。

如果错误填写其他根目录，Pages Functions 可能无法识别 `/api/config`。

---

## Build Output Directory

如果 Cloudflare 当前界面允许留空，可以直接留空。

如果界面要求必须填写目录，请按照 Cloudflare 当前静态 Pages 项目的提示设置仓库根目录作为静态资源目录。

核心原则只有一个：

> 最终部署内容必须包含根目录的 `index.html`，同时 `/functions` 必须被 Cloudflare Pages Functions 正确识别。

---

# 第四阶段：第一次部署

点击：

```text
Save and Deploy
```

等待 Cloudflare 完成部署。

第一次部署完成后，导航页面通常已经可以正常打开。

但是此时：

> KV 数据库还没有和 Pages Functions 绑定。

所以后台修改内容时可能只能保存在本地，云端同步无法正常工作。

---

# 第五阶段：绑定 KV 数据库

进入刚刚创建好的 Pages 项目。

打开：

```text
Settings
↓
Bindings
↓
Add
↓
KV namespace
```

新增 KV Binding。

---

## ⚠️ 最重要的一步

Variable name 必须填写：

```text
NAV_DB
```

注意：

```text
NAV_DB
```

必须：

* 全部大写
* 中间有下划线
* 不要增加空格
* 不要改成 NAV_DATABASE

因为后端代码使用的是：

```javascript
env.NAV_DB
```

如果填写错误，Cloudflare Function 就无法连接数据库。

---

KV Namespace 选择之前创建的：

```text
NAV_DATABASE
```

最终类似：

```text
Variable name:

NAV_DB


KV namespace:

NAV_DATABASE
```

然后保存。

---

# 第六阶段：重新部署

⚠️ KV Binding 设置完成以后，需要重新部署一次。

进入项目：

```text
Deployments
```

找到最新部署。

执行：

```text
Retry deployment
```

或者重新向 GitHub 提交一次代码。

Cloudflare Pages Git 集成会自动触发新的部署。

---

# ✅ 检查 API 是否正常

部署完成以后，在自己的 Pages 域名后面增加：

```text
/api/config
```

例如：

```text
你的域名/api/config
```

正常情况下第一次打开可能返回：

```json
{}
```

这代表：

✅ Pages Functions 正常
✅ `/api/config` 正常
✅ KV 可以开始存储配置

如果出现：

```text
500
```

通常检查：

```text
NAV_DB
```

是否绑定正确。

---

# 🔐 登录后台

网站默认管理员密码：

```text
admin888
```

进入网站后，双击页面底部版权文字即可触发管理员登录。

输入：

```text
admin888
```

即可进入管理模式。

第一次成功登录以后，建议立即修改管理员密码。

---

# 🔑 修改管理员密码

后台打开设置菜单。

找到：

```text
修改管理员密码
```

输入新的密码并保存。

新密码会随：

```text
site_config
```

保存到 Cloudflare KV。

---

# 🔎 忘记管理员密码怎么办？

进入 Cloudflare KV。

找到当前网站使用的 KV Namespace。

找到：

```text
site_config
```

打开以后，可以看到类似：

```json
{
  "version": 2,
  "wallpaper": "...",
  "adminPwd": "你的密码",
  "sections": []
}
```

其中：

```text
adminPwd
```

就是当前管理员密码。

---

# 🔄 GitHub 修改代码后会自动更新吗？

会。

如果 Cloudflare Pages 使用 GitHub Git Integration 部署，那么：

```text
修改 GitHub
↓
Commit
↓
Cloudflare 自动检测
↓
自动重新部署
↓
网站更新
```

所以以后修改：

```text
index.html
```

或者：

```text
functions/api/config.js
```

提交到生产分支后，Cloudflare Pages 会自动创建新的部署。

---

# ♻️ 老版本无损升级到新版

如果已经部署过旧版 Smart Nav，建议先备份。

### 第一步

进入旧版后台：

```text
网站数据管理
→
JSON 完整备份
```

下载 JSON 文件。

---

### 第二步

保留原来的 Cloudflare KV Namespace。

不要删除数据库。

尤其不要删除：

```text
site_config
custom_links
```

---

### 第三步

更新 GitHub 仓库里的：

```text
index.html
```

以及：

```text
functions/
```

目录。

---

### 第四步

确认原 Pages 项目的 KV Binding 仍然是：

```text
NAV_DB
```

---

### 第五步

重新部署 Pages。

新版代码包含旧数据迁移逻辑，会尝试读取：

```text
/api/links
```

以及浏览器本地旧版导航数据，并转换成新版数据结构。

---

### 第六步

确认数据无误以后，再导出一份新的：

```text
JSON 完整备份
```

作为新版备份。

---

# 💾 推荐升级流程

最安全的方式：

```text
旧版本
   ↓
导出 JSON
   ↓
保留原 KV
   ↓
更新 GitHub 代码
   ↓
确认 NAV_DB
   ↓
重新部署
   ↓
检查网站数据
   ↓
重新导出 JSON
```

这样即使升级过程中出现问题，也可以通过 JSON 文件恢复网站。

---

# ❌ 常见问题

## 1. 网站可以打开，但是无法云端同步

检查：

```text
Settings
→
Bindings
→
KV namespace
```

变量名称是否为：

```text
NAV_DB
```

---

## 2. `/api/config` 显示 404

一般说明：

```text
/functions
```

没有被 Cloudflare Pages Functions 正确识别。

检查 GitHub：

```text
index.html
functions/
```

是否都位于项目根目录。

---

## 3. `/api/config` 显示 500

优先检查 KV Binding。

必须：

```text
NAV_DB
```

---

## 4. 修改 GitHub 后网站没有变化

检查：

```text
Cloudflare Pages
→
Deployments
```

看看是否已经生成新的部署。

同时确认 GitHub 修改的是生产分支：

```text
main
```

必要时执行：

```text
Retry deployment
```

---

## 5. 页面正常但后台修改只在当前浏览器有效

这通常表示：

```text
localStorage
```

正常工作，但 Cloudflare KV 没有成功同步。

检查：

```text
/api/config
```

以及：

```text
NAV_DB
```

KV Binding。

---

# ⚠️ 安全说明

本项目目前属于轻量级个人导航后台。

管理员密码主要用于前端管理界面的访问控制，并不是完整的企业级服务端身份认证系统。

因此建议：

* 用于个人导航站
* 家庭导航站
* 小型共享导航
* 演示项目
* 学习 Cloudflare Pages Functions / KV

如果准备做公开的大型导航平台，建议进一步给 `/api/config` 和其他写入 API 增加真正的服务端身份验证、Token 校验以及请求权限控制。

---

# 🛠️ 技术栈

前端：

```text
HTML5
Tailwind CSS
Vanilla JavaScript
Font Awesome
```

Cloudflare：

```text
Cloudflare Pages
Cloudflare Pages Functions
Cloudflare Workers Runtime
Cloudflare Workers KV
```

无需：

```text
❌ VPS
❌ Linux服务器
❌ Nginx
❌ MySQL
❌ PHP
❌ Node.js服务器
```

---

# 🎯 适合用途

* 浏览器主页
* 私人导航站
* 资源导航网站
* AI 工具导航
* 开发者工具导航
* 公司内部导航
* 常用网站收藏
* 个人工作台
* Cloudflare Serverless 学习项目

---

# ⭐ 支持项目

如果这个项目对你有帮助，欢迎：

```text
⭐ Star
🍴 Fork
📢 分享
```

你可以 Fork 后修改成自己的私人导航网站。


