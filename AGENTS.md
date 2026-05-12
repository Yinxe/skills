# Skills 仓库

## 仓库约束

- **严禁推送** — 未经用户明确允许，不得执行 `git push` 到远程
- **禁止自动提交** — 必须先获得用户批准
- 使用 git worktree 开发：`git worktree add ../skills-<name> main && git checkout -b feature/xxx`
  - 完成后清理：`git worktree remove ../skills-<name>`

## 项目结构

```
desktop/                        # 桌面环境
  gnome-shell-extension-development/
docs/                           # 技术文档
  hexo-docs/                    # Hexo 博客框架
  opencode-docs/                # OpenCode 中文文档
  opentui-doc/                  # OpenTUI 框架文档
media/                          # 多媒体
  mimo-tts/                     # 文字转语音
tooling/                        # 工具链
  web-docs-to-skill/            # 文档转 SKILL
```

每个技能包含 `SKILL.md`（`name` 字段用于 `npx skills` 发现），以及可选的 `references/`、`scripts/`、`templates/`。

## 技能规范

- 脚本优先 JavaScript (Node.js >= 18) 或 Python (>= 3.10)，避免 Shell
- 跨平台兼容（路径用 `path.join()` 或 `/`，环境变量读取兼容多平台）
- 禁止 hardcode 绝对路径，路径需支持参数或环境变量配置
- 脚本需有 shebang 和可执行权限（`chmod +x`）

## 提交规范

使用 [Conventional Commits](https://www.conventionalcommits.org/)：
`<type>(<scope>): <subject>`，如 `feat(lark-im): add send message capability`
