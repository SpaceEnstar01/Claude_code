# 个人复现记录（Claude Code Best / CCB）

> 本文档为个人操作备忘；**勿将真实 API Key 提交到公开仓库**。若需随仓库忽略，可将 `personal.md` 加入 `.gitignore` 或仅保留占位符。

---

## 1. 仓库来源

- 个人备份仓库：<https://github.com/SpaceEnstar01/Claude_code>
- 克隆命令：

```bash
git clone https://github.com/SpaceEnstar01/Claude_code.git
cd Claude_code
```

---

## 2. 环境：Bun

- 要求：Bun ≥ 1.3.11（见项目 README）。
- **当前终端**临时生效：

```bash
export BUN_INSTALL="$HOME/.bun"
export PATH="$BUN_INSTALL/bin:$PATH"
bun --version
```

- **长期生效**：将上述两行写入 `~/.zshrc`，保存后执行 `source ~/.zshrc` 或新开终端。

---

## 3. 安装依赖

```bash
cd /path/to/Claude_code   # 本地路径按实际修改

# 国内拉取 ripgrep 较慢时可选用（可选）
# export DEFAULT_RELEASE_BASE=https://ghproxy.net/https://github.com/microsoft/ripgrep-prebuilt/releases/download/v15.0.1

bun install
```

说明：`postinstall` 若提示找不到 `dist/download-ripgrep.js` 属未构建时的常见现象，脚本会回退下载 ripgrep；以 `bun install` 最终成功为准。

---

## 4. 启动开发模式

```bash
bun run dev
```

- 若启动横幅中出现 **v2.1.888**（或 README 所述 888 线索），表示 dev 注入正常。
- 退出：在进程前台用 **Ctrl+C**（勿用 Ctrl+Z 挂起）。

---

## 5. 大模型对接（DeepSeek · OpenAI 兼容）

在 REPL 中输入 **`/login`**，选择 **「2. OpenAI Compatible」**（Chat Completions 兼容，与 DeepSeek 文档一致）。

在表单中填写（**请使用 DeepSeek 控制台中的真实密钥与模型 ID，勿写入本文档**）：

| 字段 | 填写说明 |
|------|----------|
| Base URL | `https://api.deepseek.com/v1`（以 DeepSeek 官方文档为准，通常带 `/v1`） |
| API Key | 在 DeepSeek 控制台创建，形如 `sk-...`，**勿写入公开文档** |
| Haiku / Sonnet / Opus | 填 DeepSeek 提供的 **模型 ID**；若只有一个常用模型，三格可填同一 ID（如文档中的 `deepseek-chat` 等，以控制台为准） |

操作：**Tab / Shift+Tab** 切换字段；在 **最后一项** 按 **Enter** 保存。亦可按项目 README 直接编辑 `~/.claude/settings.json` 的 `env`（等价于写入 `OPENAI_*` 等变量，具体键名以保存后文件为准）。

---

## 6. 可选：不用 UI、命令行指定 OpenAI 兼容后端

与 `docs/plans/openai-compatibility.md` 一致，可在启动前设置环境变量（示例，模型名请自行替换）：

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY="<你的 DeepSeek API Key>"
export OPENAI_BASE_URL="https://api.deepseek.com/v1"
export OPENAI_MODEL="<模型 ID>"
bun run dev
```

---

## 7. 安全提醒

- 任何 **sk-** 密钥若曾出现在聊天、截图或误提交的仓库中，应在服务商控制台 **作废并重新生成**。
- 公开推送前检查：`git status` / 历史中是否包含 `personal.md` 内的真实密钥。

---

## 8. 本人本机路径备忘（可改）

- 开发目录示例：`/Users/spur/X/space/claudeV2`（与克隆后的 `Claude_code` 二选一，以实际为准）
