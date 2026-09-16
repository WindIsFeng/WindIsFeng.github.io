# 网站内容维护指南

本指南按项目当前代码编写。所有路径相对于项目根目录。日常更新主要修改 `content/`、`content_zh/` 和 `public/`。

## 1. 修改位置速查

| 要修改的内容 | 英文文件 | 中文文件或共享位置 |
| --- | --- | --- |
| 姓名、身份、学校、邮箱、社交链接 | `content/config.toml` | `content_zh/config.toml` |
| 导航名称、顺序、页脚更新时间 | `content/config.toml` | `content_zh/config.toml` |
| 首页个人简介 | `content/bio.md` | `content_zh/bio.md` |
| 首页研究兴趣、模块标题、顺序、代表作数量 | `content/about.toml` | `content_zh/about.toml` |
| 动态 | `content/news.toml` | `content_zh/news.toml` |
| 论文条目、作者、排序、代表图 | `content/publications.bib` | 当前中英文共用这一个文件 |
| 论文页面标题和介绍 | `content/publications.toml` | `content_zh/publications.toml` |
| 研究项目 | `content/projects.toml` | `content_zh/projects.toml` |
| 简历正文 | `content/cv.md` | `content_zh/cv.md` |
| 简历页面标题 | `content/cv.toml` | `content_zh/cv.toml` |
| 头像 | `public/profile.jpg` | 中英文共享 |
| 论文代表图 | `public/papers/` | 由论文的 `preview` 指定 |
| 浏览器图标 | `public/favicon.svg` | 默认配置的 `[site].favicon` 指定路径 |
| 查看全部、摘要、展开等固定按钮文字 | `src/lib/i18n/messages.ts` | 同一个文件维护两种语言 |

每次更新建议按顺序：修改内容 → 同步中英文 → 更新页脚日期 → 预览 → 构建 → 发布。

## 2. 中英文同步规则

- `content/` 是默认内容，也是当前英文内容目录；`content_zh/` 是中文内容。
- 网站不会自动翻译。简介、动态、项目和简历需要分别维护两份。
- 普通内容按整个文件回退：中文目录没有该文件时，使用默认目录中的同名文件；已有中文文件时，不会自动合并英文文件的新条目。
- 当前没有 `content_zh/publications.bib`，所以新增论文只需修改 `content/publications.bib`。如果以后创建中文 BibTeX 文件，两份列表就需要分别维护。
- `config.toml` 特殊：中文的 `site`、`author`、`social` 字段覆盖默认字段；中文导航整体替换默认导航。`features`、`i18n` 始终读取 `content/config.toml`。
- `public/` 中图片和附件共享，不必为中文再复制一份。

## 3. 个人信息、链接、头像和更新时间

在两份 `config.toml` 的原有段落中修改，不要在文件末尾重复添加同名段落。

| 段落 | 字段 | 作用 |
| --- | --- | --- |
| `[site]` | `title` | 站点名称；默认配置也用于网页标题 |
| `[site]` | `description` | 站点描述；网页元信息读取默认配置 |
| `[site]` | `last_updated` | 页脚更新时间，需要手动维护 |
| `[author]` | `name` | 姓名，也用于论文作者高亮匹配 |
| `[author]` | `title`、`institution` | 身份、学校或单位 |
| `[author]` | `avatar` | 头像网址路径，例如 `/profile.jpg` |
| `[social]` | `email` | 邮箱地址，不加 `mailto:` |
| `[social]` | `location`、`location_url` | 地点文字和地图链接 |
| `[social]` | `location_details` | 位置详情的字符串数组 |
| `[social]` | `google_scholar`、`orcid`、`github` | 对应个人主页的完整网址 |

例如把英文 `[site]` 中的日期改为 `last_updated = "September 16, 2026"`，中文改为 `last_updated = "2026年9月16日"`，使用实际修改日期。编辑正文不会自动更新日期。

身份、单位或联系方式变化时，也检查两份 `bio.md`、`cv.md` 中的重复信息，它们不会随配置自动更新。切换语言不会重新生成中文网页元信息。

更换头像最简单的方法是替换 `public/profile.jpg`，保持实际图片格式与扩展名一致。若改为 `portrait.png`，两份配置的 `avatar` 都改为 `/portrait.png`。图标建议继续使用 SVG；当前页面代码明确指定了 SVG 类型。

资源路径规则：`public/profile.jpg` 对应网址 `/profile.jpg`，网址不写 `public/`。文件名大小写必须一致，建议使用英文小写和连字符。

## 4. 个人简介和研究兴趣

简介分别编辑两份 `bio.md`，支持基本 Markdown：

```markdown
我目前在**某大学**从事台风风灾研究。

研究方向包括：
- 台风风场建模
- 风险分析

更多信息见[个人主页](https://example.com)。
```

示例内容和链接请替换成真实信息；段落之间留空行。

首页侧栏研究兴趣在两份 `about.toml` 的 `[profile]` 中修改：

```toml
[profile]
research_interests = [
  "Tropical Cyclone",
  "Natural Hazards",
  "Deep Learning",
  "Climate Change"
]
```

中文文件可使用中文术语。侧栏兴趣、简介、简历中的研究方向不会自动同步。

## 5. 新增或删除动态

在 `content/news.toml` 顶部新增完整条目：

```toml
[[news]]
date = "2026-09"
content = "Our new paper was accepted by JOURNAL NAME."
```

在 `content_zh/news.toml` 顶部添加对应中文：

```toml
[[news]]
date = "2026-09"
content = "我们的新论文被某期刊接收。"
```

- 用真实日期和内容替换示例，日期建议用 `YYYY-MM`。
- 动态按文件顺序显示，不自动按日期排序；最新条目放最前面。
- 当前显示全部动态。删除时移除完整的 `[[news]]`、`date`、`content` 块。
- 动态按纯文本显示，不解析 Markdown；`[论文](网址)` 不会变成链接。

## 6. 新增、更新和排序论文

### 新增论文模板

编辑 `content/publications.bib`，可复制一条相似论文再修改。以下模板中的论文信息、DOI 和图片名都是占位内容，使用前必须替换；没有的可选字段直接删除。

```bibtex
@article{hu2026example,
  title = {Replace with the actual paper title},
  author = {Feng Hu and Firstname Lastname},
  year = {2026},
  month = {9},
  journal = {Replace with the actual journal},
  doi = {10.xxxx/replace-with-real-doi},
  selected = {true},
  sort_order = {0},
  preview = {example-paper.png},
  description = {A short summary of the contribution.},
  abstract = {The full abstract.},
  keywords = {Tropical cyclone, Risk analysis}
}
```

`hu2026example` 是唯一标识，需要换成未使用过的名称。字段间保留逗号，花括号配对，字段名推荐小写。

| 字段 | 填写方法与作用 |
| --- | --- |
| `title` | 论文标题 |
| `author` | 作者间用 ` and ` 分隔；可写 `Feng Hu` 或 `Hu, Feng`，不要用逗号分隔不同作者 |
| `year`、`month` | 实际年份和月份，月份可用 `{9}` 或 `{sep}` |
| `journal` | 期刊名；会议论文可用 `booktitle` |
| `volume`、`number`、`pages` | 卷、期、页码或文章编号 |
| `doi` | 仅填写 `10.…/…`，不带 `https://doi.org/`，页面会自动补齐 |
| `code` | 代码仓库完整网址，显示代码按钮 |
| `selected` | `{true}` 或 `{yes}` 入选首页代表作；删除或设为 `{false}` 则不入选 |
| `sort_order` | 数值越小越靠前，影响论文列表和首页代表作 |
| `preview` | `public/papers/` 内的图片文件名 |
| `description` | 卡片上的简短介绍，过长会截断 |
| `abstract` | 完整摘要，在论文列表中点击摘要按钮展开 |
| `keywords` | 用英文逗号分隔的关键词 |

当前论文卡片显示 DOI、代码、摘要、BibTeX 按钮。虽然解析器读取 `url`，但没有对应通用链接按钮；新增 `pdf` 字段也不会自动生成 PDF 按钮。

### 代表图

1. 把图片放到 `public/papers/example-paper.png`。
2. 在论文条目中写 `preview = {example-paper.png}`。
3. 检查首页和完整论文列表的图片。

`preview` 只填文件名，不加 `/papers/` 或 `public/papers/`。没有图片时删除该字段即可。

### 代表作和排序

- 首页先筛选 `selected` 为 `true` 或 `yes` 的论文，然后从排序结果中取前几篇。
- 数量由两份 `about.toml` 中 `id = "featured_publications"` 模块的 `limit` 控制，目前为 `5`。
- 排序首先按 `sort_order` 升序；设置该字段的条目排在未设置的条目前面。两篇都没设置时，才按年份、月份从新到旧排序。
- 当前论文已使用手动排序，因此新论文若不写 `sort_order`，即使年份更新，也可能排在后面。
- 若当前最小值为 `1`，新论文可用 `0` 置顶；也可统一重新编号。建议避免重复值。
- 仅移动条目在 BibTeX 文件中的位置，不能代替修改排序字段。
- `limit` 使用正整数；设为 `0` 会回退到默认 `5`。隐藏代表作模块应移除完整模块配置。

### 作者标记和投稿状态

作者名后的 `#` 表示共同作者标记，页面显示下划线；`*` 表示通讯作者，页面显示上标星号：

```bibtex
author = {Feng Hu# and Firstname Lastname# and Another Author*},
```

本人姓名根据站点配置自动高亮；展开的 BibTeX 会去掉作者标记及网站自定义展示字段。

期刊论文用 `@article`，会议论文用 `@inproceedings`，未发表稿件可沿用当前的 `@misc`。当前未发表稿件在 `journal`、`description` 中写明 `Manuscript under review` 等状态，不要依赖新增 `status` 字段改变展示。正式发表时检查条目类型、期刊、日期、卷期页、DOI、简介和摘要。

## 7. 修改研究项目

两份 `projects.toml` 顶部的 `title`、`description` 是页面标题和介绍，每个 `[[items]]` 是一个项目。新增示例：

```toml
[[items]]
title = "项目名称（项目编号）"
subtitle = "承担角色或资助来源"
date = "2026–2029"
tags = ["台风", "风险分析"]
content = """
第一段介绍研究目标。

第二段介绍方法和预期成果。

更多信息见[项目主页](https://example.com)。
"""
```

替换示例信息。`subtitle`、`date`、`tags` 可省略。项目按文件顺序显示，调整顺序时移动完整条目。正文三引号之间可换行；展开后支持 Markdown，收起时显示压缩后的纯文本预览，适合把简短概述放在第一段。

## 8. 修改简历和添加 PDF

修改两份 `cv.md` 中的教育经历、研究方向、联系方式。页面标题在两份 `cv.toml` 中修改，保留 `source = "cv.md"`。

添加 PDF 下载：

1. 自行准备 PDF，放入 `public/`，例如 `cv-en.pdf`、`cv-zh.pdf`。
2. 英文 `cv.md` 添加 `[Download CV (PDF)](/cv-en.pdf)`。
3. 中文 `cv.md` 添加 `[下载简历（PDF）](/cv-zh.pdf)`。

这些 PDF 需要实际提供；网页内容和 PDF 不会自动同步，后续要分别更新。

## 9. 首页模块、导航、新页面和语言

### 首页模块

两份 `about.toml` 的 `[[sections]]` 按文件顺序显示。改标题用 `title`；改顺序移动整块；隐藏模块移除整块，原内容文件可以保留。简介和动态的 `source` 只写内容目录内的文件名，不加 `content/` 前缀。日常修改保留原有 `id`、`type`、`source`。

### 导航与新增文字页面

导航由两份 `config.toml` 的 `[[navigation]]` 控制，按文件顺序显示。只改名称时修改 `title`，不用改 `target` 和 `href`。

以增加教学页面 `/teaching` 为例：

1. 新建 `content/teaching.md`、`content_zh/teaching.md`，分别写两种语言正文。
2. 新建 `content/teaching.toml`：

```toml
type = "text"
title = "Teaching"
source = "teaching.md"
```

3. 新建 `content_zh/teaching.toml`，内容相同，把 `title` 改为 `"教学"`。
4. 在英文 `config.toml` 的导航列表中添加：

```toml
[[navigation]]
title = "Teaching"
type = "page"
target = "teaching"
href = "/teaching"
```

5. 中文配置添加同样的导航块，标题改为 `"教学"`。
6. 重新构建，检查新页面。

静态页面路径由默认 `content/config.toml` 的导航生成，因此只添加中文导航或正文文件是不够的。当前中英文共用 `/publications`、`/projects`、`/cv` 等路径，通过界面切换语言，不要自行加 `/zh/` 前缀。

### 默认语言

只修改 `content/config.toml` 的现有 `[i18n]`。当前初始语言固定为英文，并记住用户的选择。如需首次访问默认中文，修改：

```toml
default_locale = "zh"
mode = "fixed"
fixed_locale = "zh"
```

保留现有其他设置。`persist = true` 时老访客此前选择的语言优先，验证首次访问效果可用无痕窗口。日常内容更新不用改语言及 `features` 设置。

## 10. 格式注意事项

- 使用 UTF-8 保存文件。
- TOML 字符串使用英文双引号，布尔值用 `true`、`false`，数量用数字。
- `[site]` 等为单个配置段；`[[news]]`、`[[items]]` 为可重复条目，不要漏掉一层方括号。
- 单行字符串内的双引号用 `\"` 转义；长段落参考项目正文的三引号写法。
- 字段必须放在正确段落里，例如 `last_updated` 属于 `[site]`，写在 `[social]` 下不会更新页脚。
- 示例里的新图片、PDF 和网址需要自行提供或替换，不使用的可选字段应删除。

## 11. 预览、构建和发布

### 本地预览

安装 Node.js 22，在项目根目录打开终端。首次使用或依赖需重装时执行：

```bash
npm ci
```

已有依赖时，日常只改内容不必重新安装。启动预览：

```bash
npm run dev
```

打开终端提示的地址，通常是 `http://localhost:3000`。保存后刷新；如内容未变化，停止服务再启动。按 `Ctrl+C` 停止。

### 发布前清单

- [ ] 分别检查中英文首页、论文、项目、简历。
- [ ] 新论文出现在完整列表；代表作也出现在首页，数量和顺序正确。
- [ ] 图片、DOI、代码、PDF 链接有效。
- [ ] 项目展开正文和窄屏显示正常。
- [ ] 两种语言页脚日期已更新。
- [ ] 停止开发预览后执行构建并确认成功：

```bash
npm run build
```

构建输出位于 `out/`，不要直接修改 `out/` 或 `.next/`，它们会被重新生成。项目使用静态导出，日常预览使用 `npm run dev`，不要把 `npm start` 当作静态导出预览方式。

### 发布到线上

`.github/workflows/deploy.yml` 已配置推送到 `main` 后自动构建并发布 GitHub Pages：

1. 在 Git 客户端检查改动，只选择本次所需文件。
2. 创建提交，例如“更新论文和九月动态”。
3. 推送到远程 `main`；其他分支需要合并到 `main` 后才触发该自动发布。
4. 在 GitHub 仓库 **Actions** 中查看 **Deploy personal homepage to GitHub Pages**，确认构建、部署均成功。
5. 检查[线上网站](https://windisfeng.github.io/)，必要时强制刷新。

保存文件或本地构建不会直接更新线上。若 Git 客户端提示不是有效仓库，先确认打开了可用仓库副本及正确远程地址，不要直接重新初始化仓库来绕过问题。

## 12. 常见问题

| 问题 | 优先检查 |
| --- | --- |
| 英文更新了，中文没变 | 是否同步修改已有的 `content_zh/` 文件 |
| 动态顺序不对 | 按文件顺序显示，移动完整条目 |
| 新论文未上首页 | `selected` 是否为小写 `true` / `yes`，是否超出 `limit` |
| 新论文排在后面 | 是否遗漏 `sort_order` |
| 论文图片不显示 | 文件是否在 `public/papers/`，`preview` 是否仅为文件名，大小写是否一致 |
| DOI 打不开 | 是否误填完整网址或占位 DOI |
| `url`、`pdf` 没有按钮 | 当前卡片未实现，需要修改组件 |
| 动态里的 Markdown 原样显示 | 动态按纯文本渲染 |
| TOML 修改后模块消失或构建失败 | 检查引号、数组、重复字段、方括号、所属段落及终端错误 |
| PDF 404 | 是否提供实际文件，链接是否去掉 `public/` 前缀 |
| 新页面发布后 404 | 是否添加默认配置的导航，`target` 是否匹配配置文件名 |
| 默认语言不变 | 浏览器记住旧选择，切换语言或用无痕窗口验证 |
| 页脚日期没变 | 是否修改两份配置的 `[site].last_updated` |
| 本地更新而线上没变 | 是否推送到 `main`，Actions 是否成功，浏览器是否有缓存 |

## 13. 改布局时参考的代码

| 调整目标 | 文件 |
| --- | --- |
| 头像、侧栏信息布局 | `src/components/home/Profile.tsx` |
| 简介、动态、代表作样式 | `src/components/home/About.tsx`、`src/components/home/News.tsx`、`src/components/home/SelectedPublications.tsx` |
| 完整论文列表及按钮 | `src/components/publications/PublicationsList.tsx` |
| 项目卡片与展开行为 | `src/components/pages/CardPage.tsx` |
| 导航、页脚 | `src/components/layout/Navigation.tsx`、`src/components/layout/Footer.tsx` |
| 全局样式 | `src/app/globals.css` |
| 论文字段解析与排序 | `src/lib/bibtexParser.ts` |
| 内容回退与配置合并 | `src/lib/content.ts`、`src/lib/config.ts` |

这些位置用于改变样式或增加功能；日常内容更新按前述文件操作即可。
