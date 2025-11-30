# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个 **Claude Code 社区指南项目**，专注于：
- 提供全面的 Claude Code 使用指南和最佳实践
- 收集和整理各种技术栈的 CLAUDE.md 配置模板
- 跟踪 Anthropic 官方发布信息和更新
- 构建 Claude Code 开发者社区资源

## 项目架构

### 核心目录结构
```
claude-code-guide/
├── Guide On CLAUDE.md/          # CLAUDE.md 指南和模板集合
│   ├── CLAUDE.md by [作者]/     # 个人贡献的指南
│   └── CLAUDE.md Collection/    # 按技术栈分类的模板
│       ├── Python/              # Python 生态系统
│       ├── react/               # React 生态系统
│       ├── vue/                 # Vue 生态系统
│       ├── django/              # Django 框架
│       ├── laravel/             # Laravel 框架
│       ├── rails/               # Ruby on Rails
│       ├── universal/           # 通用配置
│       ├── Optimisers/          # 代码优化和审查
│       └── orchestrators/       # 项目编排和管理
└── Official Claude Releases/    # 官方信息镜像
    ├── CHANGELOG.md             # 变更日志
    ├── api.md                   # API 文档
    ├── system-prompts.md        # 系统提示词
    └── [其他官方文档]
```

### 模板分类系统

**语言专家模板** - 针对特定编程语言优化的配置
**框架专家模板** - 针对特定框架和库的专业配置
**工具专家模板** - 代码审查、性能优化、文档生成等专业工具

## 常用开发任务

### 文档管理
```bash
# 更新中文 README
edit README_中文.md

# 检查英文主 README
head -50 README.md

# 查看特定模板
cat "Guide On CLAUDE.md/CLAUDE.md Collection/[分类]/[模板].md"
```

### 模板操作
```bash
# 搜索特定技术的模板
find "Guide On CLAUDE.md/CLAUDE.md Collection" -name "*react*" -type f
find "Guide On CLAUDE.md/CLAUDE.md Collection" -name "*python*" -type f

# 查看模板内容结构
grep -r "# " "Guide On CLAUDE.md/CLAUDE.md Collection/" | head -20
```

### 官方信息跟踪
```bash
# 检查最新同步状态
cat "Official Claude Releases/README.md"

# 查看变更日志
head -30 "Official Claude Releases/CHANGELOG.md"
```

## 项目特定指导

### 内容创建原则
1. **多语言支持** - 提供中英文版本的重要文档
2. **结构化组织** - 按技术栈和用途清晰分类模板
3. **实用性导向** - 所有模板都应该是可直接使用的
4. **社区驱动** - 鼓励社区贡献和改进

### 文件命名规范
- `CLAUDE.md` - 项目配置文件
- `README.md` / `README_中文.md` - 主文档
- `[技术栈]-[功能].md` - 模板文件命名

### 模板维护
- 定期检查模板的有效性和最新性
- 根据 Claude Code 功能更新调整配置
- 收集用户反馈并持续改进

## 贡献工作流

### 添加新模板
1. 确定模板的分类和目标用途
2. 创建结构化的 CLAUDE.md 配置
3. 添加详细的使用说明和示例
4. 提交 PR 并请求社区审查

### 更新现有内容
1. 检查内容的准确性和时效性
2. 根据最新的 Claude Code 功能更新
3. 保持与官方文档的同步
4. 维护多语言版本的一致性

### 质量控制
- 所有新增模板必须经过测试验证
- 确保配置文件语法正确且功能完整
- 提供清晰的使用文档和示例

## 技术注意事项

### Git 工作流
- 主分支: `main`
- 使用描述性的提交信息
- 大型更改通过 PR 进行审查

### 自动化同步
- 官方信息通过 GitHub Actions 每日同步
- 同步状态在 `Official Claude Releases/README.md` 中更新

### 文档维护
- README 文件需要保持中英文版本同步
- 目录结构变更时更新相关文档
- 定期检查外部链接的有效性