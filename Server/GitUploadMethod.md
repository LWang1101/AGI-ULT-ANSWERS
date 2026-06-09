以下是将内容转换为 Markdown 格式：

```markdown
# 使用 GitHub 备份代码的详细步骤

GitHub 配合 Git 是一个强大的版本控制工具，可以帮你记录代码的每次修改、回溯历史版本，甚至多人协作。以下是详细步骤，假设你是初次使用 GitHub 备份代码，我会从头讲起，确保你能顺利操作你的项目（比如 BODE-GEN.py 等）。

## 前提准备

### 安装 Git

- 检查是否已安装：
  ```bash
  git --version
  ```

- 如果没安装，在你的系统上安装：
  - Linux：`sudo apt install git`（Ubuntu/Debian）或 `sudo yum install git`（CentOS）。
  - macOS：`brew install git`（需先装 Homebrew）。
  - Windows：下载安装 Git for Windows（[下载地址](https://git-scm.com/download/win)）。

### GitHub 账户

确保你有 GitHub 账户（github.com），如果没有，注册一个。

### 代码目录

假设你的代码在 `/data1/leihanwa/secret/`（包含 BODE-GEN.py 等）。

## 步骤：用 GitHub 备份代码

### 1. 初始化本地 Git 仓库

进入你的代码目录：
```bash
cd /data1/leihanwa/secret
```

初始化 Git 仓库：
```bash
git init
```
这会在目录下创建一个 .git 文件夹，用于跟踪版本。

### 2. 添加代码到暂存区

添加所有文件：
```bash
git add .
```

或者只添加特定文件：
```bash
git add BODE-GEN.py LLM_Eval_Utils.py
```

检查状态：
```bash
git status
```
应该看到添加的文件列表。

### 3. 提交第一个版本

提交更改到本地仓库：
```bash
git commit -m "Initial commit: Add BODE-GEN.py and related files"
```
`-m` 后的消息是这次提交的描述，比如“初始提交”。

### 4. 创建 GitHub 远程仓库

- 登录 GitHub（github.com）。
- 点击右上角 “+” -> “New repository”。
- 填写：
  - Repository name：比如 BODE-GEN（随便起名）。
  - Public/Private：选 Private（私密，只有你和邀请的人可见）或 Public（公开）。
  - Initialize with README：不要勾选（因为你已有本地代码）。
- 点击 “Create repository”。
- 复制仓库的 URL：
  - 格式如：https://github.com/你的用户名/BODE-GEN.git。

### 5. 连接本地仓库到 GitHub

在本地添加远程仓库：
```bash
git remote add origin https://github.com/你的用户名/BODE-GEN.git
```
替换 `你的用户名` 和 `BODE-GEN` 为实际值。

验证连接：
```bash
git remote -v
```
应该看到 `origin` 指向你的 GitHub URL。

### 6. 推送代码到 GitHub

推送本地代码到远程：
```bash
git push -u origin master
```
提示输入账号密码：输入你的 GitHub 用户名和 Personal Access Token（PAT，见下文）。

`-u` 设置默认分支，之后可直接用 `git push`。

#### 生成 PAT（如果需要）

- GitHub -> Settings -> Developer settings -> Personal access tokens -> Tokens (classic)。
- 点击 “Generate new token”。
- 勾选 `repo` 权限，生成并复制 token（类似 `ghp_xxxxxxxxxxxxxxxx`）。
- 推送时用这个 token 代替密码。

### 7. 备份后续版本

每次修改代码后：

添加更改：
```bash
git add .
```

提交新版本：
```bash
git commit -m "Update: Modify BODE-GEN.py for BO optimization"
```
描述清楚这次改了什么。

推送备份：
```bash
git push
```

## 完整示例

假设你的代码在 `/data1/leihanwa/secret`，GitHub 仓库是 `https://github.com/leihanwa/BODE-GEN.git`：
```bash
cd /data1/leihanwa/secret
git init
git add .
git commit -m "Initial commit: Add code generation scripts"
git remote add origin https://github.com/leihanwa/BODE-GEN.git
git push -u origin master
```

修改代码后：
```bash
git add BODE-GEN.py
git commit -m "Fix: Update model loading in BODE-GEN.py"
git push
```

## 进阶用法

### 查看版本历史：

```bash
git log
```
显示每次提交的记录。

### 回退到某个版本：

找到版本的 commit ID（`git log` 中显示，如 `a1b2c3d`）：
```bash
git checkout a1b2c3d
```

### 恢复最新版本：

```bash
git checkout master
```

### 分支管理：

创建新分支实验新功能：
```bash
git branch feature-bo-optimize
git checkout feature-bo-optimize
```

提交后合并回主分支：
```bash
git checkout master
git merge feature-bo-optimize
git push
```

## 注意事项

### 忽略不需要备份的文件：

创建 `.gitignore` 文件，写入不想上传的内容：
```plaintext
*.pyc
__pycache__/
/data1/leihanwa/anaconda3/
```
然后 `git add .gitignore` 并提交。

### 大文件问题：

如果模型文件很大（如 Llama-3-70B），用 Git LFS：
```bash
git lfs install
git lfs track "*.bin"
git add .
git commit -m "Add large model files with LFS"
git push
```

### 权限设置：

如果是私密项目，邀请导师：
- GitHub 仓库 -> Settings -> Collaborators -> 添加导师的 GitHub 用户名。

### 验证备份

推送后，访问你的 GitHub 仓库（比如 `https://github.com/leihanwa/BODE-GEN`），确认代码已上传。
点击 “Commits” 查看版本历史。

## 总结

流程：初始化 -> 添加/提交 -> 创建远程仓库 -> 推送 -> 持续更新。
好处：每个版本都安全备份在 GitHub，可随时回退或分享。
后续：有问题（比如推送失败），告诉我错误，我帮你解决！
试试这些步骤吧，把你的代码安全存起来！有什么进展或邮箱要给我，随时说，我可以用邮件继续支持！
```

请将上述内容粘贴到你的 Markdown 文件中。
