选择适合的 **Platform（操作系统）** 主要取决于你的本地设备是什么系统：

1. **Linux**（如果你的电脑运行 Linux）  
   - 直接在 **终端（Terminal）** 运行 `ssh` 命令即可。
   - 不需要额外安装 SSH 客户端，Linux 自带 OpenSSH。

2. **Windows**（如果你的电脑运行 Windows）  
   - **推荐方法 1**：使用 **Windows Terminal 或 PowerShell**（Windows 10/11 自带 SSH）  
     直接运行：
     ```sh
     ssh 用户名@服务器IP
     ```
   - **推荐方法 2**：安装 **Git Bash**（如果你习惯 Linux 命令）  
     [下载 Git Bash](https://git-scm.com/downloads)，然后在 Git Bash 里运行 `ssh` 命令。
   - **推荐方法 3**：使用 **PuTTY**（如果你需要 GUI 界面）  
     - [下载 PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
     - 在 **Host Name** 输入 `服务器IP`
     - 选择端口（默认 22），点击 **Open** 连接。

3. **macOS**（如果你的电脑运行 macOS）  
   - macOS 自带 SSH 客户端，可以直接在 **终端（Terminal）** 运行：
     ```sh
     ssh 用户名@服务器IP
     ```

### **怎么选？**
- **你的本地电脑是什么系统，就选对应的 platform**（Linux / Windows / macOS）。
- 如果你的电脑是 **Windows**，但你习惯 Linux 命令，可以装 Git Bash。
- 如果你是新手，Windows 上 **PuTTY** 可能更友好，但终端更通用。

在 Windows 上使用 **VS Code** 连接服务器，推荐使用 **Remote - SSH 插件**，具体步骤如下：

### **步骤 1：安装 Remote - SSH 插件**
1. 打开 **VS Code**。
2. 在 **扩展（Extensions，Ctrl+Shift+X）** 搜索 **Remote - SSH**。
3. 点击 **安装**。

### **步骤 2：配置 SSH 连接**
1. **打开命令面板（Ctrl+Shift+P）**，输入 `Remote-SSH: Connect to Host...` 并选择它。
2. **输入服务器地址**，格式如下：
   ```
   用户名@服务器IP
   ```
   例如：
   ```
   root@192.168.1.100
   ```
3. 如果 SSH 端口不是默认的 22，可以输入：
   ```
   ssh 用户名@服务器IP -p 端口号
   ```
4. 选择 `Windows (cmd.exe)` 作为终端类型（默认即可）。
5. 如果是 **首次连接**，会提示是否信任该主机，输入 **yes**。
6. **输入服务器密码**，如果使用 SSH 密钥，则无需输入密码。

### **步骤 3：使用 SSH 配置文件（推荐）**
如果经常连接同一台服务器，可以配置 `~/.ssh/config`（Windows 对应 `C:\Users\你的用户名\.ssh\config`）：
```ini
Host myserver
    HostName 192.168.1.100
    User root
    Port 22
    IdentityFile C:\Users\你的用户名\.ssh\id_rsa
```
之后，可以在 **VS Code 直接输入 `myserver` 连接**，无需输入完整 IP 和用户名。

### **步骤 4：打开远程文件夹**
成功连接服务器后，VS Code 会进入远程模式：
- 点击 **"Open Folder"** 选择服务器上的项目目录。
- 现在你可以像在本地一样使用 VS Code 远程编辑代码！🚀

是的，**VS Code 连接远程服务器时，必须选择 Linux**，因为服务器一般运行的是 Linux，而 Windows 只是你本地的操作系统。VS Code 通过 SSH 连接到远程 Linux 服务器并运行 VS Code Server，这样你就可以在本地 VS Code 编辑远程文件。  

### **为什么必须选 Linux？**
- 你连接的是 **Linux 服务器**，VS Code 需要在服务器端安装 **VS Code Server**。
- 选 Windows 的话，VS Code 会尝试在远程服务器上运行 Windows 版 VS Code Server，而大多数服务器是 Linux，自然无法兼容。

### **正确的做法**
1. **在 VS Code 连接时，选择 Linux 作为远程服务器类型**（即使你的本地是 Windows）。
2. **本地是 Windows，服务器是 Linux，这很常见**，所以选 Linux 服务器是正确的。

连接到服务器后，你通常需要做以下几件事，具体取决于你的目标：  

---

## **1. 确认服务器环境**
### **检查 Python 版本（如果你要跑 AI 相关代码）**
```sh
python3 --version
```
如果 Python 版本太低，你可能需要更新或安装：
```sh
sudo apt update && sudo apt install python3 python3-pip -y  # Ubuntu
sudo yum install python3 -y  # CentOS
```

### **检查已有的库**
```sh
pip list
```
如果发现缺少必要的库，可以重新安装。

---

## **2. 配置开发环境**
### **（1）创建虚拟环境（推荐）**
在服务器上安装库时，建议使用 **虚拟环境**，避免污染系统环境：
```sh
python3 -m venv venv  # 创建虚拟环境
source venv/bin/activate  # 激活虚拟环境
pip install --upgrade pip  # 更新 pip
```
在虚拟环境里安装的库不会影响系统全局环境。

### **（2）安装所需库**
如果你之前在本地开发过，可以把本地的 `requirements.txt` 传到服务器，然后运行：
```sh
pip install -r requirements.txt
```
如果没有 `requirements.txt`，可以手动安装：
```sh
pip install numpy pandas torch transformers
```

---

## **3. 传输代码和数据**
### **（1）用 SCP 传输文件**
从本地上传代码到服务器：
```sh
scp -r ./my_project 用户名@服务器IP:/home/your_user/
```
从服务器下载文件到本地：
```sh
scp 用户名@服务器IP:/home/your_user/output.txt ./
```

### **（2）VS Code 直接编辑远程代码**
既然你已经连上了服务器，可以直接用 **VS Code 编辑服务器上的代码**，无需手动上传。

---

## **4. 运行代码**
进入代码目录，运行 Python 代码：
```sh
cd my_project
python3 main.py
```

如果代码需要 GPU 计算，检查 GPU 是否可用：
```sh
nvidia-smi  # 查看显卡状态
python3 -c "import torch; print(torch.cuda.is_available())"  # PyTorch 检查 GPU
```

---

## **5. 持久运行代码（如果是长时间任务）**
如果你需要让代码长时间运行，即使断开 SSH 连接也不中断：
### **方法 1：使用 `tmux`**
```sh
tmux new -s mysession
```
然后在 tmux 里运行代码，按 `Ctrl+B` 然后 `D` 退出 tmux，代码仍在后台运行。

### **方法 2：使用 `nohup`**
```sh
nohup python3 myscript.py > output.log 2>&1 &
```
这样，即使 SSH 断开，代码也不会停止。

---

## **总结**
你连接服务器后，通常要：
1. **检查环境**（Python、CUDA）
2. **配置虚拟环境**（避免污染系统）
3. **安装依赖库**
4. **上传代码 / 数据**
5. **运行代码**
6. **使用 tmux 或 nohup 让任务持续运行**

如果你连接到服务器后发现 **目录是空的**，可能有以下几种情况：  

---

## **1. 你连接的目录不是你的工作目录**
🔹 你可以用以下命令检查当前所在路径：
```sh
pwd
```
如果输出类似于：
```
/home/your_user
```
但你的代码和数据可能存放在其他地方，例如 `/home/your_user/project/` 或 `/data/your_user/`。

🔹 **尝试查看所有文件**
```sh
ls -lah
```
如果这里仍然是空的，试试切换到 `root` 目录或者 `/data/`：
```sh
cd /data/your_user  # 试试常见存放数据的位置
ls -lah
```

---

## **2. 你登录的账户权限不足**
🔹 **检查你登录的账户**
```sh
whoami
```
如果你是普通用户，而数据可能存放在 `root` 账户下，你可能需要 `sudo` 权限或者联系管理员。

🔹 **尝试切换到 root 账户**
```sh
sudo -i
```
然后再 `ls` 看看是否能找到文件。

---

## **3. 服务器可能是新配置的**
如果服务器真的是 **新搭建的，没有任何环境和代码**，你需要：
1. **手动上传代码**（SCP、Git 或 VS Code 直接同步）。
2. **安装 Python、CUDA、PyTorch 等必要环境**（如果是 GPU 服务器）。

---

## **4. 你可能连接到了错误的服务器**
如果你确定服务器应该有代码，但你的 SSH 连接上去发现是空的：
🔹 **检查服务器 IP**
```sh
hostname -I  # 查看当前服务器的 IP
```
🔹 **在 VS Code 里检查 SSH 目标**
```sh
cat ~/.ssh/config
```
确保你连接的 `HostName` 是正确的。

---

### **✅ 解决方案**
1. **检查目录**（`pwd` 和 `ls -lah`）。
2. **尝试进入 `/home/your_user/` 或 `/data/your_user/` 目录**。
3. **确认 SSH 连接的是正确的服务器**。
4. **如果真的啥都没有，你可能需要手动上传代码或重新配置服务器**。
