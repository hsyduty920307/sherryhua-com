# 潇秋木的小宇宙：Hugo + PaperMod 建站说明

这个文件是给小白看的操作说明。当前目录已经放好了 Hugo 项目的基础文件、栏目、示例文章、`robots.txt`、`llms.txt` 和 GitHub Actions 自动部署配置。

## 1. 先安装软件

你需要安装 3 个软件：

1. Git：用来保存版本、上传 GitHub、安装 PaperMod 主题。
2. Hugo Extended：用来生成静态网站。
3. Visual Studio Code：用来编辑文章和配置文件。

在 Windows 上点哪里：

1. 点击开始菜单。
2. 搜索 `PowerShell`。
3. 右键 `Windows PowerShell`，选择“以管理员身份运行”。

复制这条命令：

```powershell
winget install --id Git.Git --exact
winget install --id Hugo.Hugo.Extended --exact
winget install --id Microsoft.VisualStudioCode --exact
```

完成后应该看到：

- 每个软件安装进度到 100%。
- 可能会弹出确认协议，输入 `Y` 回车即可。

如果报错，先检查：

- 你是不是用“管理员身份”打开 PowerShell。
- Windows 是否支持 winget。Windows 11 一般自带；Windows 10 需要从 Microsoft Store 更新“应用安装程序”。

安装完成后，关闭 PowerShell，再重新打开一个普通 PowerShell，运行：

```powershell
git --version
hugo version
code --version
```

应该看到 Git、Hugo、VS Code 的版本号。

## 2. 打开项目目录

点哪里：

1. 打开 VS Code。
2. 点击左上角 `File`。
3. 点击 `Open Folder...`。
4. 选择这个文件夹：

```text
C:\Users\HUA\Documents\Codex\2026-05-11\hugo-papermod-github-pages-sherryhua-com
```

完成后应该看到左侧文件列表里有：

- `hugo.yaml`
- `content`
- `archetypes`
- `layouts`
- `static`
- `.github`

## 3. 安装 PaperMod 主题

在 VS Code 里点哪里：

1. 点击顶部菜单 `Terminal`。
2. 点击 `New Terminal`。
3. 确认终端所在目录就是本项目目录。

复制这几条命令：

```powershell
git init
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive
```

完成后应该看到：

- 新增 `themes/PaperMod` 文件夹。
- 新增 `.gitmodules` 文件。

如果报错，先检查：

- `git --version` 是否正常。
- 网络是否能访问 GitHub。
- 当前终端目录是否是本项目目录。

## 4. 本地预览网站

复制命令：

```powershell
hugo server -D
```

完成后应该看到类似：

```text
Web Server is available at http://localhost:1313/
```

点哪里：

1. 按住 `Ctrl`。
2. 点击终端里的 `http://localhost:1313/`。

你应该看到：

- 首页标题：潇秋木的小宇宙。
- 导航栏：关于、博客、读书、旅行、视频、近况、归档。
- 最新文章列表。

如果报错，先检查：

- `themes/PaperMod` 是否存在。
- `hugo version` 是否正常。
- `hugo.yaml` 是否仍在项目根目录。

停止预览：

```text
在终端按 Ctrl + C
```

## 5. 创建 GitHub 仓库

点哪里：

1. 打开 https://github.com/ 并登录。
2. 右上角点击 `+`。
3. 点击 `New repository`。
4. Repository name 填：`sherryhua-com`
5. 选择 `Public`。
6. 不要勾选 README、.gitignore、license。
7. 点击 `Create repository`。

完成后 GitHub 会显示几段命令。你只需要复制下面这组，把 `你的GitHub用户名` 换成你的真实用户名：

```powershell
git add .
git commit -m "Initial Hugo PaperMod site"
git branch -M main
git remote add origin https://github.com/你的GitHub用户名/sherryhua-com.git
git push -u origin main
```

完成后应该看到：

- GitHub 仓库页面出现所有项目文件。
- `Actions` 页面开始出现一个自动构建任务。

如果报错，先检查：

- GitHub 用户名是否写对。
- 是否已经登录 GitHub。
- 如果提示身份验证，需要按 GitHub 弹窗或浏览器提示完成登录。

## 6. 设置 GitHub Pages 自动部署

点哪里：

1. 进入 GitHub 仓库 `sherryhua-com`。
2. 点击 `Settings`。
3. 左侧点击 `Pages`。
4. `Build and deployment` 里的 `Source` 选择 `GitHub Actions`。
5. 不需要点 Save。

然后点哪里查看部署：

1. 点击仓库顶部 `Actions`。
2. 点击最新的 `Build and deploy Hugo site`。
3. 等它变成绿色。

完成后应该看到：

- 绿色对勾。
- 部署地址通常是 `https://你的GitHub用户名.github.io/sherryhua-com/`，绑定域名后会变成 `https://sherryhua.com/`。

如果报错，先检查：

- `themes/PaperMod` 是否以 submodule 形式提交了。
- `Settings > Pages` 是否选择了 `GitHub Actions`。
- Actions 报错里是否提示某个 YAML 或 Hugo 配置行。

## 7. 绑定 Porkbun 域名 sherryhua.com

先在 GitHub 设置自定义域名：

1. 进入 GitHub 仓库。
2. 点击 `Settings`。
3. 左侧点击 `Pages`。
4. `Custom domain` 填：`sherryhua.com`
5. 点击 `Save`。
6. 等 DNS 生效后，勾选 `Enforce HTTPS`。

再到 Porkbun 设置 DNS：

1. 登录 https://porkbun.com/
2. 进入 `Domain Management`。
3. 找到 `sherryhua.com`。
4. 点击 `Details`。
5. 找到 `DNS Records`，点击编辑。

建议设置这些记录：

```text
类型  主机  内容
A     @     185.199.108.153
A     @     185.199.109.153
A     @     185.199.110.153
A     @     185.199.111.153
CNAME www   你的GitHub用户名.github.io
```

如果 Porkbun 已经有旧的 `A`、`AAAA`、`CNAME` 记录指向别的网站，先删除旧记录，再添加上面的记录。

完成后应该看到：

- `https://sherryhua.com/` 打开你的博客。
- `https://www.sherryhua.com/` 自动跳转到主域名或也能访问。
- GitHub Pages 里 HTTPS 状态变成可用。

如果报错，先检查：

- GitHub 用户名是否写对。
- DNS 是否还没生效，通常需要几分钟到 24 小时。
- 有没有冲突的旧 DNS 记录。

## 8. 以后怎么写新文章

AI、人和人类社会：

```powershell
hugo new content blog/ai-human-society/my-new-post/index.md
```

投资笔记：

```powershell
hugo new content blog/investment-notes/my-investment-note/index.md
```

读书：

```powershell
hugo new content books/book-title/index.md
```

旅行：

```powershell
hugo new content travel/place-or-trip-title/index.md
```

视频：

```powershell
hugo new content --kind video videos/video-title/index.md
```

写完后，把文章头部的：

```yaml
draft: true
```

改成：

```yaml
draft: false
```

然后发布：

```powershell
git add .
git commit -m "Add new post"
git push
```

几分钟后 GitHub Actions 会自动重新部署。
