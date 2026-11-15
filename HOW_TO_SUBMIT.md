# 从本地文件到最终提交：完整操作手册

截止时间 **2026-11-17 23:59（北京时间）**。本文按顺序执行即可，每一步都写明"在哪点、点什么、拿到什么链接"。

---

## 第 0 步：准备（10 分钟，先做完再动手）

需要两个人各自具备：

| 项目 | 要求 |
| --- | --- |
| GitHub 账号 | 两人各一个，记得用户名和邮箱 |
| CSDN 账号 | 两人各一个，并且**已加入课程社区** 2601_FZU-MU_SE |
| 本机 Git | 命令行 `git --version` 有输出即可；没有就装 Git for Windows |
| 队名 | 两人商量一个，后面博客里要填 |

还要确认一件事：**老师给的那个要 Fork 的仓库地址**。

已核实：作业帖 https://bbs.csdn.net/topics/620593436 的正文里**没有贴任何仓库链接**（只有一句 "Fork the repository provided for this assignment"），社区其他帖子也没有。所以这个地址只能从别处拿：

1. 课程 QQ 群 / 微信群 / 课程平台的**公告和置顶消息**（最常见）；
2. 老师上课的 PPT、第一次课的 Git 演示页；
3. 直接问老师或课代表，把帖子里那句英文截图发过去；
4. 问已经交了作业的同学要他们的仓库链接，打开后在页面标题下方看有没有 **"forked from xxx/yyy"**，那个父仓库就是老师的模板。

**如果确认老师确实没提供模板仓库**：自建一个团队仓库即可。评分表只要求"GitHub repository link、≥3 commits、有 PR、有 Release"，没有强制必须是 fork。这种情况下在博客里写一句"课程未提供可 fork 的模板仓库，故由小组新建团队仓库"。不要随便拿别人的仓库冒充老师发的。

> ⚠️ 重要：当前 `address-book-assignment` 里的 git 提交作者是占位的 `Address Book Student <student@example.com>`。这样传上去，GitHub 的 Contributors 会显示成一个陌生账号，老师统计"每人提交数"就对不上。第 2 步会教你怎么用真实账号重做提交。

---

## 第 1 步：建立团队仓库

两种情况，按有无老师模板仓库二选一。

### 情况 A：有老师的仓库 → Fork

1. 浏览器打开老师给的仓库地址（形如 `https://github.com/xxx/address-book`）。
2. 右上角点 **Fork**。
3. Owner 选**你们其中一人**（通常是组长 A），Repository name 保持原名，点 **Create fork**。
4. 现在你有了 `https://github.com/<A的用户名>/address-book`。
5. 进仓库 → **Settings** → 左侧 **Collaborators** → **Add people** → 填队友 B 的用户名 → **Add**，B 去邮箱点接受。

### 情况 B：老师没给模板 → 自建团队仓库

**两种建法，区别在仓库归谁：**

| 方式 | 仓库归属 | 适合 |
| --- | --- | --- |
| 组长个人仓库 + 加 Collaborator | 组长个人账号 | 最快，5 分钟 |
| 建 GitHub Organization，仓库放进组织 | 团队共有 | 更像"团队仓库"，老师观感更好 |

#### B-1 组长个人仓库（最快）

1. 浏览器打开 https://github.com/new
2. **Repository name**：`address-book` 或 `address-book-<队名>`
3. **Description**：`EE308FZ Extreme Programming - Address Book (Team <队名>)`
4. 可见性选 **Public**（**必须 Public**，私有仓库老师打不开，直接没分）
5. **不要勾** "Add a README file"、"Add .gitignore"、"Choose a license"——保持完全空白，否则 push 时会和本地历史冲突
6. 点 **Create repository**
7. 进仓库 → **Settings** → **Collaborators** → **Add people** → 填 B 的用户名 → **Add**
8. B 在邮箱里点 **Accept invitation**

#### B-2 建 Organization（推荐，更正式）

1. 打开 https://github.com/account/organizations/new → 选 **Free** 计划
2. Organization account name 填 `fzu-se-2601-team<组号>`（全局唯一即可）
3. Contact email 填组长邮箱 → **Next** → 可跳过邀请成员 → **Complete setup**
4. 进组织页 → **People** → **Invite member** → 填 B 的用户名 → 角色选 **Member** → 发送
5. B 在邮箱接受邀请
6. 组织页 → **Repositories** → **New repository** → 名字 `address-book` → **Public** → 不勾任何初始化文件 → **Create**
7. 组织 **Settings → Member privileges** 里确认 **Base permissions** 是 `Read` 或 `Write`（Write 才能让两人都 push）

得到仓库地址：`https://github.com/<组织名或用户名>/address-book`

#### B-3 把本地代码推上去

```powershell
cd C:\Users\15750\Documents\deepseek-harness\default-workspace\address-book-assignment
git remote add origin https://github.com/<组织名或用户名>/address-book.git
git push -u origin main
```

> 若前面建仓库时不小心勾了 README，push 会报 `rejected (fetch first)`。解决：
> ```powershell
> git pull --rebase origin main
> git push -u origin main
> ```

#### B-4 加两道"像个团队项目"的设置（可选但加分）

- **保护 main**：仓库 **Settings → Branches → Add branch protection rule** → 填 `main` → 勾 **Require a pull request before merging**。这样必须走 PR，正好对应老师要的 PR 证据。
- **仓库介绍**：仓库首页右侧 About 齿轮 → 填 Description 和 Topics（`software-engineering`、`address-book`、`extreme-programming`）。

### 两人协同的关键提醒

- **提交归属看 email，不看 push 账号**。每人 `git config user.email` 必须是自己 GitHub 账号绑定的邮箱，Contributors 才会显示两个人。
- 如果两人共用一台电脑 push，浏览器授权的是同一个 GitHub 账号，**PR 和 Review 会都算成一个人**。想让 PR 证据真实，最好各自用自己的电脑 / 各自登录自己的账号。
- 建议组长在仓库 README 顶部加一行队名和成员，老师一眼能看出是团队作业。

---

## 第 2 步：把本地代码传上去（关键：用真实身份重做提交）

打开 PowerShell，进入项目目录：

```powershell
cd C:\Users\15750\Documents\deepseek-harness\default-workspace\address-book-assignment
```

### 2.1 清掉占位历史，重新初始化

```powershell
Remove-Item -Recurse -Force .git
git init
git branch -M main
```

### 2.2 两个人各自配置真实身份

**由组长 A 先做**（换成自己的名字和 GitHub 邮箱）：

```powershell
git config user.name "A的真实姓名或GitHub用户名"
git config user.email "A的GitHub邮箱"
```

第一个提交由 A 做：

```powershell
git add index.html styles.css app.js README.md CODE_STANDARDS.md
git commit -m "feat: implement address book base features"
```

记住当前提交数，然后换 B 上场（B 在同一台电脑上操作，改配置即可）：

```powershell
git config user.name "B的真实姓名或GitHub用户名"
git config user.email "B的GitHub邮箱"
git add TEST_PLAN.md blog-template.md CONTRIBUTING.md CHANGELOG.md DELIVERY_CHECKLIST.md
git commit -m "docs: add test plan, code standards and blog template"
```

> 若两人用两台电脑：A 在自己电脑上建仓库并 push，B 用 `git clone` 拉下来，各自 `git config` 后提交、push。
> 想让提交数好看，可以每人再多拆 1~2 个提交（例如 A 再提交一个 `fix:` 的小改动）。**总数必须 ≥ 3，且两个人都有。**

### 2.3 推送到 GitHub

```powershell
git remote add origin https://github.com/<A的用户名>/address-book.git
git push -u origin main
```

第一次 push 会要求登录。推荐用 **GitHub CLI** 或浏览器弹窗授权；如果卡在密码，去 GitHub → Settings → Developer settings → Personal access tokens 生成一个 token 当密码用。

推送成功后，浏览器刷新仓库页面，应该能看到所有文件。

---

## 第 3 步：用分支 + Pull Request 完成剩余功能（这步同时产出 PR 证据）

老师要求"Release a project version and initiate a pull request"，所以要真的开一次 PR。

### 3.1 建功能分支改点东西

```powershell
git checkout -b feature/excel-export
```

随便做一个**真实的小改进**，例如：

- 在导出文件名里加上日期：`星笺联系人-YYYYMMDD.xlsx`
- 或者导出时如果没有任何联系人，给出更明确的提示

改完提交：

```powershell
git add app.js
git commit -m "feat: add date suffix to exported excel filename"
git push -u origin feature/excel-export
```

### 3.2 在 GitHub 上开 PR

1. 回到仓库页面，会看到黄色提示条 **Compare & pull request**，点它。
2. base 选 `main`，compare 选 `feature/excel-export`。
3. 标题写 `feat: 导出文件名增加日期`，描述里写清改动 + 已按 TEST_PLAN 验证。
4. 点 **Create pull request**。
5. 让队友在 **Files changed** 里点 **Review changes** → Approve。
6. 点 **Merge pull request** → **Confirm merge**。

**把这个 PR 的 URL 记下来**，博客里要填。

---

## 第 4 步：创建 Release

1. 仓库首页右侧 **Releases** → **Create a new release**（或地址栏加 `/releases/new`）。
2. **Choose a tag** 输入 `v1.0.0` → 点 **Create new tag: v1.0.0 on publish**。
3. Release title 填 `v1.0.0 星笺联系人管理`。
4. 描述里写功能清单（可直接抄 `CHANGELOG.md`）。
5. 点 **Publish release**。

**记下 Release 的 URL**。

> 如果还想上传视频，可以在 Release 编辑页把 mp4 拖进 "Attach binaries" 区域。

---

## 第 5 步：截图（博客的"Git 贡献证据"和"程序证据"）

用 `Win + Shift + S` 截区域，保存成 PNG，建议放进项目的 `evidence/` 目录后一起 push。

必须有的截图：

| 文件名 | 怎么截 |
| --- | --- |
| `01-home.png` | 应用主界面，有 3~5 个联系人卡片 |
| `02-favorite.png` | 点星标后，"我的收藏"筛选状态 + 左侧计数 |
| `03-methods.png` | 编辑弹窗里，同一个联系人有多条联系方式 |
| `04-excel.png` | 导出的 Excel 用 Excel/WPS 打开的样子（列名完整、每人一行） |
| `05-import.png` | 导入成功后的提示和列表 |
| `06-commit-history.png` | GitHub 仓库 **Commits** 页面 |
| `07-contributors.png` | GitHub 仓库 **Insights → Contributors**，显示两人各自提交数 |
| `08-release.png` | Release 页面 |
| `09-pr.png` | 已合并的 PR 页面 |

**Contributors 页面是"每人提交数"的官方证据**，这张图老师一定会看，务必截到两个人的头像和数字。

---

## 第 6 步：录完整演示视频

老师要求 "complete demonstration video"，不是几张截图。

### 6.1 用什么录

- Windows 自带：`Win + G` 打开 Xbox Game Bar → 点录制。最简单，不用装东西。
- 或用 OBS Studio（更清晰，能录指定窗口）。

### 6.2 录什么（照着念，2~4 分钟）

1. 打开应用，说明"这是我们的地址簿，数据存在浏览器本地"。
2. 新建联系人「林晓」，公司「星河科技」，职位「产品经理」。
3. 点「＋ 添加联系方式」，加**手机、邮箱、微信**三条 → 保存。
4. 再建一位联系人 → 展示卡片列表。
5. 点星标收藏 → 点左侧「我的收藏」→ 只剩收藏的人，计数变化。
6. 在搜索框输入姓名/电话 → 列表实时过滤。
7. 点「编辑」改职位 → 保存 → 卡片更新。
8. 点「导出 Excel」→ 打开下载的文件 → 指出列名和"一人一行"。
9. 删除一个联系人 → 再「导入 Excel」把刚才的文件导回来 → 数据恢复。
10. 按 F5 刷新 → 数据还在（证明持久化）。

### 6.3 上传拿链接

- **B站**：投稿 → 自制 → 上传 → 标题写清课程作业 → 发布后复制 BV 链接。可以设"仅通过链接访问"。
- 或 **GitHub Release 附件**：把 mp4 拖进 Release 编辑页的 Attach binaries。
- 别用网盘链接（老师可能打不开、要登录）。

---

## 第 7 步：可选加分 —— 公网部署（+15 分）

老师原话："deploy to a cloud server, such as Huawei Cloud or Alibaba Cloud"。`localhost` 不算。

### 方案 A：GitHub Pages（10 分钟，免费）

1. 仓库 → **Settings** → 左侧 **Pages**。
2. Source 选 **Deploy from a branch**，Branch 选 `main`，目录选 `/ (root)`，点 **Save**。
3. 等 1~2 分钟，页面顶部出现 `https://<用户名>.github.io/address-book/`。
4. 打开验证功能正常。

> 这是公网可访问的链接，但不是"华为云/阿里云"。**先问老师是否认可**；不认可就走方案 B。

### 方案 B：阿里云/华为云学生机（约 10~40 元/月）

1. 买一台最低配 ECS（1核2G 足够），系统选 Ubuntu 22.04。
2. 安全组放行 **80** 端口。
3. SSH 登录后装 nginx：

```bash
sudo apt update && sudo apt install -y nginx
```

4. 把 `index.html`、`styles.css`、`app.js` 传到 `/var/www/html/`（用 `scp` 或 WinSCP）：

```bash
scp index.html styles.css app.js root@<公网IP>:/var/www/html/
```

5. 浏览器访问 `http://<公网IP>/` 验证。

**记下公网 URL**，博客"Project links"里填。

---

## 第 8 步：写并发布 CSDN 博客

### 8.1 填模板

打开 [blog-template.md](blog-template.md)，把所有 `【】` 占位符替换成真实内容：

- 队名
- GitHub 仓库链接
- Code Standards 链接（`.../blob/main/CODE_STANDARDS.md`）
- Release 链接、PR 链接
- 公网 URL（有就填，没有写"未申请加分项"）
- 视频链接
- 两位成员姓名
- 两处"提交数"
- 两张 PSP 表的真实数字（估时/实际耗时）
- 贡献比例（合计 100%）

### 8.2 图片怎么进博客

CSDN 编辑器支持直接**拖拽图片**进正文，会自动上传到 CSDN 图床并生成链接。把 `evidence/` 里的 PNG 拖到对应小节即可，不要用本地路径 `evidence/01.png`（读者打不开）。

### 8.3 发布

1. 登录 CSDN → 右上「创作中心」→「写文章」。
2. 编辑器右上角切到 **Markdown** 模式。
3. 粘贴填好的全文。
4. 右侧填：标题、分类专栏（选课程相关）、标签（`软件工程`、`极限编程`、`Git`）。
5. 点 **发布文章**。

> ⚠️ CSDN 发布后可能进审核，**不要拖到 11-17 晚上才发**。今明两天就发掉。

### 8.4 两人各发一篇

老师明确要求 "each student must publish an individual blog as their own assignment record"。所以 A、B 各发一篇，内容可以是同一份文档，但**各自账号发布、各自有自己的链接**。

---

## 第 9 步：提交博客链接（最后一步）

1. 浏览器打开作业帖：https://bbs.csdn.net/topics/620593436
2. 确认已登录，且**已加入**课程社区 2601_FZU-MU_SE（右上「+ 加入社区」）。
3. 页面底部有 **「提交任务」** 按钮（帖子下方显示"0人已提交 / 完成率0%"那块）。
4. 点进去 → 粘贴**你自己那篇博客的 URL** → 提交。
5. 两人分别提交各自的那篇。

提交后回到帖子，应该能看到自己的提交记录。

---

## 时间安排建议（今天是 11-15）

| 时间 | 做什么 |
| --- | --- |
| 今天下午 | 第 0~2 步（Fork、建仓库、用真实身份推代码） |
| 今天傍晚 | 第 3~4 步（分支、PR、Release），第 5 步截图 |
| 今天晚上 | 第 6 步录视频并上传 |
| 明天上午 | 第 7 步部署（可选）、第 8 步写博客 |
| 明天下午 | 两人各发博客，第 9 步提交链接，留出审核时间 |

---

## 常见卡点

**push 时提示 `remote: Permission denied`**
→ 你是用别人的账号登录的。去 Windows 凭据管理器删掉 `git:https://github.com` 那条，重新登录。

**Contributors 只显示一个人**
→ 另一个人的 `git config user.email` 不是 GitHub 账号绑定的邮箱。用 `git log --format='%an <%ae>'` 检查，改配置后重做提交（可以 `git commit --amend --reset-author`）。

**导出的 Excel 打不开**
→ 应用依赖 CDN 上的 SheetJS。断网时会失败，演示时保证联网，或把 `xlsx.full.min.js` 下载到本地并改 `index.html` 的 `<script src>`。

**老师仓库找不到**
→ 作业帖只写了 "the repository provided for this assignment"，具体地址在群公告。直接问老师或课代表，别猜。
