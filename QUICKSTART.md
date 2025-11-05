# 🚀 快速入门

5 分钟快速启动 AKTOOLS 项目。

---

<!-- TODO 优化文档内容 -->

## 📋 前置要求

确保已安装：
- Node.js 18+
- pnpm 8+ (`npm install -g pnpm`)
- Python 3.12+

---

## ⚡ 三步启动

### 1️⃣ 安装依赖

```bash
pnpm install
```

### 2️⃣ 安装 Python 依赖

```bash
nx run aktools-server:install
```

### 3️⃣ 运行服务

```bash
pnpm dev:api
```

✅ 打开浏览器访问: http://127.0.0.1:8080/

---

## 🎯 常用命令

```bash
# 运行服务
pnpm dev:api

# 构建 Docker 镜像
pnpm docker:build

# 运行 Docker 容器
pnpm docker:run

# 查看所有项目
nx show projects

# 可视化项目依赖
nx graph
```

---

## 🐳 Docker 快速启动

```bash
# 构建并运行
pnpm docker:build
pnpm docker:run

# 查看日志
nx run aktools-server:docker-logs

# 停止
nx run aktools-server:docker-stop
```

---

## 🔧 传统 Python 方式

不想用 Nx？直接使用 Python：

```bash
cd apps/aktools-server
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python -m aktools
```

---

## ❓ 遇到问题？

**依赖安装失败**
```bash
pnpm store prune
pnpm install
```

**Python 依赖问题**
```bash
cd apps/aktools-server
pip install --upgrade pip
pip install -r requirements.txt
```

**端口被占用**
```bash
lsof -i :8080  # 查看占用进程
```

**更多帮助**
- 查看 [完整文档](./README.md)
- 访问 [Nx 官网](https://nx.dev)

---

## 🎉 下一步

- [ ] 添加 React 前端: `pnpm add -D @nx/react && nx g @nx/react:app web`
- [ ] 探索 Nx 功能: `nx list`
- [ ] 查看依赖图: `nx graph`

**Happy Coding!** 🚀
