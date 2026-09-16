# 胡丰个人主页

这个仓库用于维护胡丰的个人学术主页：

https://windisfeng.github.io/

胡丰目前是香港城市大学博士生，主要研究方向是台风风灾建模与风险分析，研究手段包括 AI 模型、概率模型和物理模型等。

## 网站内容

- 个人简介
- 研究兴趣
- 代表性论文
- 完整论文列表
- 动态
- 简历

## 本地开发

请先在本机安装 Node.js 22（含 npm），不需要把 Node.js 程序或安装包放进项目。

安装依赖：

```bash
npm ci
```

启动本地开发服务器：

```bash
npm run dev
```

构建静态网站：

```bash
npm run build
```

每次推送到 `main` 分支后，GitHub Actions 会自动构建并发布到 GitHub Pages。

## 主要内容文件

详细操作请看 **[网站内容维护指南](docs/content-editing-guide.md)**，包含文件速查、字段说明、论文和动态模板、中英文同步规则、预览发布步骤及常见问题。

- `content/config.toml`：英文站点信息、导航和社交链接
- `content/about.toml`：英文首页模块
- `content/bio.md`：英文个人简介
- `content/publications.bib`：论文信息
- `content/news.toml`：英文动态
- `content_zh/`：中文内容
- `public/profile.jpg`：头像
- `public/papers/`：论文代表图

## 致谢

本站基于开源学术主页模板 PRISM 定制。

## 本地文件与空间管理

`node_modules/` 是本项目的本地依赖，开发和构建需要使用；可通过 `npm ci` 重建。`.next/` 是构建缓存，`out/` 是静态导出结果，停止开发服务后可删除，需要时通过 `npm run build` 重新生成。这些目录已被 Git 忽略，但云盘同步需要另外设置排除。保留 `package.json` 和 `package-lock.json`，以便恢复一致的依赖。npm 默认使用用户目录中的缓存，无需在项目中保留 `.npm-cache/`。

