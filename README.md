# ?CTF 2025 等待页面

这是一个使用Vue.js构建的CTF比赛等待页面，包含倒计时功能和比赛信息展示。

## 项目结构

- `waiting-page-vue/` - Vue.js项目主目录
- `.github/workflows/deploy.yml` - GitHub Actions自动部署配置

## 本地开发

1. 进入项目目录：
   ```bash
   cd waiting-page-vue
   ```

2. 安装依赖：
   ```bash
   npm install
   ```

3. 启动开发服务器：
   ```bash
   npm run dev
   ```

4. 构建生产版本：
   ```bash
   npm run build
   ```

## 自动部署

项目配置了GitHub Actions自动部署到GitHub Pages：

1. 当代码推送到`main`或`master`分支时，会自动触发构建
2. 构建完成后会自动部署到`gh-pages`分支
3. 可通过GitHub Pages访问部署的页面

### 部署配置说明

- **触发条件**：推送到main/master分支
- **构建环境**：Ubuntu最新版本，Node.js 18
- **构建路径**：`waiting-page-vue/dist`
- **部署分支**：`gh-pages`

### 启用GitHub Pages

1. 进入仓库的Settings页面
2. 找到Pages设置
3. 选择Source为"Deploy from a branch"
4. 选择分支为`gh-pages`，目录为`/ (root)`
5. 保存设置

部署完成后，页面将可通过 `https://[用户名].github.io/waiting-page/` 访问。

## 功能特性

- 📅 双赛道倒计时显示
- 📱 响应式设计，支持移动端
- 🎨 现代化UI设计
- ⚡ 基于Vite的快速构建
- 🚀 自动化部署到GitHub Pages