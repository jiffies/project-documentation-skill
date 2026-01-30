# 配置说明组织指南

## 核心原则

### 1. 分层组织
将配置项按照重要性和功能分组：
- **必需配置项**: 系统无法运行的配置
- **推荐配置项**: 影响核心功能的配置
- **可选配置项**: 增强功能的配置

### 2. 清晰标注
为每个配置项提供：
- 配置项名称
- 用途说明
- 示例值
- 获取方式（如果需要外部服务）
- 默认值（如果有）

### 3. 多方案对比
当有多种配置方案时，提供对比表格帮助用户选择。

---

## 配置文件结构

### 推荐的 .env.example 结构

```bash
# ========================================
# 分类标题（使用分隔线）
# ========================================
配置项=示例值

# ----------------------------------------
# 子分类标题（使用短分隔线）
# ----------------------------------------
配置项=示例值
```

### 完整示例

```bash
# ========================================
# 服务器配置
# ========================================
PORT=3000
NODE_ENV=development

# ========================================
# 数据库配置
# ========================================
DATABASE_PATH=./data/db.sqlite

# ========================================
# Telegram API 配置
# ========================================
# 从 https://my.telegram.org 获取
TELEGRAM_API_ID=your_api_id
TELEGRAM_API_HASH=your_api_hash

# ========================================
# AI Provider 配置
# ========================================
# 可选值: mock (测试), openai, deepseek, gemini, custom
AI_PROVIDER=mock

# ----------------------------------------
# OpenAI 兼容 API 配置（用于 openai/deepseek/custom）
# ----------------------------------------
# 需要同时配置 API Key、Base URL 和 Model
AI_API_KEY=your_api_key
AI_API_BASE_URL=https://api.deepseek.com/v1
AI_MODEL=deepseek-chat

# ----------------------------------------
# Google Gemini 专用配置
# ----------------------------------------
# 获取 API Key: https://aistudio.google.com/app/apikey
# 如果不配置 GEMINI_API_KEY，会回退使用 AI_API_KEY
# AI_PROVIDER=gemini
# GEMINI_API_KEY=your_gemini_api_key
# AI_MODEL=gemini-2.5-flash

# ========================================
# Web Push 浏览器推送通知配置（可选）
# ========================================
# 生成 VAPID 密钥: cd apps/backend && pnpm exec web-push generate-vapid-keys --json
VAPID_PUBLIC_KEY=your_vapid_public_key
VAPID_PRIVATE_KEY=your_vapid_private_key
VAPID_SUBJECT=mailto:admin@example.com
```

---

## README 中的配置说明

### 模板 1: 必需配置项

```markdown
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

> ⚠️ **注意**: 所有 `your_*` 占位符都必须替换为实际值
```

### 模板 2: 多方案配置对比

```markdown
### 步骤 3: 获取 AI API Key

选择以下任一 AI 服务商：

| 服务商 | 性价比 | 速度 | 质量 | 推荐场景 |
|--------|--------|------|------|----------|
| Deepseek | ⭐⭐⭐⭐⭐ | 快 | 高 | 日常使用（推荐） |
| OpenAI | ⭐⭐⭐ | 中 | 最高 | 高质量要求 |
| Gemini | ⭐⭐⭐⭐ | 快 | 高 | 免费额度大 |

#### 方案 A: Deepseek（推荐，性价比高）

1. 访问 [https://platform.deepseek.com](https://platform.deepseek.com)
2. 注册并登录
3. 创建 API Key
4. 记录 API Key（格式：`sk-xxxxx`）

**配置示例**:
```bash
AI_PROVIDER=deepseek
AI_API_KEY=sk-xxxxxxxxxxxxx
AI_API_BASE_URL=https://api.deepseek.com/v1
AI_MODEL=deepseek-chat
```

#### 方案 B: OpenAI

1. 访问 [https://platform.openai.com](https://platform.openai.com)
2. 创建 API Key
3. 记录 API Key

**配置示例**:
```bash
AI_PROVIDER=openai
AI_API_KEY=sk-xxxxxxxxxxxxx
AI_API_BASE_URL=https://api.openai.com/v1
AI_MODEL=gpt-4o-mini
```

#### 方案 C: Google Gemini

1. 访问 [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)
2. 创建 API Key
3. 记录 API Key

**配置示例**:
```bash
AI_PROVIDER=gemini
GEMINI_API_KEY=AIzaSyxxxxxxxxxxxxx
AI_MODEL=gemini-2.5-flash
```
```

### 模板 3: 可选配置项

```markdown
#### 可选配置项（Web Push 浏览器推送通知）

如果需要浏览器推送通知功能，配置以下项：

```bash
# 1. 生成 VAPID 密钥对
cd apps/backend
pnpm exec web-push generate-vapid-keys --json

# 2. 将输出的密钥添加到 .env
VAPID_PUBLIC_KEY=BNxxxxxxxxxxxxxx
VAPID_PRIVATE_KEY=xxxxxxxxxxxxxx
VAPID_SUBJECT=mailto:your-email@example.com
```

**功能说明**:
- 任务完成后自动推送通知
- 即使浏览器在后台也能收到
- 无需额外的推送服务

> 💡 **提示**: 如果不配置，系统仍可正常运行，只是没有推送通知功能
```

---

## 配置项说明表格

### 模板: 配置项详细说明

```markdown
## 配置项说明

| 配置项 | 必需 | 默认值 | 说明 | 获取方式 |
|--------|------|--------|------|----------|
| `PORT` | 否 | `3000` | 后端服务端口 | - |
| `NODE_ENV` | 否 | `development` | 运行环境 | - |
| `DATABASE_PATH` | 否 | `./data/db.sqlite` | 数据库文件路径 | - |
| `TELEGRAM_API_ID` | 是 | - | Telegram API ID | [my.telegram.org](https://my.telegram.org) |
| `TELEGRAM_API_HASH` | 是 | - | Telegram API Hash | [my.telegram.org](https://my.telegram.org) |
| `AI_PROVIDER` | 是 | `mock` | AI 服务商 | - |
| `AI_API_KEY` | 是* | - | AI API 密钥 | 对应服务商官网 |
| `AI_API_BASE_URL` | 是* | - | AI API 端点 | 对应服务商文档 |
| `AI_MODEL` | 是 | `deepseek-chat` | AI 模型名称 | 对应服务商文档 |
| `GEMINI_API_KEY` | 否 | - | Gemini 专用密钥 | [aistudio.google.com](https://aistudio.google.com/app/apikey) |
| `VAPID_PUBLIC_KEY` | 否 | - | Web Push 公钥 | 使用 `web-push` 生成 |
| `VAPID_PRIVATE_KEY` | 否 | - | Web Push 私钥 | 使用 `web-push` 生成 |
| `VAPID_SUBJECT` | 否 | `mailto:admin@example.com` | Web Push 联系邮箱 | - |

> *注: 当 `AI_PROVIDER` 不为 `mock` 时必需
```

---

## 配置验证清单

### 用户视角检查
- [ ] 清楚哪些配置是必需的
- [ ] 知道如何获取每个配置项的值
- [ ] 理解每个配置项的用途
- [ ] 能够找到配置示例
- [ ] 知道配置错误时如何排查

### 技术视角检查
- [ ] 所有必需配置项都有说明
- [ ] 提供了多种配置方案（如果适用）
- [ ] 示例值格式正确
- [ ] 外部服务链接可访问
- [ ] 配置文件结构清晰

### 文档质量检查
- [ ] 使用了清晰的分隔线
- [ ] 配置项按功能分组
- [ ] 注释简洁明了
- [ ] 提供了获取方式链接
- [ ] 包含了故障排查提示

---

## 常见错误

### ❌ 错误示例 1: 缺少分组

```bash
PORT=3000
DATABASE_PATH=./data/db.sqlite
TELEGRAM_API_ID=your_api_id
AI_API_KEY=your_api_key
```

**问题**: 所有配置项混在一起，难以理解和维护。

### ✅ 正确示例 1

```bash
# ========================================
# 服务器配置
# ========================================
PORT=3000

# ========================================
# 数据库配置
# ========================================
DATABASE_PATH=./data/db.sqlite

# ========================================
# Telegram API 配置
# ========================================
TELEGRAM_API_ID=your_api_id

# ========================================
# AI Provider 配置
# ========================================
AI_API_KEY=your_api_key
```

---

### ❌ 错误示例 2: 缺少说明

```bash
TELEGRAM_API_ID=your_api_id
TELEGRAM_API_HASH=your_api_hash
```

**问题**: 用户不知道如何获取这些值。

### ✅ 正确示例 2

```bash
# ========================================
# Telegram API 配置
# ========================================
# 从 https://my.telegram.org 获取
# 1. 登录 Telegram 账号
# 2. 点击 "API development tools"
# 3. 创建应用获取 api_id 和 api_hash
TELEGRAM_API_ID=your_api_id
TELEGRAM_API_HASH=your_api_hash
```

---

### ❌ 错误示例 3: 多方案混乱

```bash
AI_PROVIDER=deepseek
AI_API_KEY=your_api_key
AI_API_BASE_URL=https://api.deepseek.com/v1
GEMINI_API_KEY=your_gemini_key
```

**问题**: 不清楚什么时候用哪个配置。

### ✅ 正确示例 3

```bash
# ========================================
# AI Provider 配置
# ========================================
AI_PROVIDER=deepseek  # 可选: mock | openai | deepseek | gemini

# ----------------------------------------
# OpenAI 兼容 API 配置（用于 openai/deepseek/custom）
# ----------------------------------------
AI_API_KEY=your_api_key
AI_API_BASE_URL=https://api.deepseek.com/v1
AI_MODEL=deepseek-chat

# ----------------------------------------
# Google Gemini 专用配置
# ----------------------------------------
# 如果使用 Gemini，取消下面的注释并配置
# AI_PROVIDER=gemini
# GEMINI_API_KEY=your_gemini_api_key
# AI_MODEL=gemini-2.5-flash
```

---

## 配置文件最佳实践

### 1. 使用分隔线
- 主分类使用 `# ========================================`
- 子分类使用 `# ----------------------------------------`

### 2. 注释规范
- 每个分组都有标题注释
- 复杂配置项提供获取方式
- 可选配置项明确标注"可选"

### 3. 示例值规范
- 使用 `your_*` 作为占位符
- 提供真实格式的示例（如 `sk-xxxxx`）
- 敏感信息使用占位符，不要使用真实值

### 4. 多方案处理
- 使用注释说明不同方案
- 非默认方案使用 `#` 注释掉
- 提供切换方案的说明

### 5. 依赖关系
- 说明配置项之间的依赖关系
- 标注条件必需的配置项
- 提供配置组合示例
