# yvezao 个人学术主页

基于 [academicpages](https://github.com/academicpages/academicpages.github.io) 模板的个人学术主页。
站点最终将部署在 `https://yvezao.github.io`。

---

## 一、如何查看主页（本地预览）

模板是 Jekyll 静态站点，本地预览需要 **Ruby + Bundler + Jekyll**。
当前电脑检测到没有 Ruby，所以有两条路可选：

### 方案 A：安装 Ruby 后本地预览（推荐，可以看到实时刷新）

1. 下载并安装 Ruby（Windows）：
   - 推荐用 [RubyInstaller](https://rubyinstaller.org/downloads/) 的 **Ruby+Devkit** 版本（带 MSYS2）。
   - 安装时勾选 `ridk install` 步骤，一路回车直到安装完成。
2. 安装完成后**重启终端**（PowerShell / Git Bash），验证：
   ```bash
   ruby -v
   gem -v
   ```
3. 进入项目目录，安装依赖：
   ```bash
   cd "C:/shwork_RUC/个人信息/my_web_page"
   bundle install
   ```
4. 启动本地预览：
   ```bash
   bundle exec jekyll serve -l -H 127.0.0.1
   ```
5. 浏览器打开 [http://127.0.0.1:4000](http://127.0.0.1:4000) 即可看到主页。
   修改 `_config.yml` 后需要 Ctrl+C 重启服务；修改 Markdown 文件会自动刷新。

### 方案 B：跳过本地预览，直接部署到 GitHub Pages

省事，但每次修改都得提交到 GitHub 才能看到效果（通常 1–2 分钟）。
**详见第二节**。

### 方案 C：用 Docker 跑（如果你装了 Docker Desktop）

项目里已经有 `Dockerfile` 和 `docker-compose.yaml`，直接：
```bash
docker compose up
```
然后访问 `http://127.0.0.1:4000`。

---

## 二、如何把主页部署到 GitHub 并对外分享

### 第 1 步：在 GitHub 上创建仓库

1. 登录你的 GitHub 账号 `yvezao`（**先改密码**！你刚才在对话里把密码明文发出来了）。
2. 点 [https://github.com/new](https://github.com/new) 新建一个仓库：
   - **Repository name** 必须填：`yvezao.github.io`
   - **Public**（必须公开，GitHub Pages 才免费）
   - **不要**勾选 "Add a README file" / "Add .gitignore" / "Choose a license"
3. 点 Create repository。

### 第 2 步：推送本地代码

回到终端（在项目目录下）：
```bash
cd "C:/shwork_RUC/个人信息/my_web_page"

# 第一次推送前，添加 GitHub 远程仓库
git remote add origin https://github.com/yvezao/yvezao.github.io.git

# 推送主分支
git branch -M main
git push -u origin main
```

> 如果 git 弹出登录窗口，用你**改过的新密码**登录，或者用 Personal Access Token（PAT）。
> 现在 GitHub 已经不支持账号密码推送了，必须用 PAT：
> https://github.com/settings/tokens → 生成一个 `Fine-grained token` 或 `Classic token (repo)`。

### 第 3 步：开启 GitHub Pages

1. 进入 `https://github.com/yvezao/yvezao.github.io/settings/pages`
2. **Source** 选择 `Deploy from a branch`
3. **Branch** 选择 `main`，文件夹 `/ (root)`
4. 点 Save。
5. 等待 1–2 分钟，访问 `https://yvezao.github.io` 即可看到你的主页。

### 之后每次更新

```bash
cd "C:/shwork_RUC/个人信息/my_web_page"
# 修改完文件后：
git add .
git commit -m "说明你改了什么"
git push
```
GitHub 会在 1–2 分钟内自动重新构建站点。

---

## 三、如何手动编辑主页信息

### 必改的两处核心配置

打开 `_config.yml`，修改以下字段：

| 字段 | 含义 | 当前占位 |
|---|---|---|
| `title` | 浏览器标签页标题 | `yvezao / 学术主页` |
| `name` | 全站显示名 | `yvezao` |
| `description` | 网站描述 | `yvezao 的个人学术主页` |
| `url` | 你的站点 URL | `https://yvezao.github.io` |
| `author.name` | 侧边栏姓名 | `yvezao` |
| `author.bio` | 侧边栏一句话简介 | 待填 |
| `author.employer` | 单位 | `Renmin University of China` |
| `author.location` | 所在地 | `Beijing, China` |
| `author.email` | 联系邮箱 | `1371874652@qq.com` |
| `author.github` | GitHub 用户名 | `yvezao` |
| `author.googlescholar` / `orcid` / `zhihu` / `weibo` 等 | 各学术/社交链接 | 空着，按需填 |

> 注意：改 `_config.yml` 后**必须重启 Jekyll 服务**（Ctrl+C 后重新 `bundle exec jekyll serve`）。

### 编辑各个页面

所有页面都是 Markdown 文件，路径如下：

| 文件 | 内容 | 怎么改 |
|---|---|---|
| `_pages/about.md` | 首页（默认也是 About 页） | 直接修改里面的 Markdown 文字 |
| `_pages/cv.md` | CV 页 | 可以改成纯文字版简历，或保留并链接 `files/CV.pdf` |
| `_pages/publications.html` | Publications 列表页 | 一般不用动，列表由 `_publications/` 自动生成 |
| `_pages/talks.html` | Talks 列表页 | 同上 |
| `_pages/teaching.html` | Teaching 列表页 | 同上 |
| `_pages/portfolio.html` | Portfolio 列表页 | 同上 |
| `_data/navigation.yml` | 顶部导航菜单 | 想隐藏某个栏目，注释掉对应条目即可 |

### 添加/删除页面

- 想加一篇文章 → 在 `_posts/` 里新建 `YYYY-MM-DD-标题.md`
- 想加一篇论文 → 在 `_publications/` 里新建 `YYYY-MM-DD-标题.md`
- 想加一个讲座 → 在 `_talks/` 里新建 `YYYY-MM-DD-标题.md`
- 想加一门课 → 在 `_teaching/` 里新建 `学期-课程名.md`
- 想加一个作品 → 在 `_portfolio/` 里新建 `项目名.md`

每个文件的**最上面**是一段 YAML 头（`---` 之间），下面才是 Markdown 正文。
具体格式可以参考模板原始仓库的 [markdown 指南](https://academicpages.github.io/markdown/)。

### 替换头像/简历

- 头像：`images/profile.jpg`（当前用的是你的 `1寸白底-精修.jpg`）。
  如果想换：直接把新照片**覆盖**这个文件，文件名保持不变。
- 简历：`files/CV.pdf`（当前用的是你的 `简历4.pdf`）。
  想换：直接覆盖。

### 修改主题颜色

打开 `_config.yml`，找到 `site_theme`，可选值：
`default` / `air` / `sunrise` / `mint` / `dirt` / `contrast`。

---

## 四、还缺哪些信息（请补给我）

当前主页是占位状态。要把它做成真正的主页，请告诉我以下内容（能给的都给，我一项一项帮你填）：

### 必填（核心身份）
- [ ] **真实姓名**（中英文）—— 显示在侧边栏、首页、各处
- [ ] **英文名 / 拼音**（用于英文场合）
- [ ] **所在院校、专业、年级**（如：人大 经济学院 硕士二年级）
- [ ] **导师姓名**
- [ ] **研究方向 / 研究兴趣**（一段话）
- [ ] **个人简介 / About**（一段自我介绍，200–500 字即可）

### 强烈建议填
- [ ] **教育背景**（本科 / 硕士，时间、学校、专业、GPA 等）
- [ ] **工作 / 实习经历**（如果有）
- [ ] **Google Scholar 链接**（如果已有账号）
- [ ] **ORCID 链接**（如果已有）
- [ ] **知乎 / 微博 / 微信公众号 ID**（可选）

### 选填（有什么填什么）
- [ ] **论文 / 工作论文**（标题、作者、期刊/会议、年份、PDF、链接）
- [ ] **会议演讲 / 报告**（题目、会议、时间、地点）
- [ ] **助教 / 授课经历**
- [ ] **获奖 / 荣誉**
- [ ] **项目 / 代码 / 数据集**（放 Portfolio）
- [ ] **博客 / 随笔**（放 _posts）

---

## 五、目录速查

```
my_web_page/
├── _config.yml            ← 全站配置（改这里改站名、简介、社交链接）
├── _pages/                ← 顶层页面（about, cv, publications, talks 等）
├── _publications/         ← 每篇论文一个 .md
├── _talks/                ← 每个讲座一个 .md
├── _teaching/             ← 每门课一个 .md
├── _portfolio/            ← 每个作品/项目一个文件
├── _posts/                ← 博客文章 YYYY-MM-DD-title.md
├── _data/navigation.yml   ← 顶部导航菜单
├── _includes/             ← 主题片段（一般不用动）
├── _layouts/              ← 页面布局（一般不用动）
├── _sass/                 ← 样式（一般不用动）
├── images/profile.jpg     ← 你的头像
├── files/CV.pdf           ← 你的简历 PDF
└── README.md              ← 本文件
```

---

## 六、常见问题

**Q: 改完文件浏览器没变化？**
- Markdown 改动：等几秒自动刷新。
- `_config.yml` 改动：必须 Ctrl+C 重启 `jekyll serve`。

**Q: 推送到 GitHub 后页面 404？**
- 等 2–3 分钟，GitHub Actions 还在构建。
- 去看仓库的 **Actions** 标签页，有无报错。
- 确认仓库名严格是 `yvezao.github.io`，大小写一致。

**Q: 怎么换主题颜色？**
- 改 `_config.yml` 的 `site_theme`。

**Q: 怎么加中文/英文双语？**
- 这是进阶功能，模板默认单语言。要做双语得改 `_layouts/` 和 `_data/navigation.yml`，到时候告诉我要不要做。

