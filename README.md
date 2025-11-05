# AKTOOLS Monorepo

这是一个使用 Nx 管理的 monorepo 项目，包含 AKTOOLS 的后端服务和（未来的）前端应用。

More detail about AKTOOLS: https://github.com/akfamily/aktools?tab=readme-ov-file

<!-- TODO 优化文档内容 -->

> 💡 **第一次使用？** 查看 [快速入门指南](./QUICKSTART.md) 立即开始！

---

## 📦 项目结构

```
aktools-monorepo/
├── apps/
│   ├── aktools-server/      # Python FastAPI 后端服务
│   └── web/                 # (预留) React 前端应用
├── packages/                # (预留) 共享代码库
├── nx.json                  # Nx 配置
├── package.json             # Node.js 依赖
└── README.md
```

### 为什么使用 Monorepo？

- ✅ **统一管理**: 一套工具管理前后端项目
- ✅ **代码共享**: 便于共享类型定义、工具函数等
- ✅ **任务编排**: Nx 自动处理任务依赖关系
- ✅ **智能缓存**: 只重新运行变更的部分
- ✅ **可扩展**: 轻松添加新的应用和库

---

## 🚀 快速开始

### 前置要求

- Node.js 18+
- pnpm 8+
- Python 3.12+
- Docker (可选)

### 安装和运行

```bash
# 1. 安装依赖
pnpm install

# 2. 安装 Python 依赖
nx run aktools-server:install

# 3. 运行服务
pnpm dev:api

# 访问 http://127.0.0.1:8080/
```

详细步骤请查看 [快速入门指南](./QUICKSTART.md)

---

## 📖 命令参考

### 开发命令

| 任务 | 命令 | 说明 |
|------|------|------|
| 运行服务 | `pnpm dev:api` | 启动开发服务器 |
| 安装 Python 依赖 | `nx run aktools-server:install` | 安装 requirements.txt |
| 查看项目 | `nx show projects` | 列出所有项目 |
| 项目依赖图 | `nx graph` | 可视化项目关系 |

### Docker 命令

| 任务 | 命令 |
|------|------|
| 构建镜像 | `pnpm docker:build` |
| 运行容器 | `pnpm docker:run` |
| 查看日志 | `nx run aktools-server:docker-logs` |
| 停止容器 | `nx run aktools-server:docker-stop` |

---

## 🔧 传统方式运行（不使用 Nx）

如果你更喜欢传统的 Python 开发方式：

```bash
cd apps/aktools-server

# 创建虚拟环境
python -m venv venv
source venv/bin/activate

# 安装依赖
pip install -r requirements.txt

# 运行服务
python -m aktools
```

---

## ➕ 添加新项目

### 添加 React 前端

```bash
# 安装 React 插件
pnpm add -D @nx/react

# 生成应用
nx g @nx/react:app web
```

### 添加共享库

```bash
# TypeScript 库
nx g @nx/js:lib shared-types

# React 组件库
nx g @nx/react:lib ui-components
```

---

## 📚 Monorepo 迁移说明

本项目已从单体 Python 项目迁移到 Nx monorepo 结构。

### 目录变化对比

**之前:**
```
AKTOOLS-SERVER/
├── requirements.txt
├── Dockerfile
└── README.md
```

**现在:**
```
AKTOOLS-SERVER/
├── apps/aktools-server/      # Python 项目移到这里
│   ├── requirements.txt
│   ├── Dockerfile
│   └── README.md
├── apps/web/                 # 预留前端
├── packages/                 # 预留共享库
├── nx.json
└── package.json
```

### 命令对照表

| 操作 | 原命令 | 新命令 |
|------|--------|--------|
| 安装依赖 | `pip install -r requirements.txt` | `nx run aktools-server:install` |
| 运行服务 | `python -m aktools` | `pnpm dev:api` |
| 构建镜像 | `docker build -t aktools-server .` | `pnpm docker:build` |
| 运行容器 | `docker run -d -p 8080:8080 ...` | `pnpm docker:run` |

### 兼容性保证

- ✅ 所有原有功能保持不变
- ✅ 可以继续使用传统 Python 方式（进入 `apps/aktools-server/` 目录）
- ✅ Docker 配置完全兼容
- ✅ Python 依赖版本不变

---

## ❓ 常见问题

<details>
<summary><strong>Q: 为什么要迁移到 monorepo?</strong></summary>

A: 为了统一管理前后端代码，便于代码共享和协作，同时保持各项目的独立性。未来可以添加 React 前端、共享类型库等。
</details>

<details>
<summary><strong>Q: Nx 会影响 Python 项目的运行吗?</strong></summary>

A: 不会。Python 项目可以完全独立运行，Nx 只是提供了一个可选的管理层。你可以直接进入 `apps/aktools-server/` 使用传统方式开发。
</details>

<details>
<summary><strong>Q: 必须使用 Nx 命令吗?</strong></summary>

A: 不必须。你可以继续使用传统的 Python 命令，只需进入 `apps/aktools-server/` 目录即可。Nx 是为了提升效率，不是必需的。
</details>

<details>
<summary><strong>Q: 如何回滚到原有结构?</strong></summary>

A: 如果需要回滚：
```bash
# 复制文件回根目录
cp apps/aktools-server/requirements.txt .
cp apps/aktools-server/Dockerfile .

# 删除 Nx 相关
rm -rf apps packages node_modules
rm package.json nx.json pnpm-lock.yaml
```
</details>

<details>
<summary><strong>Q: pnpm 和 npm 有什么区别?</strong></summary>

A: pnpm 更快、更省空间，且对 monorepo 支持更好。如果你更喜欢 npm，只需将 `pnpm` 命令替换为 `npm` 即可。
</details>

---

## 📖 参考资源

- [Nx 官方文档](https://nx.dev)
- [Nx Python 插件](https://github.com/lucasvieirasilva/nx-plugins)
- [AKTOOLS GitHub](https://github.com/akfamily/aktools)
- [FastAPI 文档](https://fastapi.tiangolo.com/)
- [pnpm 文档](https://pnpm.io/)
