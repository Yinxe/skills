# Skills 技能仓库

面向 AI Agent 的技能集合，为 OpenCode Openclaw  等Agent提供扩展能力。

## 已有的技能

### Blogging / 博客

| 技能 | 说明 |
|------|------|
| hexo | Hexo 博客框架 — 安装、配置、写作、部署、主题开发、插件开发 |

### Desktop / 桌面环境

| 技能 | 说明 |
|------|------|
| gnome-shell-extension-development | GNOME Shell 扩展开发全面指南 |

### Docs / 技术文档

| 技能 | 说明 |
|------|------|
| opencode-docs | OpenCode AI 编码代理中文参考指南 |
| opentui-doc | OpenTUI 终端 UI 框架文档 |

### Media / 多媒体

| 技能 | 说明 |
|------|------|
| mimo-tts | 文字转语音、情绪语音合成 |

### Tooling / 工具链

| 技能 | 说明 |
|------|------|
| web-docs-to-skill | Web 文档站点转换为可复用的 SKILL |

## 安装

```bash
npx skills add https://github.com/Yinxe/skills --skill <技能名>
```

示例：

```bash
# 安装 mimo-tts 技能
npx skills add https://github.com/Yinxe/skills --skill media/mimo-tts
```

# 选择多个技能同时安装
```bash
npx skills add Yinxe/skills
```

首次使用前请参考各技能的 `SKILL.md` 中关于环境变量的配置说明。
