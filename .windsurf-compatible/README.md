# HAP Skills for Windsurf

> 明道云 HAP 开发技能包 - Windsurf 适配版本

## 📦 包含的规则

- **hap-view-plugin.md** - HAP 视图插件开发指导
- **hap-v3-api.md** - HAP V3 API 使用指导
- **hap-mcp-usage.md** - HAP MCP 使用指南
- **hap-as-database.md** - 使用 HAP 作为数据库搭建网站

## 🚀 安装方法

### 方法一：项目级安装（推荐）

将规则文件复制到你的项目目录：

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 在你的项目目录中创建规则文件夹
mkdir -p .windsurf/rules

# 复制所有规则文件
cp ~/HAP-Skills-Public/.windsurf-compatible/rules/*.md .windsurf/rules/
```

### 方法二：使用符号链接

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 在项目中创建符号链接
mkdir -p .windsurf/rules
ln -s ~/HAP-Skills-Public/.windsurf-compatible/rules/*.md .windsurf/rules/
```

## 💡 使用方法

### 在 Windsurf 中使用规则

由于 Windsurf 不支持 YAML 自动触发，你需要在对话中提及规则：

#### 直接提及规则名称

```
使用 hap-view-plugin 规则，帮我开发一个 HAP 甘特图插件
```

```
根据 hap-v3-api 规则，教我如何查询产品数据
```

```
参考 hap-mcp-usage 规则，我该如何配置 HAP MCP？
```

```
按照 hap-as-database 规则，用 HAP 搭建企业官网
```

#### 添加到项目配置

如果 Windsurf 支持项目配置文件（如 `.windsurf/config.json`），可以引用规则目录：

```json
{
  "rules": {
    "directories": [".windsurf/rules"]
  }
}
```

## 🎯 使用场景

### 开发 HAP 视图插件
```
使用 hap-view-plugin 规则创建产品展示看板
```

### 使用 HAP API
```
根据 hap-v3-api 规则在 React 项目中调用 HAP API
```

### 配置 HAP MCP
```
参考 hap-mcp-usage 规则配置应用执行 MCP
```

### 搭建网站
```
按照 hap-as-database 规则用 HAP 做后端搭建官网
```

## ⚠️ 注意事项

### 与 Claude Code 版本的区别

1. **无 YAML 元数据**：Windsurf 不支持 YAML frontmatter，已移除
2. **无自动触发**：需要手动在对话中提及规则名称
3. **内容相同**：规则内容与 Claude Code 版本完全一致

### 限制

- 不支持命令调用（如 `/hap-view-plugin`）
- 需要每次在对话中提及规则
- 规则需要放在项目目录中

## 📚 相关资源

- [HAP 官方文档](https://help.mingdao.com)
- [HAP API 文档](https://api.mingdao.com/docs)
- [Windsurf 官方文档](https://codeium.com/windsurf)
- [主仓库](https://github.com/garfield-bb/HAP-Skills-Public)
- [多平台适配指南](https://github.com/garfield-bb/HAP-Skills-Public/blob/main/MULTI-PLATFORM-GUIDE.md)

## 🆘 需要帮助？

- [提交 Issue](https://github.com/garfield-bb/HAP-Skills-Public/issues)
- [参与讨论](https://github.com/garfield-bb/HAP-Skills-Public/discussions)

---

**💡 提示**：如果你使用 Claude Code，推荐使用原生版本以获得更好的自动触发体验。
