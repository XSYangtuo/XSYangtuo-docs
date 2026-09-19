# XSYangtuo-docs

XSYangtuo 的文章发布站，用 MkDocs Material 构建，发布在 <https://xsyangtuo.github.io/XSYangtuo-docs/>。

## 目录结构

```
mkdocs.yml                                  站点配置（主题、导航、Markdown 扩展）
requirements.txt                            构建依赖（版本已固定）
docs/
  index.md                                  首页
  XSYangtuodocs/
    index.md                                文章目录（所有 chapter 一览）
    chapter1/                               第一篇文章
      assets/*.png                          该篇全部配图
      00-README-索引与注释.md                阅读顺序、术语表、背景速查、原文链接
      01-正文-给AI时代泼一层温水.md           正文
      02-搬运-Fable《走》全文.md
      03-事件-大物普物讲义风波.md
      04-热评精选.md
      05-相关帖子摘要.md
.github/workflows/deploy.yml                push 到 main 后自动构建并发布
```

一篇文章 = 一个 `docs/XSYangtuodocs/chapterN/` 目录，正文、注释、配图都放在该目录内，篇与篇之间互不影响。

## 本地预览

```bash
python -m venv .venv
.venv/Scripts/pip install -r requirements.txt   # Windows；Linux/macOS 用 .venv/bin/pip
.venv/Scripts/mkdocs serve                      # 打开 http://127.0.0.1:8000
```

构建产物检查（严格模式，坏链接、缺图、缺页都会直接报错）：

```bash
.venv/Scripts/mkdocs build --strict
```

## 发布

push 到 `main` 即自动发布：GitHub Actions 安装依赖 → `mkdocs build --strict` → `mkdocs gh-deploy`，把构建产物推到 `gh-pages` 分支。

**首次需要在仓库 Settings → Pages 里选一次 Source**（两种都能用，任选其一）：

| 方式 | 设置 | 说明 |
| --- | --- | --- |
| **Deploy from a branch**（推荐） | Branch 选 `gh-pages`，目录选 `/(root)` | 站点地址 <https://xsyangtuo.github.io/XSYangtuo-docs/>；分支已由 Actions 维护，选完即可访问 |
| **GitHub Actions** | Source 选 `GitHub Actions` | 走官方 Pages 发布链路，workflow 里已备好，选完需再跑一次 workflow |

手动发布（本地已装好依赖时）：

```bash
mkdocs gh-deploy --force
```

## 新增一篇文章

1. 建目录 `docs/XSYangtuodocs/chapter2/`，把 Markdown 和配图（放 `assets/`）拷进去；
2. 在 `mkdocs.yml` 的 `nav` 里，照 `chapter1` 的写法加一段；
3. 在 `docs/XSYangtuodocs/index.md` 的表格里加一行；
4. 本地 `mkdocs build --strict` 确认无告警后 push。

图内引用写相对路径（`assets/xxx.png`）即可，同一目录内的文章互引用也写相对文件名，构建时会自动转成站点链接。

## 内容来源与版权

- 站内正文均为 CC98 论坛原帖及回帖的**原文搬运，未改一字**，著作权归原作者及各位回帖用户所有；
- 标注【**AI 整理者注**】的段落、导读、术语表与章节编排为 **AI** 生成，不代表原作者观点；
- `chapter1/02-搬运-Fable《走》全文.md` 为他人作品的全文搬运，**侵删**，删除该文件不影响其余文档。
