# HAP Skills Collection

> 明道云 HAP 平台开发技能包，适用于 Claude Code

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

## 🚀 安装方法

### 方法一：通过 ZIP 安装（推荐）

1. 从 [Releases](../../releases) 下载对应的 skill ZIP 文件
2. 解压到 `~/.claude/skills/` 目录

```bash
cd ~/.claude/skills/
unzip ~/Downloads/hap-view-plugin.zip
unzip ~/Downloads/hap-v3-api.zip
```

### 方法二：通过 Git Clone

```bash
cd ~/.claude/skills/
git clone https://github.com/YOUR-USERNAME/HAP-Skills-Public.git temp
cp -r temp/hap-view-plugin ./
cp -r temp/hap-v3-api ./
rm -rf temp
```

### 方法三：符号链接（开发者）

```bash
git clone https://github.com/YOUR-USERNAME/HAP-Skills-Public.git ~/HAP-Skills-Public
ln -s ~/HAP-Skills-Public/hap-view-plugin ~/.claude/skills/
ln -s ~/HAP-Skills-Public/hap-v3-api ~/.claude/skills/
```

---

## 📖 使用方法

安装后，在 Claude Code 中：

1. **自动触发**：当你提到相关需求时，skill 会自动激活
2. **手动调用**：使用命令 `/hap-view-plugin` 或 `/hap-v3-api`

### 示例对话

```
用户：我想开发一个 HAP 的甘特图插件
Claude：我看到你需要开发 HAP 视图插件，让我使用 hap-view-plugin skill...
```

```
用户：如何通过 API 查询 HAP 的产品数据？
Claude：让我使用 hap-v3-api skill 指导你...
```

---

## 🛠️ 系统要求

- **Claude Code**: 最新版本
- **Node.js**: 18+ (hap-view-plugin 需要)
- **Python**: 3.8+ (脚本工具需要)

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
