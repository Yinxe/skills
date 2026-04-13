# Skills 仓库

## 仓库约束

- **严禁推送** — 未经用户明确允许，严禁执行 `git push`、`git push --force` 或任何推送到远程仓库的操作
- **禁止自动提交** — 修改代码后如需提交，必须先获得用户批准

## 编码规范

### 跨平台兼容性

- 所有 Skill 必须保证跨平台兼容性（Linux/macOS/Windows）
- 脚本优先使用 **JavaScript**（Node.js）或 **Python** 编写
- 避免使用平台特定的命令或路径写法
- 路径分隔符使用 `path.join()` 或 `/`（Unix 风格）
- 环境变量读取需兼容多平台

### 脚本规范

| 语言 | 适用场景 | 要求 |
|------|----------|------|
| JavaScript | 轻量逻辑、API 调用、JSON 处理 | Node.js >= 18 |
| Python | 数据处理、文件操作、系统集成 | Python >= 3.10 |
| Shell | 极简包装场景 | 仅当无替代方案时使用 |

- 禁止在脚本中 hardcode 绝对路径
- 所有路径需支持通过参数或环境变量配置
- 脚本需有执行权限说明（`chmod +x` 或 `#!` shebang）

## 开发流程规范

### 分支策略

```
main (稳定分支)
├── feature/* (功能分支)
├── fix/* (修复分支)
└── refactor/* (重构分支)
```

- `main` 是唯一稳定分支，永远保持可发布状态
- 禁止直接在 `main` 上开发或修复
- 分支命名规范：`{type}/{ticket-id}-{简短描述}` 或 `{type}/{简短描述}`
  - 例：`feature/add-lark-im-skill`、`fix/video-download-timeout`

### Worktree 使用规范

**核心规则：一个功能 = 一个 worktree = 一个独立目录**

1. **创建功能分支 worktree**
   ```bash
   # 在 skills 目录下执行
   git worktree add ../skills-feature-xxx main
   cd ../skills-feature-xxx
   git checkout -b feature/xxx
   ```

2. **在 worktree 中开发**
   - 切换到对应 worktree 目录进行开发
   - 每个 worktree 独立运行，互不干扰

3. **合并完成后清理**
   ```bash
   # 合并完成后，删除 worktree 目录
   git worktree remove ../skills-feature-xxx
   ```

4. **查看所有 worktree**
   ```bash
   git worktree list
   ```

### 功能开发流程

```
1. 创建 worktree
   └── git worktree add ../skills-feature-xxx main

2. 创建功能分支
   └── git checkout -b feature/xxx

3. 开发 & 提交
   └── git add . && git commit -m "feat: add xxx"

4. 推送远程
   └── git push -u origin feature/xxx

5. 合并到 main
   └── (合并请求审查后) git checkout main && git merge --no-ff feature/xxx

6. 清理
   └── git worktree remove ../skills-feature-xxx
```

### 提交信息规范

使用 [Conventional Commits](https://www.conventionalcommits.org/)：

```
<type>(<scope>): <subject>

feat(lark-im): add send message capability
fix(bilibili): resolve download timeout issue
docs(readme): update installation guide
refactor(scripts): extract common utilities
test(downloader): add unit tests for extractor
```

**Type 类型：**
- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式（不影响功能）
- `refactor`: 重构
- `test`: 测试相关
- `chore`: 构建/工具相关

### 合并策略

- 使用 `--no-ff` 合并，保持分支历史
- 合并前确保本地 `main` 是最新的
- 合并后删除已合并的远程分支

```bash
git checkout main
git pull origin main
git merge --no-ff feature/xxx
git push origin main
git branch -d feature/xxx          # 删除本地分支
git push origin --delete feature/xxx  # 删除远程分支
```

## 项目结构

```
skills/
  skill-name/
    SKILL.md          # Skill 定义文件
    reference/        # 参考文件目录
    templates/        # 模板文件目录
    scripts/          # Skill 脚本目录
      skill.js
```

## 紧急修复流程

当 `main` 出现需要立即修复的问题时：

```
1. 从 main 创建临时修复分支
   └── git worktree add ../skills-fix-urgent main
   └── git checkout -b fix/urgent-xxx

2. 修复并提交
   └── git add . && git commit -m "fix: resolve critical issue"

3. 快速审查后合并到 main
   └── git checkout main && git merge --no-ff fix/urgent-xxx

4. 清理
   └── git worktree remove ../skills-fix-urgent
```

## 常见问题处理

| 场景 | 操作 |
|------|------|
| worktree 冲突 | `git worktree remove <path> --force` 强制移除 |
| 分支落后 main | 在分支上 `git rebase main` 变基 |
| 误删 worktree 目录 | `git worktree prune` 清理 worktree 列表 |
| 切换分支繁忙 | 使用 `git stash` 暂存当前更改 |
