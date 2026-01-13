# HAP Skills Collection

> 明道云 HAP 平台开发技能包，支持多个 AI 编程助手

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/github/v/release/garfield-bb/HAP-Skills-Public)](https://github.com/garfield-bb/HAP-Skills-Public/releases)

## 🤖 支持的 AI 产品

| AI 编程助手 | 安装路径 | 状态 | 获取方式 |
|------------|---------|------|---------|
| **Claude Code** | `~/.claude/skills/` | ✅ 完全支持 | [下载 ZIP](../../releases) |
| **Cursor** | `.cursor/rules/` | ✅ 可用 | [查看说明](./.cursor-compatible/) |
| **Windsurf** | `.windsurf/rules/` | ✅ 可用 | [查看说明](./.windsurf-compatible/) |
| **GitHub Copilot** | `.github/prompts/` | ✅ 可用 | [查看说明](./.github-copilot-compatible/) |
| **其他产品** | - | ✅ 通用格式 | [查看说明](./.universal-compatible/) |

> 💡 **当前版本**：已支持 **Claude Code**（完全支持）、**Cursor**、**Windsurf**、**GitHub Copilot** 及其他 AI 产品。每个平台都有对应的适配版本和使用说明。

## 📦 可用 Skills

### 1. hap-view-plugin
创建和开发明道云 HAP 自定义视图插件的专业技能。

**功能特性：**
- 初始化视图插件项目
- 配置开发环境和调试
- HAP SDK 集成指导
- 本地测试和打包发布

[查看详情](./hap-view-plugin/) | [下载 ZIP](../../releases)

---

### 2. hap-v3-api
使用明道云 HAP V3 接口搭建页面和操作数据的专业技能。

**功能特性：**
- HAP API V3 调用指导
- 接口鉴权配置
- 筛选器语法支持
- 完整的开发工作流

[查看详情](./hap-v3-api/) | [下载 ZIP](../../releases)

---

### 3. hap-mcp-usage
明道云 HAP MCP 使用指南技能。

**功能特性：**
- 理解两种 HAP MCP 的区别
- API 文档 MCP 使用指导
- 应用执行 MCP 使用指导
- MCP 配置和安全提示

[查看详情](./hap-mcp-usage/) | [下载 ZIP](../../releases)

---

### 4. hap-as-database
使用明道云 HAP 作为数据库搭建独立网站的技能。

**功能特性：**
- HAP + 前端项目架构指导
- API 集成和数据渲染
- 企业官网/CMS 系统搭建
- 部署到生产环境

[查看详情](./hap-as-database/) | [下载 ZIP](../../releases)

---

## 🚀 安装方法

### 📍 根据你使用的 AI 产品选择安装方式

<details>
<summary><b>🔵 Claude Code（完全支持）</b></summary>

#### 方法一：通过 ZIP 安装（推荐）

1. 从 [Releases](../../releases) 下载对应的 skill ZIP 文件
2. 解压到 `~/.claude/skills/` 目录

```bash
cd ~/.claude/skills/
unzip ~/Downloads/hap-view-plugin.zip
unzip ~/Downloads/hap-v3-api.zip
unzip ~/Downloads/hap-mcp-usage.zip
unzip ~/Downloads/hap-as-database.zip
```

#### 方法二：通过 Git Clone

```bash
cd ~/.claude/skills/
git clone https://github.com/garfield-bb/HAP-Skills-Public.git temp
cp -r temp/hap-view-plugin ./
cp -r temp/hap-v3-api ./
cp -r temp/hap-mcp-usage ./
cp -r temp/hap-as-database ./
rm -rf temp
```

#### 方法三：符号链接（开发者）

```bash
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public
ln -s ~/HAP-Skills-Public/hap-view-plugin ~/.claude/skills/
ln -s ~/HAP-Skills-Public/hap-v3-api ~/.claude/skills/
ln -s ~/HAP-Skills-Public/hap-mcp-usage ~/.claude/skills/
ln -s ~/HAP-Skills-Public/hap-as-database ~/.claude/skills/
```

#### 使用方法

**自动触发**（推荐）：当你提到相关需求时，skill 会自动激活

```
你：我想开发一个 HAP 的甘特图插件
Claude：我看到你需要开发 HAP 视图插件，让我使用 hap-view-plugin skill...
```

**手动调用**：
```bash
/hap-view-plugin
/hap-v3-api
/hap-mcp-usage
/hap-as-database
```

</details>

<details>
<summary><b>🟣 Cursor（可用）</b></summary>

> ✅ Cursor 适配版本已就绪！直接使用即可。

#### 快速安装

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 复制到项目
mkdir -p .cursor/rules
cp ~/HAP-Skills-Public/.cursor-compatible/rules/*.md .cursor/rules/
```

#### 使用方法

在 Cursor 中使用 @ 引用规则文件：

```
@hap-view-plugin.md 帮我开发一个 HAP 甘特图插件
```

详细说明：[.cursor-compatible/README.md](./.cursor-compatible/README.md)

</details>

<details>
<summary><b>🔷 Windsurf（可用）</b></summary>

> ✅ Windsurf 适配版本已就绪！直接使用即可。

#### 快速安装

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 复制到项目
mkdir -p .windsurf/rules
cp ~/HAP-Skills-Public/.windsurf-compatible/rules/*.md .windsurf/rules/
```

#### 使用方法

在 Windsurf 中提及规则名称：

```
使用 hap-view-plugin 规则，帮我开发一个 HAP 甘特图插件
```

详细说明：[.windsurf-compatible/README.md](./.windsurf-compatible/README.md)

</details>

<details>
<summary><b>💚 GitHub Copilot（可用）</b></summary>

> ✅ GitHub Copilot 适配版本已就绪！直接使用即可。

#### 快速安装

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 复制到项目
mkdir -p .github/copilot/prompts
cp ~/HAP-Skills-Public/.github-copilot-compatible/prompts/*.md .github/copilot/prompts/
```

#### 使用方法

在 GitHub Copilot Chat 中引用 prompt：

```
@workspace 参考 hap-view-plugin prompt，帮我开发 HAP 插件
```

详细说明：[.github-copilot-compatible/README.md](./.github-copilot-compatible/README.md)

</details>

<details>
<summary><b>🌟 其他 AI 产品（通用格式）</b></summary>

> ✅ 通用格式版本已就绪！适用于所有 AI 编程助手。

支持产品：**Cline**、**Aider**、**Continue**、**ChatGPT**、**Claude.ai** 等

#### 快速使用

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 查看通用格式文件
ls ~/HAP-Skills-Public/.universal-compatible/
```

#### 使用方法

**方式 1**：直接复制粘贴内容到 AI 对话

**方式 2**：作为项目文档让 AI 读取

**方式 3**：根据你的 AI 产品特定功能使用

详细说明：[.universal-compatible/README.md](./.universal-compatible/README.md)

</details>

---

## 🛠️ 系统要求

### 通用要求
- **AI 编程助手**：Claude Code / Cursor / Windsurf / 其他
- **操作系统**：macOS / Linux / Windows

### 特定 Skills 要求
- **hap-view-plugin**: Node.js 18+ （插件开发和打包）
- **hap-v3-api**: 无额外要求
- **hap-mcp-usage**: 无额外要求
- **hap-as-database**: 无额外要求

---

## 📚 相关文档

- [HAP 官方文档](https://help.mingdao.com)
- [HAP API 文档](https://api.mingdao.com/docs)
- [Claude Code 官方文档](https://github.com/anthropics/claude-code)

---

## 🤝 贡献指南

欢迎贡献！如果你有改进建议：

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开一个 Pull Request

---

## 📝 更新日志

查看完整的 [CHANGELOG.md](./CHANGELOG.md)

### v1.1.0 (2026-01-13)
- ✨ 新增 hap-mcp-usage skill - HAP MCP 使用指南
- ✨ 新增 hap-as-database skill - 使用 HAP 作为数据库搭建网站
- 📚 添加多平台支持说明
- 📝 更新安装指南

### v1.0.0 (2024-01-13)
- 🎉 首次发布
- ✨ 添加 hap-view-plugin skill
- ✨ 添加 hap-v3-api skill

---

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

## 💬 支持

如有问题或建议：
- 提交 [Issue](../../issues)
- 参与 [Discussions](../../discussions)

---

**⭐ 如果这个项目对你有帮助，请给个 Star！**
