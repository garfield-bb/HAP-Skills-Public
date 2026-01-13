# HAP Skills for GitHub Copilot

> 明道云 HAP 开发技能包 - GitHub Copilot 适配版本

## 📦 包含的 Prompts

- **hap-view-plugin.md** - HAP 视图插件开发指导
- **hap-v3-api.md** - HAP V3 API 使用指导
- **hap-mcp-usage.md** - HAP MCP 使用指南
- **hap-as-database.md** - 使用 HAP 作为数据库搭建网站

## 🚀 安装方法

### 方法一：项目级安装（推荐）

将 prompt 文件复制到你的项目目录：

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 在你的项目目录中创建 prompts 文件夹
mkdir -p .github/copilot/prompts

# 复制所有 prompt 文件
cp ~/HAP-Skills-Public/.github-copilot-compatible/prompts/*.md .github/copilot/prompts/
```

### 方法二：全局安装

如果 GitHub Copilot 支持全局 prompts（具体请查看官方文档）：

```bash
# 创建全局 prompts 目录
mkdir -p ~/.github/copilot/prompts

# 复制文件
cp ~/HAP-Skills-Public/.github-copilot-compatible/prompts/*.md ~/.github/copilot/prompts/
```

## 💡 使用方法

### 在 GitHub Copilot Chat 中使用

GitHub Copilot 的 prompt 使用方式（根据官方文档）：

#### 方式 1：使用 @ 引用工作区

```
@workspace 参考 hap-view-plugin prompt，帮我开发 HAP 甘特图插件
```

#### 方式 2：直接提及文件

```
根据 .github/copilot/prompts/hap-view-plugin.md 的指导开发插件
```

#### 方式 3：使用命令（如果支持）

```
/prompt hap-view-plugin
```

## 🎯 使用场景

### 开发 HAP 视图插件
```
@workspace 使用 hap-view-plugin prompt 创建产品展示看板
```

### 使用 HAP API
```
@workspace 根据 hap-v3-api prompt 在 React 中调用 HAP API
```

### 配置 HAP MCP
```
@workspace 参考 hap-mcp-usage prompt 配置 MCP
```

### 搭建网站
```
@workspace 按 hap-as-database prompt 用 HAP 搭建官网
```

## ⚠️ 注意事项

### 与 Claude Code 版本的区别

1. **无 YAML 元数据**：GitHub Copilot 不支持 YAML frontmatter，已移除
2. **无自动触发**：需要手动引用 prompt
3. **内容相同**：prompt 内容与 Claude Code 版本完全一致
4. **格式适配**：按照 GitHub Copilot 的 prompt 规范组织

### GitHub Copilot Prompts 说明

GitHub Copilot 的 prompt 功能可能根据版本有所不同，建议：

1. 查看 [GitHub Copilot 官方文档](https://docs.github.com/en/copilot)了解最新用法
2. 确认你的 Copilot 订阅支持 custom prompts
3. 如果不支持，可以将内容作为普通 Markdown 文档引用

### 限制

- 功能取决于 GitHub Copilot 版本和订阅类型
- 可能不支持自动加载项目级 prompts
- 需要手动引用每次使用

## 📚 相关资源

- [HAP 官方文档](https://help.mingdao.com)
- [HAP API 文档](https://api.mingdao.com/docs)
- [GitHub Copilot 文档](https://docs.github.com/en/copilot)
- [主仓库](https://github.com/garfield-bb/HAP-Skills-Public)
- [多平台适配指南](https://github.com/garfield-bb/HAP-Skills-Public/blob/main/MULTI-PLATFORM-GUIDE.md)

## 🔄 未来计划

随着 GitHub Copilot 功能的完善，我们将：

- 适配最新的 prompt 格式
- 添加 Copilot 特定的元数据
- 提供更好的集成方式

## 🆘 需要帮助？

- [提交 Issue](https://github.com/garfield-bb/HAP-Skills-Public/issues)
- [参与讨论](https://github.com/garfield-bb/HAP-Skills-Public/discussions)
- 分享你的使用经验

---

**💡 提示**：如果你使用 Claude Code，推荐使用原生版本以获得更好的自动触发体验。

---

**🤝 贡献**：如果你发现更好的 GitHub Copilot 集成方式，欢迎提交 PR！
