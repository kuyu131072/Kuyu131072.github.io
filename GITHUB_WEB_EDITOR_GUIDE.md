# 用 GitHub 网页写作和发布博客

## 创建第一篇文章

1. 打开[博客仓库](https://github.com/kuyu131072/Kuyu131072.github.io)，确认左上方分支是 `main`。
2. 打开 [`src/content/posts/`](https://github.com/kuyu131072/Kuyu131072.github.io/tree/main/src/content/posts)，点击 **Add file → Create new file**。
3. 文件名输入 `hello-fuwari.md`。如果要给文章单独放图片，可以输入 `hello-fuwari/index.md`，GitHub 会随文件创建目录。两种方式任选一种，建议文件名用小写英文、数字和连字符。
4. 把下方模板复制进编辑器，修改标题、日期和正文。页首的两行 `---` 要保留，首行从第一个字符开始。
5. 点击 **Commit changes…**，填写提交说明，直接提交到 `main`。如果仓库要求 Pull Request，合并进 `main` 后网站才会更新。

## 可复制的文章模板

复制以下代码框**内部**的全部内容。初次发布可以直接使用，不需要先上传图片。

~~~~markdown
---
title: "我的第一篇博客"
published: 2026-11-14
description: "一篇通过 GitHub 网页发布的文章。"
image: ""
tags: ["博客", "随笔"]
category: "生活记录"
draft: false
lang: "zh-CN"
---

## 写在开头

把文章正文写在这里。行内公式可以这样写 $f(x)=x^2$。

## 公式与代码

独立公式在两行 `$$` 之间书写。

$$
\int_0^1 x^2\,dx = \frac{1}{3}
$$

```python
for number in range(3):
    print(number)
```
~~~~

| 字段 | 填写方法 |
| --- | --- |
| `title` | 必填，文章标题。标题有冒号等标点时，用引号包住。 |
| `published` | 必填，使用 `YYYY-MM-DD` 格式，例如 `2026-11-14`。 |
| `description` | 可选，文章摘要。 |
| `image` | 可选，封面路径。暂时没有图片时填 `""` 或省略。 |
| `tags` | 可选，标签数组，例如 `["摄影", "旅行"]`。无标签时填 `[]`。 |
| `category` | 可选，一个分类名称，例如 `"摄影"`。 |
| `draft` | 可选，`true` 表示草稿，`false` 表示发布，省略时默认发布。 |
| `lang` | 可选，文章语言。中文文章可以填写 `"zh-CN"`。 |
| `updated` | 可选，修改日期，格式与 `published` 相同。 |

## 封面和正文图片

推荐把图片和文章放在同一目录。先按上面的步骤创建 `hello-fuwari/index.md`，保留 `image: ""`，或者先设为草稿。提交后进入 `src/content/posts/hello-fuwari/`，点击 **Add file → Upload files**，上传图片并提交。图片已经在仓库里之后，再编辑文章添加引用。

```text
src/content/posts/hello-fuwari/
├── index.md
├── cover.jpg
└── photo.jpg
```

- **封面**在 Front Matter 写成 `image: "./cover.jpg"`。
- **正文图片**在正文写成 `![照片内容的简短说明](./photo.jpg)`。
- 如果多篇文章共用图片，也可上传到 `public/images/`。例如仓库里的 `public/images/cover.jpg`，封面写成 `image: "/images/cover.jpg"`，正文可写成 `![图片说明](/images/cover.jpg)`。
- 文件名和引用的大小写、扩展名需一致，例如 `.jpg` 与 `.jpeg` 对应不同文件。尽量使用小写英文文件名。
- 使用 `public/images/` 封面的例子可查看 [`src/content/posts/guide/index.md`](src/content/posts/guide/index.md)。

## 公式、代码和文章目录

- 行内公式用一对 `$`，例如 `$I=U/R$`。独立公式用单独两行 `$$` 包住 LaTeX。
- 代码块用三反引号包住，第一行的反引号后可写 `python`、`javascript` 等语言名以启用语法高亮。
- 用 `##` 和 `###` 分节，Fuwari 会根据标题生成文章目录。GitHub 编辑器的 Preview 与最终网页的渲染样式可能不同。

## 草稿、修改和发布

- 设置 `draft: true` 后，生产构建会排除这篇草稿。仓库是公开的，已提交的 Markdown 源文件仍可在 GitHub 上浏览。
- 准备好时把它改为 `draft: false`，提交到 `main`。
- 修改已发布文章时，打开 Markdown 文件，点击铅笔图标，编辑后再提交。保留原文件名可继续使用原来的文章链接。

## 检查部署结果

1. 提交后打开仓库的 [Actions](https://github.com/kuyu131072/Kuyu131072.github.io/actions)。
2. 打开对应这次提交的 **Deploy to GitHub Pages** 运行记录，确认 `build` 和 `deploy` 都显示绿色对勾。失败时点进红色步骤查看错误，重点检查 Front Matter 和图片路径。
3. 部署成功后，打开[博客首页](https://kuyu131072.github.io/)查看新文章。通过首页点击文章也能获得它的实际网址。
4. 若需要手动部署，在 **Actions → Deploy to GitHub Pages → Run workflow** 选择 `main`，再点击 **Run workflow**。

站点的发布来源应设为 **Settings → Pages → Build and deployment → Source → GitHub Actions**。日常写作、上传图片和查看发布结果都可以在 GitHub 网页完成。
