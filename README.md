# OpenCode 快速入门

# 安装配置

---

## 1. 安装

### 方式一：bun（推荐）

```cmd
bun install -g opencode-ai
```

### 方式二：npm

```cmd
npm i -g opencode-ai
```

### 方式三：其他形态

https://opencode.ai/zh/download

支持 TUI、Web、IDE 多种形态，推荐 CLI 模式。

### 补充方式：CodeAgent CLI

- [产品手册](https://wiki.huawei.com/domains/171127/wiki/8/WIKI2026032710576951)
- [下载地址](https://his.huawei.com/csop/index.html#/ToolInfo?samType=his&toolId=1955187767393722369)

### 验证安装

```
opencode --version
```

### 版本更新

```cmd
opencode upgrade 1.4.6
```

---

## 2. 基础配置

> **内网使用建议**：关闭免费模型，避免调用

### 完整配置参考

```json
{
  "$schema": "http://wsr-kwe.his.huawei.com/36b6eb820464410c9c35242389b3e972/Pro/code-agent-admin/oc/config.json",
  "share": "disabled",
  "autoupdate": false,
  "enabled_providers": [
    "local",
    "w3",
    "cm"
  ],
  "provider": {
    "local": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "local",
      "options": {
        "baseURL": "https://oneapi.rnd.huawei.com/v1",
        "apiKey": ""
      },
      "models": {
        "GLM-4.7-w8a8-MAE-M": {
          "name": "GLM-4.7-w8a8-MAE-M"
        }
      }
    },
    "cm": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "cm",
      "models": {
        "Glm-4.5-air": {
          "name": "Glm-4.5-air"
        },
        "MiniMax-M2.5": {
          "name": "MiniMax-M2.5"
        },
        "Qwen2.5-VL-72B-Instruct": {
          "name": "Qwen2.5-VL-72B-Instruct"
        }
      },
      "options": {
        "baseURL": "",
        "apiKey": "",
      }
    }
  },
  "plugin": [
    "oh-my-openagent@latest"
  ],
  "mcp": {
  }
}
```

### 内部模型市场

[模型市场](https://panshi.rnd.huawei.com/ocloudcommonwebsite/index.html#/aiResources/model/market)

---

# 基础操作

> 建议进入项目目录后再启动opencode



| 符号 | 作用     | 示例                            |
| :--- | :------- | :------------------------------ |
| `@`  | 引用文件 | `@src/main.ts 这个文件做了什么` |
| `!`  | 执行命令 | `!ls -la` 查看目录              |
| `/`  | 斜杠命令 | `/help` 查看帮助                |

### 斜杠命令

| 命令        | 说明                         |
| ----------- | ---------------------------- |
| `/sessions` | 查看历史会话                 |
| `/new`      | 开启新会话                   |
| `/export`   | 导出当前会话                 |
| `/timeline` | 查看会话时间线               |
| `/init`     | 初始化项目（创建 AGENTS.md） |
| `/compact`  | 压缩上下文，释放 Token       |

### 常用快捷键

| 快捷键      | 作用             |
| :---------- | :--------------- |
| Tab         | 切换Agent        |
| Shift+Enter | 换行（不发送）   |
| Ctrl+C      | 中断当前操作     |
| Ctrl+X Y    | 复制最后一条消息 |
| Ctrl+X N    | 新建会话         |
| Ctrl+X L    | 打开会话列表     |
| Ctrl+X M    | 切换模型         |
| Esc         | 取消/返回        |

## 4. 原子能力

> OpenCode 的主要内置工具

| 工具        | 功能                   |
| ----------- | ---------------------- |
| `read`      | 读取文件内容           |
| `write`     | 写入/覆盖文件          |
| `edit`      | 编辑文件（精确替换）   |
| `glob`      | 按模式查找文件         |
| `grep`      | 正则表达式搜索文件内容 |
| `webfetch`  | 获取网页内容           |
| `todowrite` | 创建和管理待办列表     |
| `question`  | 询问用户问题           |
| `skill`     | 加载技能               |
| `bash`      | 执行终端命令           |

### Skills（技能系统）

OpenCode 支持扩展技能，详见详细文档。

### MCP（Model Context Protocol）

支持连接外部工具和服务，详见详细文档。

### 自定义命令

在 `~/.config/opencode/commands/` 目录下创建 `.md` 文件即可定义自定义命令。

---

## 4. 进阶技巧

### 子代理

#### 超大规模任务时，AI产生畏难情绪

1. 一开始能基本按模板要求分析

![image-20260420105316058](http://image.huawei.com/tiny-lts/v1/images/hi3ms/7e2c4910a82dbcd7357e4cdd1a59ee4c_1500x1360.png)

2. 逐渐失去耐心，偷工减料

![image-20260420105423768](http://image.huawei.com/tiny-lts/v1/images/hi3ms/d4c6b8931fcd3a7a3c59ef13ea5542cf_1363x951.png)

3. 直接放弃

![image-20260420105443664](http://image.huawei.com/tiny-lts/v1/images/hi3ms/770766ca8a85f464046bcf801ba77605_1346x1267.png)

![image-20260420105516231](http://image.huawei.com/tiny-lts/v1/images/hi3ms/5ccf933c36930823efce64ac2eaa8199_506x1194.png)

#### 提示词无济于事

![image-20260420105612990](http://image.huawei.com/tiny-lts/v1/images/hi3ms/aab931fe5d1e87e37c5672bf430d5062_565x140.png)



#### 使用子代理拆分任务

yaml-analyzer只分析一个yaml：

![image-20260423105624378](http://image.huawei.com/tiny-lts/v1/images/hi3ms/6d822eec9d3e455c0a731adbbee7a6ff_1432x978.png)

api-analyzer只分析一个yaml：

![image-20260423105649077](http://image.huawei.com/tiny-lts/v1/images/hi3ms/64a684b23e799760cb0bcd284b6a0d4e_1687x813.png)

#### 子代理执行结果

![image-20260423105545323](http://image.huawei.com/tiny-lts/v1/images/hi3ms/5b30b8d8e75fefe5e0669c1d7efb2c32_723x1008.png)

![image-20260423110146565](http://image.huawei.com/tiny-lts/v1/images/hi3ms/89ac0fbcfd92d50f1a5a45bfee856696_2554x4749.png)

### 常用技巧

- 使用 `cc-switch` 查看历史会话更高效
  - 下载：https://github.com/farion1231/cc-switch



### 已知问题

#### 问题 1：思考过程中调用工具导致崩溃

- 症状：输出中出现 `<tool_call>` 标签后异常中断
- 状态：官方已知 issue，GLM 模型更容易触发
- 参考：https://github.com/anomalyco/opencode/issues/8877

#### 问题 2：PowerShell 命令不兼容

- 原因：OpenCode 默认使用 PowerShell
- 解决：配置 SHELL 环境变量指向 Git Bash（如上所示）

- 

---

## 5.生态

### oh-my-openagent (OMO)

> OpenCode 的增强工具包，提供预设 Agents、Skills、Hooks、MCPs，大幅提升效率。

**一键安装**：

```cmd
bunx oh-my-opencode install
```

codeagent cli离线安装：

https://wiki.huawei.com/domains/171127/wiki/8/WIKI2026032710577003

**核心特性**：

| 特性            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| **Agents**      | Sisyphus（主 agent）、Prometheus（规划）、Oracle（架构/调试）、Librarian 等 |
| **Skills**      | `playwright`（浏览器自动化）、`git-master`、`frontend-ui-ux` 等内置技能 |
| **MCPs**        | `websearch`（Exa 驱动）、`context7`、`grep_app` 等           |
| **ultrawork**   | 安装后直接输入 `ultrawork` 或 `ulw` 即可开始工作流           |
| **子代理调度**  | 通过 `@` 使用特定代理，如 `@explore` 搜索代码                |
| **/ralph-loop** | 让 AI 坚持完成困难任务，避免中途放弃                         |

**配置位置**：

- 全局：`~/.config/opencode/oh-my-openagent.json`
- 项目级：`.opencode/oh-my-openagent.json`

**文档**：[oh-my-openagent GitHub](https://github.com/code-yeongyu/oh-my-openagent)

### superpowers

仓库 [superpowers Github](https://github.com/obra/superpowers)

在 `opencode.json`（全局或项目级别）中的 `plugin` 数组中添加:

```
{
  "plugin": ["superpowers@git+https://github.com/obra/superpowers.git"]
}
```

重新启动 OpenCode。插件将通过 Bun 自动安装，并自动注册所有技能。
通过提问验证：“告诉我你的superpowers是什么”



```cmd
npm install superpowers@git+https://github.com/obra/superpowers.git --prefix "%USERPROFILE%\.config\opencode"
```

## 6.坑

### 1. 思考过程中调用了工具

思考过程中调用工具(出现<tool_call>标签)，opencode异常中断。

GLM模型概览大。

#### 参考issue

https://github.com/anomalyco/opencode/issues/8877

https://github.com/anomalyco/opencode/issues/9674

#### 示意图

![image-20260415093216904](http://image.huawei.com/tiny-lts/v1/images/hi3ms/af45724522d70065fe1dbf1d46d2d849_2035x577.png)

### 2. 默认使用Powershell

1.3 版本后的opencode默认使用powershell，使用powershell调用bash命令，命令不兼容。

#### 参考PR

https://github.com/anomalyco/opencode/pull/16069

#### 示意图

![image-20260415094027768](http://image.huawei.com/tiny-lts/v1/images/hi3ms/812ee062d29e91ba5ee6f9b325d39b05_1092x435.png)

#### 解决方案

配置环境变量

SHELL=D:\App\Git\usr\bin\bash.exe

### 3. LSP 没有自动下载

- 说明：OpenCode 使用的 LSP 不会自动下载
- 解决：手动下载, 并配置到path，如 [eclipse-jdtls](https://github.com/eclipse-jdtls/eclipse.jdt.ls)

## 附录

### 斜杠命令

| 命令        | 说明                         |
| ----------- | ---------------------------- |
| `/model`    | 切换模型                     |
| `/sessions` | 查看历史会话                 |
| `/new`      | 开启新会话                   |
| `/export`   | 导出当前会话                 |
| `/timeline` | 查看会话时间线               |
| `/init`     | 初始化项目（创建 AGENTS.md） |
| `/compact`  | 压缩上下文，释放 Token       |
| `/copy`     | 复制整个会话内容到粘贴板     |

#### 会话相关

| 命令        | 作用                             |
| :---------- | :------------------------------- |
| `/new`      | 新建会话                         |
| `/sessions` | 查看并切换会话                   |
| `/undo`     | 撤销上一步操作(实测仅撤销了消息) |
| `/redo`     | 重做被撤销的操作                 |
| `/compact`  | 压缩上下文                       |
| `/export`   | 导出对话记录                     |
| `/share`    | 分享会话（生成链接）             |

### 快捷键手册

| 快捷键      | 作用             |
| :---------- | :--------------- |
| Tab         | 切换Agent        |
| Shift+Enter | 换行（不发送）   |
| Ctrl+C      | 中断当前操作     |
| Ctrl+X Y    | 复制最后一条消息 |
| Ctrl+X N    | 新建会话         |
| Ctrl+X L    | 打开会话列表     |
| Ctrl+X M    | 切换模型         |
| Esc         | 中断 AI 响应     |
| Ctrl+X U    | 撤销消息         |
| Ctrl+X R    | 重做消息         |
| Ctrl+X C    | 压缩上下文       |
| Ctrl+X B    | 切换侧边栏       |
| Ctrl+X T    | 切换主题         |
| Ctrl+P      | 命令面板         |
| Ctrl+A      | 跳到行首         |
| Ctrl+E      | 跳到行尾         |
| Ctrl+K      | 删除光标到行尾   |
| Ctrl+U      | 删除光标到行首   |
| Ctrl+W      | 删除上一个单词   |
| Alt+B       | 后退一个单词     |
| Alt+F       | 前进一个单词     |

### 常用路径

**通用格式**：

- 全局：`~/.config/opencode/`
- 项目级：`.opencode/`

| 类型       | 全局路径                               | 项目路径              |
| ---------- | -------------------------------------- | --------------------- |
| 主配置     | `~/.config/opencode/opencode.json`     | `./opencode.json`     |
| Skills     | `~/.config/opencode/skills/`           | `.opencode/skills/`   |
| Agents     | `~/.config/opencode/agents/`           | `.opencode/agents/`   |
| Commands   | `~/.config/opencode/commands/`         | `.opencode/commands/` |
| Plugins    | `~/.config/opencode/plugins/`          | `.opencode/plugins/`  |
| Themes     | `~/.config/opencode/themes/`           | `.opencode/themes/`   |
| MCP        | 在 `opencode.json` 的 `mcp` 字段中配置 | 同左                  |
| 缓存       | ~/.cache/opencode                      |                       |
| 持久化数据 | ~/.local/share/opencode                |                       |

## 参考链接

- [Skill 标准](https://agentskills.io/)
- [OpenCode GitHub](https://github.com/anomalyco/opencode)
