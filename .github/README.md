# GitHub Actions 配置说明

本项目配置了以下 GitHub Actions 工作流：

## 1. CI 工作流 (`ci.yml`)

**触发条件：**
- 推送到 `main`、`master`、`develop` 分支
- 创建 Pull Request 到 `main`、`master`、`develop` 分支

**功能：**
- 在 Node.js 20.x 和 22.12 版本上运行测试
- 安装依赖 (`npm ci`)
- 运行代码检查 (`npm run lint`)
- 构建项目 (`npm run build`)
- 上传构建产物作为 artifacts
- 为 PR 创建预览部署

## 2. Railway 部署工作流 (`railway-deploy.yml`)

**触发条件：**
- 推送到 `main`、`master` 分支
- 手动触发 (`workflow_dispatch`)

**功能：**
- 构建项目
- 部署到 Railway 平台

## 配置步骤

### 1. 设置 GitHub Secrets

在 GitHub 仓库的 Settings > Secrets and variables > Actions 中添加以下 secrets：

- `RAILWAY_TOKEN`: Railway 的 API token
- `RAILWAY_PROJECT_ID`: Railway 项目的 ID

### 2. 获取 Railway 凭据

1. 登录 [Railway](https://railway.app)
2. 创建新项目或选择现有项目
3. 在项目设置中找到 API token 和项目 ID

### 3. 配置 Railway 项目

确保你的 Railway 项目配置正确：
- 构建命令：`npm run build`
- 启动命令：`npm run preview`（用于预览）或 `npm start`（用于生产）

## 工作流文件说明

- `ci.yml`: 持续集成，包含代码检查和构建
- `railway-deploy.yml`: 部署到 Railway
- `railway.json`: Railway 平台配置文件

## 本地开发

### 使用 nvm 管理 Node.js 版本

```bash
# 安装指定版本的 Node.js (如果已安装 nvm)
nvm install
nvm use

# 或者直接使用 Node.js 22.12
nvm install 22.12
nvm use 22.12
```

### 开发命令

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建项目
npm run build

# 预览构建结果
npm run preview

# 运行代码检查
npm run lint
```

## Node.js 版本

项目使用 Node.js 22.12 版本，通过 `.nvmrc` 文件指定。确保本地开发环境使用相同的版本。
