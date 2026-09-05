# AI工具使用

## claude code cli + deepseek API

**claude code cli**：在终端里面用的编程智能体，简单来说就是命令行工具，核心目标是自完成复杂代码任务。也就是**AI coding**

**deepseek API：**由于claude 模型是国外非常贵的模型，deepseek模型的性价比很高，且能力中等偏上。因此选择接入deepseek模型。

**简单来说，claude code cli是工具，deepseek API是模型。**

#### 第1步：安装cursor

#### [AI Coding Agent for Building Ambitious Software | Cursor](https://cursor.com/)

#### 第 2 步：环境准备（安装 Node.js 18+）

Claude Code CLI 依赖 Node.js 运行，必须 ≥ v18。

- **检查版本**：`node -v`

- **若版本过低（比如 v10）**，利用 Conda 安装新版：

  ```bash
  conda install -c conda-forge nodejs=20 -y
  ```

  刷新命令缓存：`hash -r`，再次 `node -v` 确认。

------

#### 第 3 步：全局安装 Claude Code CLI

通过 npm 将 Claude Code 安装到全局环境（**务必带 `-g`**，确保任何目录下都能调用）。

```bash
npm install -g @anthropic-ai/claude-code
```

- **验证**：`claude --version` 显示版本号即成功。
- **坑点提醒**：如果系统里有 Cursor 编辑器或其他工具也提供了 `claude` 命令，可能导致冲突。此时可用 `which claude` 查看实际调用的路径，或使用 `npx -y @anthropic-ai/claude-code` 强制调用安装的版本。

------

#### 第 4 步：获取 DeepSeek API Key

- 访问 [DeepSeek Platform](https://platform.deepseek.com/api_keys)
- 登录并点击 **「创建 API Key」**，复制生成的密钥（格式为 `sk-xxxxxx`）。
- 密钥不能告诉你。

------

#### 第 5 步：配置环境变量（核心步骤）

这一步让 Claude Code 不访问 Anthropic 官方，而是指向 DeepSeek 的兼容网关。

**方式 A：写入 `~/.bashrc`（永久生效，推荐）**

一次性执行以下命令（**务必把 `sk-你的真实Key` 替换掉**）：

```bash
echo 'export ANTHROPIC_BASE_URL="https://api.deepseek.com/anthropic"' >> ~/.bashrc
echo 'export ANTHROPIC_AUTH_TOKEN="sk-你的真实Key"' >> ~/.bashrc
echo 'export ANTHROPIC_MODEL="deepseek-v4-pro[1m]"' >> ~/.bashrc
echo 'export ANTHROPIC_DEFAULT_OPUS_MODEL="deepseek-v4-pro[1m]"' >> ~/.bashrc
echo 'export ANTHROPIC_DEFAULT_SONNET_MODEL="deepseek-v4-pro[1m]"' >> ~/.bashrc
echo 'export ANTHROPIC_DEFAULT_HAIKU_MODEL="deepseek-v4-flash"' >> ~/.bashrc
echo 'export CLAUDE_CODE_SUBAGENT_MODEL="deepseek-v4-flash"' >> ~/.bashrc
echo 'export CLAUDE_CODE_EFFORT_LEVEL="max"' >> ~/.bashrc
echo 'export CLAUDE_CODE_AUTO_COMPACT_WINDOW="786432"' >> ~/.bashrc
```

加载配置：`source ~/.bashrc`

**方式 B：临时测试（只对当前终端有效）**
直接在当前终端执行上述的 `export` 命令（同样注意替换 Key，且**不要加 `<>` 尖括号，必须加双引号**）。

- **关键语法错误提醒**：`export KEY=<sk-xxx>` 是错误的，Bash 会把 `<>` 当作重定向符。正确写法是 `export KEY="sk-xxx"`。

------

#### 第 6 步：启动与使用

- 进入你的项目目录：`cd /path/to/your/project`
- 启动 CLI：直接输入 `claude`（如果之前被 Cursor 拦截，按 Enter 继续即可；若想绕过拦截，用 `npx -y @anthropic-ai/claude-code`）
- 在对话中提问测试，例如：`请简要说明这个项目的目录结构`。

------

### 日常使用与维护

| 需求                   | 操作                                                         |
| :--------------------- | :----------------------------------------------------------- |
| **切换模型**           | 对话中输入 `/model` 选菜单，或启动时用 `claude --model deepseek-v4-pro` |
| **调整思考强度**       | 对话中输入 `/effort max`，或提问中带上关键词 `ultrathink`    |
| **临时插问不打断任务** | 对话中输入 `/btw 你的简短问题`                               |
| **查看当前状态**       | 对话中输入 `/status`                                         |
| **更新 Claude Code**   | 执行 `npm update -g @anthropic-ai/claude-code`               |



## 如果想使用claude或gpt等国外的顶尖的模型，可以使用中转站

**claude code是工具，claude和deepseek是模型**

#### 步骤1：

**去淘宝买中转站的密钥**：【淘宝】https://e.tb.cn/h.8pOMOdlTmHFaU9j?tk=iUbgTglUM0P HU293 「6.8」
点击链接直接打开 或者 淘宝搜索直接打开

#### 步骤2：

根据中转站的使用文档[Cur 助手使用文档](https://www.yuque.com/meiritoutiao/veanra/qlldv52eqzt1khvc)，安装中转站的使用助手

这样形成了两套使用工具：

一套是终端里面的claude code使用的是deepseek模型

一套是cursor里面的claude和gpt模型



## **建议流水线任务在终端里面使用deepseek模型，困难任务使用claude 和 gpt 模型**