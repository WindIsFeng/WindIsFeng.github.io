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
