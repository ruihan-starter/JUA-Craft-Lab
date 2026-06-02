# JUA Craft · GitHub 操作指南
**适用人群：** 第一次用 GitHub，不会写代码  
**目标：** 把你的文件存到 GitHub，随时可以回到任何一个版本

---

## 你需要准备的东西

- 电脑浏览器（手机也可以，但电脑更方便）
- 你的三个文件：
  - `jua_craft_scatter_beautiful.html`
  - `jua_craft_PRD_v0.2_agent.md`
  - `JUA_Craft_PRD_v0.2.docx`

---

## 第一步：注册 GitHub 账号

1. 打开 [https://github.com](https://github.com)
2. 点右上角 **Sign up**
3. 填邮箱、密码、用户名（用户名会出现在你的链接里，建议用 `jua-craft` 或你的名字）
4. 验证邮箱，完成注册

> 已有账号跳过这步。

---

## 第二步：创建仓库（Repository）

仓库就是一个文件夹，专门存你这个项目的所有东西。

1. 登录后，点右上角 **+** 号 → 选 **New repository**
2. 填写：
   ```
   Repository name:  jua-craft
   Description:      JUA Craft 手工艺品展示平台
   Public / Private: 选 Private（只有你能看到）
   ```
3. 勾选 **Add a README file**（这会自动创建一个说明文件）
4. 点绿色按钮 **Create repository**

✅ 仓库创建完成，你会看到一个空文件夹页面。

---

## 第三步：上传文件

### 创建文件夹结构

先建两个文件夹：`prototype` 和 `docs`。

**上传 HTML 原型文件：**

1. 在仓库页面，点 **Add file** → **Upload files**
2. 在页面顶部的路径栏，手动输入：
   ```
   prototype/
   ```
   （这会自动创建 prototype 文件夹）
3. 把 `jua_craft_scatter_beautiful.html` 拖进上传区域
4. 在页面底部 **Commit changes** 区域填写说明：
   ```
   add: scatter canvas prototype v0.2 — one tap to detail, timeline layout
   ```
5. 点 **Commit changes**

**上传 PRD 文件：**

重复以上步骤，这次路径输入 `docs/`，上传：
- `jua_craft_PRD_v0.2_agent.md`
- `JUA_Craft_PRD_v0.2.docx`

Commit 说明写：
```
add: PRD v0.2 — confirmed scatter mode, interaction patterns, design system
```

---

## 第四步：更新 README（可选但推荐）

README 是仓库首页显示的说明，让你或 Claude Code 一眼看到项目状态。

1. 在仓库首页，点 `README.md` 文件
2. 点右上角铅笔图标（Edit）
3. 把内容替换成：

```markdown
# JUA Craft

在非洲淘到的漂亮东西 · Nairobi, Kenya

## 项目简介

JUA Craft 手工艺品牌线上展示平台。
散落画布 + 时间线设计，一次点击看详情。

## 文件结构

prototype/
  jua_craft_scatter_beautiful.html   ← 当前最新原型，直接用浏览器打开

docs/
  jua_craft_PRD_v0.2_agent.md       ← PRD（英文，供 AI agent 执行）
  JUA_Craft_PRD_v0.2.docx           ← PRD（中文，供人阅读）

## 当前版本

v0.2 · 散落模式原型
- 卡牌直接散落在时间线两侧
- 点一下打开详情
- 已售卡牌翻面处理
- 响应式：手机 / 平板 / 电脑全适配

## 联系

jua.nairobi@gmail.com
```

4. 底部填 Commit 说明：`update: README with project structure`
5. 点 **Commit changes**

---

## 第五步：以后怎么用

### 每次做了新版本，上传新文件

1. 进入 `prototype/` 文件夹
2. 点 **Add file** → **Upload files**
3. 上传新的 HTML 文件（**用新文件名**，比如 `jua_craft_v3_with_real_photos.html`）
4. Commit 说明写清楚这个版本做了什么

> ⚠️ **重要：不要覆盖旧文件，用新文件名。** 这样每个版本都保留着，随时可以回去。

### 想回到旧版本怎么办

1. 进入 `prototype/` 文件夹
2. 找到你想要的那个 HTML 文件
3. 点文件名 → 点右上角 **Download** 按钮
4. 下载下来，在浏览器里打开就可以用

### 想让 Claude Code 读取你的项目

把这个仓库地址发给 Claude Code：
```
https://github.com/你的用户名/jua-craft
```
Claude Code 可以直接读取里面的 PRD 和代码，理解你的项目背景，不需要每次重新解释。

---

## Commit 说明怎么写（规范）

好的 Commit 说明让你以后一眼看懂这个版本做了什么：

```
add: 新增某个功能或文件
update: 修改了某个已有的东西
fix: 修复了某个问题
remove: 删除了某个东西
```

**例子：**
```
add: real product photos — buffalo earrings + elephant necklace
update: PRD v0.3 — added comment feature spec
fix: card rotation broken on iPad
remove: folded pile mode (rejected)
```

---

## 你的仓库结构（目标）

```
jua-craft/
│
├── README.md
│
├── prototype/
│   ├── jua_craft_scatter_beautiful.html     ← 当前版本
│   ├── jua_craft_v3_real_photos.html        ← 加入真实产品图后
│   └── jua_craft_v4_airtable.html           ← 接入数据库后
│
└── docs/
    ├── jua_craft_PRD_v0.2_agent.md
    ├── JUA_Craft_PRD_v0.2.docx
    └── github_guide.md                      ← 就是这份文件
```

---

## 遇到问题

**Q：上传时提示文件太大？**  
A：GitHub 单文件限制 100MB，HTML 文件不会超，图片 PNG 也没问题。

**Q：忘记仓库地址？**  
A：登录 GitHub → 右上角头像 → Your repositories → 找 jua-craft。

**Q：能不能让用户直接访问 HTML 页面，不用下载？**  
A：可以，用 GitHub Pages 功能，我们以后再开启。现在阶段先下载本地打开就够了。

---

*这份指南由 Claude 整理，专为 JUA Craft 项目定制。*
