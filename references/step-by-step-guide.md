# Step by Step 使用步骤编写指南

## 核心原则

### 1. 用户视角
从完全不了解项目的新用户角度出发，假设用户：
- 没有任何背景知识
- 需要明确的操作指令
- 希望知道每一步的目的
- 需要验证每一步是否成功

### 2. 渐进式引导
按照实际操作顺序组织步骤：
1. 前置要求检查
2. 获取外部依赖
3. 配置环境
4. 初始化系统
5. 启动服务
6. 验证运行
7. 使用功能

### 3. 完整性
每个步骤都应包含：
- 清晰的标题（动词开头）
- 操作目的说明
- 具体的命令或操作
- 预期的输出或结果
- 常见问题提示

---

## 步骤模板

### 前置要求

```markdown
### 前置要求

- ✅ 软件依赖 1（版本要求）
- ✅ 软件依赖 2
- ✅ 账号要求（如果需要）
- ✅ 其他要求

> 💡 **提示**: 可选的额外说明
> ⚠️ **警告**: 重要的注意事项
```

### 标准步骤格式

```markdown
### 步骤 N: 动词开头的标题

简短说明这一步的目的（1-2 句话）。

#### 子步骤 1: 具体操作

1. 访问 [链接文本](URL)
2. 执行某个操作
3. 获取某个信息

\`\`\`bash
# 如果有命令，提供完整的可复制命令
command --option value
\`\`\`

**预期输出**:
\`\`\`
期望看到的输出内容
\`\`\`

> 💡 **提示**: 这一步的额外说明或技巧
> ⚠️ **注意**: 常见错误或注意事项
```

---

## 实际示例

### 示例 1: 获取外部服务凭证

```markdown
### 步骤 2: 获取 Telegram API 凭证

Telegram API 凭证用于连接 Telegram 服务器，拉取群组消息。

1. 访问 [https://my.telegram.org](https://my.telegram.org)
2. 使用你的 Telegram 账号登录（输入手机号和验证码）
3. 点击 "API development tools"
4. 填写应用信息：
   - App title: 随意填写（如 "My Bot"）
   - Short name: 随意填写（如 "mybot"）
   - Platform: 选择 "Other"
5. 点击 "Create application"
6. 记录以下信息：
   - `api_id`: 一串数字（如 12345678）
   - `api_hash`: 一串字母数字组合（如 abcdef1234567890）

> ⚠️ **重要提示**: 建议使用测试小号，避免主号被封风险
> 💡 **提示**: 这些凭证会在步骤 4 中用到
```

### 示例 2: 配置环境变量

```markdown
### 步骤 4: 配置环境变量

环境变量用于存储敏感信息和配置参数，避免硬编码到代码中。

```bash
# 复制环境变量模板
cp apps/backend/.env.example apps/backend/.env

# 编辑配置文件
nano apps/backend/.env  # 或使用你喜欢的编辑器
```

#### 必需配置项

以下配置项必须填写，否则系统无法启动：

```bash
# ========================================
# Telegram API 配置（步骤 2 获取）
# ========================================
TELEGRAM_API_ID=12345678              # 替换为你的 api_id
TELEGRAM_API_HASH=abcdef1234567890    # 替换为你的 api_hash

# ========================================
# AI Provider 配置（步骤 3 获取）
# ========================================
AI_PROVIDER=deepseek                  # 可选: mock | openai | deepseek | gemini
AI_API_KEY=sk-xxxxxxxxxxxxx           # 替换为你的 API Key
AI_API_BASE_URL=https://api.deepseek.com/v1
AI_MODEL=deepseek-chat
```

#### 可选配置项

以下配置项可以跳过，使用默认值：

```bash
# ========================================
# 服务器配置（可选）
# ========================================
PORT=3000                             # 默认 3000
NODE_ENV=development                  # 默认 development
```

> 💡 **提示**: 配置文件中的注释以 `#` 开头
> ⚠️ **注意**: 不要将 `.env` 文件提交到 Git 仓库
```

### 示例 3: 启动服务

```markdown
### 步骤 6: 启动服务

#### 方式 A: 同时启动前后端（推荐）

适合日常开发使用，一条命令启动所有服务。

```bash
# 在项目根目录执行
pnpm dev
```

**预期输出**:
```
> @omniknight/backend dev
> Backend server running on http://localhost:3000

> @omniknight/web dev
> Frontend server running on http://localhost:5173
```

服务地址：
- 后端 API: [http://localhost:3000](http://localhost:3000)
- 前端 Dashboard: [http://localhost:5173](http://localhost:5173)

#### 方式 B: 分别启动（用于调试）

适合需要单独调试前端或后端的场景。

**终端 1 - 启动后端**:
```bash
pnpm --filter @omniknight/backend dev
# 后端运行在 http://localhost:3000
```

**终端 2 - 启动前端**:
```bash
pnpm --filter @omniknight/web dev
# 前端运行在 http://localhost:5173
```

> 💡 **提示**: 使用 `Ctrl+C` 停止服务
> ⚠️ **注意**: 确保端口 3000 和 5173 没有被占用
```

### 示例 4: 验证系统运行

```markdown
### 步骤 8: 验证系统运行

通过以下测试确认系统正常运行。

#### 测试 API 连接

```bash
# 测试 1: 查看群组列表
curl http://localhost:3000/api/groups

# 预期输出: JSON 格式的群组列表
# {"success":true,"data":[{"id":1,"name":"测试群组",...}]}

# 测试 2: 手动生成总结
curl -X POST http://localhost:3000/api/summaries/generate \
  -H "Content-Type: application/json" \
  -d '{
    "groupId": 1,
    "periodStart": "2025-01-29T00:00:00Z",
    "periodEnd": "2025-01-30T23:59:59Z"
  }'

# 预期输出: 返回任务ID
# {"success":true,"data":{"jobId":123}}
```

#### 查看日志

后端日志会实时输出到终端，关键日志包括：

- ✅ `Telegram 客户端连接成功` - Telegram 连接正常
- 📡 `开始拉取消息` - 开始拉取群组消息
- 🤖 `调用 AI 生成总结` - AI 服务调用成功
- ✅ `总结生成完成` - 任务执行完成

> 💡 **提示**: 如果看到错误日志，检查环境变量配置
> ⚠️ **常见问题**: 如果 API 无响应，检查后端是否正常启动
```

---

## 编写检查清单

完成步骤编写后，使用以下检查清单验证质量：

### 完整性检查
- [ ] 每个步骤都有清晰的标题
- [ ] 每个步骤都说明了目的
- [ ] 提供了完整的命令或操作指令
- [ ] 说明了预期的输出或结果
- [ ] 包含了常见问题提示

### 可操作性检查
- [ ] 命令可以直接复制粘贴执行
- [ ] 所有占位符都有明确说明（如 `your_api_key`）
- [ ] 外部链接都是可访问的
- [ ] 步骤顺序符合实际操作流程

### 用户友好性检查
- [ ] 使用了清晰的图标（✅ ⚠️ 💡）
- [ ] 提供了多种方案选择（如果适用）
- [ ] 包含了故障排查提示
- [ ] 语言简洁易懂，避免术语堆砌

### 格式规范检查
- [ ] 使用了正确的 Markdown 语法
- [ ] 代码块指定了语言类型
- [ ] 链接格式正确
- [ ] 层级结构清晰（使用 ###、####）

---

## 常见错误

### ❌ 错误示例 1: 缺少上下文

```markdown
### 配置环境变量

编辑 .env 文件。
```

**问题**: 没有说明为什么要配置、如何编辑、配置什么内容。

### ✅ 正确示例 1

```markdown
### 步骤 4: 配置环境变量

环境变量用于存储敏感信息和配置参数。

```bash
cp apps/backend/.env.example apps/backend/.env
nano apps/backend/.env
```

编辑以下必需配置项：
- `TELEGRAM_API_ID`: 步骤 2 获取的 api_id
- `AI_API_KEY`: 步骤 3 获取的 API Key
```

---

### ❌ 错误示例 2: 命令不完整

```markdown
运行 npm install 安装依赖。
```

**问题**: 没有提供完整的代码块，用户无法直接复制。

### ✅ 正确示例 2

```markdown
### 步骤 1: 安装依赖

```bash
# 使用 pnpm 安装项目依赖
pnpm install
```

**预期输出**: 依赖安装进度条，最后显示 "Done in Xs"
```

---

### ❌ 错误示例 3: 缺少验证步骤

```markdown
启动服务后，访问 http://localhost:3000
```

**问题**: 没有说明如何验证服务是否正常运行。

### ✅ 正确示例 3

```markdown
### 步骤 6: 启动服务

```bash
pnpm dev
```

**验证服务运行**:
1. 访问 [http://localhost:3000/api/health](http://localhost:3000/api/health)
2. 应该看到 `{"status":"ok"}`
3. 如果看到错误，检查端口是否被占用

> 💡 **提示**: 使用 `lsof -i :3000` 检查端口占用
```
