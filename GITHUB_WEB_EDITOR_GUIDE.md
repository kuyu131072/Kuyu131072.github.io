# Fuwari 博客使用说明

在 [GitHub 仓库](https://github.com/kuyu131072/Kuyu131072.github.io) 登录后，切换到 `main` 分支。打开文件，点击右上方的铅笔图标即可编辑。上传图片用 **Add file → Upload files**，新建文章用 **Add file → Create new file**。

编辑完成后点 **Commit changes…**，填写提交说明，再选 **Commit directly to the main branch** 并确认。如果 GitHub 要求通过 Pull Request，合并到 `main` 后才会自动部署。日常操作都可以在网页完成。

| 想做什么 | 去哪里改 |
| --- | --- |
| 头像、昵称、签名 | [`src/config.ts`](src/config.ts) 的 `profileConfig` |
| 新建、编辑、隐藏或删除文章 | [`src/content/posts/`](src/content/posts) |
| 上传供多篇文章使用的图片 | [`public/images/`](public/images) |
| 改网站标题、界面语言或导航 | [`src/config.ts`](src/config.ts) |
| 编辑「关于」页面 | [`src/content/spec/about.md`](src/content/spec/about.md) |
| 检查部署 | [GitHub Actions](https://github.com/kuyu131072/Kuyu131072.github.io/actions) |

## 更换头像、昵称和签名

### 更换头像

1. 准备一张压缩好的 JPG、PNG 或 WebP，取一个新的小写英文文件名，比如 `avatar-2027.jpg`。使用新文件名，浏览器可以直接加载新地址。
2. 打开 [`src/assets/images/`](src/assets/images)，点击 **Add file → Upload files**，上传图片并提交到 `main`。
3. 打开 [`src/config.ts`](src/config.ts)，点击铅笔图标，找到 `export const profileConfig`。将 `avatar` 改为 `"assets/images/avatar-2027.jpg"`，再提交。
4. 部署成功后打开[博客首页](https://kuyu131072.github.io/)，查看侧栏头像。上传新文件和切换引用分两次提交时，以第二次部署为准。

### 更换昵称和签名

两项也在 `profileConfig` 内。当前头像、昵称和签名对应的三行如下。修改引号里的文字并保留行尾逗号。

```ts
avatar: "assets/images/profile-avatar.jpg",
name: "逸夫",
bio: "浩然正气",
```

`name` 是侧栏昵称，也用于页脚署名和文章作者元数据。`bio` 是侧栏签名。网页标题由同一个文件里的 `siteConfig.title` 和 `siteConfig.subtitle` 设置。

## 发布文章

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
| `published` | 必填，使用 `YYYY-MM-DD` 格式，例如 `2026-11-14`，发文时请换成实际日期。 |
| `description` | 可选，文章摘要。 |
| `image` | 可选，封面路径。暂时没有图片时填 `""` 或省略。 |
| `tags` | 可选，标签数组，例如 `["摄影", "旅行"]`。无标签时填 `[]`。 |
| `category` | 可选，一个分类名称，例如 `"摄影"`。 |
| `draft` | 可选，`true` 表示草稿，`false` 表示发布，省略时默认发布。 |
| `lang` | 可选，文章语言。中文文章可以填写 `"zh-CN"`。 |
| `updated` | 可选，修改日期，格式与 `published` 相同。 |

## 封面和正文图片

已有 `.md` 文件时，也可以在文章目录用 **Add file → Upload files** 上传。上传前先补齐上述 Front Matter。

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
- 上传前可把照片另存成 8 位 JPEG，使用压缩后的副本。图片在 `public/images/` 时会以仓库中的大小直接提供给访客。
- 文件名和引用的大小写、扩展名需一致，例如 `.jpg` 与 `.jpeg` 对应不同文件。尽量使用小写英文文件名。
- 使用 `public/images/` 封面的例子可查看 [`src/content/posts/guide/index.md`](src/content/posts/guide/index.md)。

## 公式、代码和文章目录

- 行内公式用一对 `$`，例如 `$I=U/R$`。独立公式用单独两行 `$$` 包住 LaTeX。
- 代码块用三反引号包住，第一行的反引号后可写 `python`、`javascript` 等语言名以启用语法高亮。
- 用 `##` 和 `###` 分节，Fuwari 会根据标题生成文章目录。GitHub 编辑器的 Preview 与最终网页的渲染样式可能不同。

## 编辑、隐藏、恢复和删除文章

| 操作 | 在 GitHub 网页上怎么做 | 部署后的效果 |
| --- | --- | --- |
| 编辑 | 打开对应的 `.md` 文件，点铅笔，修改后提交。 | 更新内容。保留文件路径即可继续使用原网址。 |
| 隐藏 | 编辑文件顶部，将 `draft: false` 改为 `draft: true` 后提交。原来没有 `draft` 时，在两行 `---` 之间添加这一行。 | 文章退出首页、归档和搜索，原文章网址也会下线。 |
| 恢复发布 | 将 `draft: true` 改为 `draft: false` 后提交。 | 文章按原路径重新上线。 |
| 删除 | 打开文章的 `.md` 文件，点右上角的 **… → Delete file**，再点 **Commit changes…** 提交。文件夹形式的文章应删除其中的 `index.md`。 | 文章从当前版本移除。Git 提交历史仍会保存旧版本。 |

临时下架用草稿最方便。仓库是公开的，草稿的 Markdown 和已提交图片在 GitHub 上仍可见。删掉文章也会留下提交历史。私密草稿请先留在自己的编辑器里。

删文后如果想清理图片，先确认其他文章没有引用它，再单独删除。放在 `public/images/` 的图片有独立网址，会继续随博客部署，直到从该目录移除。

例如，已发布的《习概》对应 [`src/content/posts/xigai-review.md`](src/content/posts/xigai-review.md)。Fuwari 的五篇示例当前都设为草稿，恢复其中任意一篇只需修改那篇的 `draft`。

## 其他常用设置

| 想改什么 | 编辑位置 |
| --- | --- |
| 页签与站点名称 | `src/config.ts` → `siteConfig.title` 和 `siteConfig.subtitle` |
| 界面改成简体中文 | `src/config.ts` → `siteConfig.lang` 填 `"zh_CN"`。文章自己的 `lang` 可填 `"zh-CN"`。 |
| 顶部导航的 GitHub 链接 | `src/config.ts` → `navBarConfig.links` 中相应的 `url` |
| 侧栏的社交图标链接 | `src/config.ts` → `profileConfig.links`。想全部隐藏时可以写 `links: [],`。 |
| 首页横幅 | `src/config.ts` → `siteConfig.banner`。上传图片后改 `src`，再把 `enable` 改为 `true`。横幅与各篇文章的 `image` 字段分别设置。 |
| 「关于」页面的正文 | [`src/content/spec/about.md`](src/content/spec/about.md)，用 Markdown 编辑。 |

## 检查部署结果

1. 提交后打开仓库的 [Actions](https://github.com/kuyu131072/Kuyu131072.github.io/actions)。
2. 打开对应这次提交的 **Deploy to GitHub Pages** 运行记录，确认 `build` 和 `deploy` 都显示绿色对勾。失败时点进红色步骤查看错误，重点检查 Front Matter 和图片路径。
3. 部署成功后，打开[博客首页](https://kuyu131072.github.io/)查看新文章。通过首页点击文章也能获得它的实际网址。
4. 若需要手动部署，在 **Actions → Deploy to GitHub Pages → Run workflow** 选择 `main`，再点击 **Run workflow**。

如果部署已成功、浏览器还显示旧页面，可按 `Ctrl+Shift+R`（Mac 用 `⌘+Shift+R`）强制刷新，或在无痕窗口核验。GitHub Pages 的发布来源已经配置为 **GitHub Actions**，这个选项位于 **Settings → Pages → Build and deployment → Source**。
