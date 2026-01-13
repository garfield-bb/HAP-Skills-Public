# HAP Skills for Cursor

> 明道云 HAP 开发技能包 - Cursor 适配版本

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
mkdir -p .cursor/rules

# 复制所有规则文件
cp ~/HAP-Skills-Public/.cursor-compatible/rules/*.md .cursor/rules/
```

### 方法二：使用符号链接

```bash
# 克隆仓库
git clone https://github.com/garfield-bb/HAP-Skills-Public.git ~/HAP-Skills-Public

# 在项目中创建符号链接
mkdir -p .cursor/rules
ln -s ~/HAP-Skills-Public/.cursor-compatible/rules/*.md .cursor/rules/
```

## 💡 使用方法

### 在 Cursor 中引用规则

由于 Cursor 不支持 YAML 自动触发，你需要手动引用规则文件：

#### 方式 1：使用 @ 符号引用

```
@hap-view-plugin.md 帮我开发一个 HAP 甘特图插件
```

```
@hap-v3-api.md 如何通过 API 查询产品数据？
```

```
@hap-mcp-usage.md HAP MCP 怎么配置？
```

```
@hap-as-database.md 使用 HAP 搭建企业官网
```

#### 方式 2：添加到 .cursorrules

如果希望规则全局生效，可以将内容添加到项目根目录的 `.cursorrules` 文件：

```bash
# 在项目根目录创建 .cursorrules
cat .cursor/rules/hap-view-plugin.md >> .cursorrules
echo "\n---\n" >> .cursorrules
cat .cursor/rules/hap-v3-api.md >> .cursorrules
echo "\n---\n" >> .cursorrules
cat .cursor/rules/hap-mcp-usage.md >> .cursorrules
echo "\n---\n" >> .cursorrules
cat .cursor/rules/hap-as-database.md >> .cursorrules
```

**注意**：这会使文件较大，可能影响上下文窗口。建议只添加常用的规则。

## 🎯 使用场景

### 开发 HAP 视图插件
```
@hap-view-plugin.md 我想创建一个产品展示的自定义看板
```

### 使用 HAP API
```
@hap-v3-api.md 如何在 React 项目中调用 HAP API？
```

### 配置 HAP MCP
```
@hap-mcp-usage.md 我该用哪种 HAP MCP？
```

### 搭建网站
```
@hap-as-database.md 用 HAP 作为后端搭建企业官网
```

## ⚠️ 注意事项

### 与 Claude Code 版本的区别

1. **无 YAML 元数据**：Cursor 不支持 YAML frontmatter，已移除
2. **无自动触发**：需要手动使用 @ 引用规则文件
3. **内容相同**：规则内容与 Claude Code 版本完全一致

### 限制

- 不支持命令调用（如 `/hap-view-plugin`）
- 需要手动引用每次使用
- 文件较大时可能占用较多上下文

## 📚 相关资源

- [HAP 官方文档](https://help.mingdao.com)
- [HAP API 文档](https://api.mingdao.com/docs)
- [主仓库](https://github.com/garfield-bb/HAP-Skills-Public)
- [多平台适配指南](https://github.com/garfield-bb/HAP-Skills-Public/blob/main/MULTI-PLATFORM-GUIDE.md)

## 🆘 需要帮助？

- [提交 Issue](https://github.com/garfield-bb/HAP-Skills-Public/issues)
- [参与讨论](https://github.com/garfield-bb/HAP-Skills-Public/discussions)

---

**💡 提示**：如果你使用 Claude Code，推荐使用原生版本以获得更好的自动触发体验。
