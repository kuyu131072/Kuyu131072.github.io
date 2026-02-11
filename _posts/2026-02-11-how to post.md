---
title: how to post
date: 2026-02-11 12:00:00 +0800
categories: [生活]
tags: [日记]
---
我发现这里可以写md格式：

使用什么样的md格式来发博客来着？这里我引用ai的回答：

### 如何写文章？

以后你甚至不需要 Codespaces 了，直接在网页上操作：

1. 进入 _posts 文件夹。
2. 点击右上角 **Add file** -> **Create new file**。
3. 文件名必须是：2024-01-30-我的第一篇文章.md (日期-标题.md)。
4. 内容复制下面的模板：codeMarkdown
    - `--
    title: 我的第一篇文章
    date: 20240130 12:00:00 +0800
    categories: [生活]
    tags: [日记]
    --
    ## 你好，世界
    这是我的第一篇博客，完全在浏览器上完成！`
5. 点击 **Commit changes**。
6. 等待几分钟，刷新你的博客网址，文章就出现了。
嗯所以，写文章就是这么简单，

## 那么下一步，如何插入背景图，在文章中插入图片和视频，修改我的头像？

### 修改头像 (最简单)

Chirpy 的头像显示在左侧边栏（电脑端）或顶部（手机端）。

1. **上传图片**：
    - 准备一张**正方形**的图片（建议 512x512 像素），重命名为 avatar.jpg（或者 .png）。
    - 在 GitHub 仓库里，进入 assets -> img 文件夹。
    - 点击右上角 **Add file** -> **Upload files**，把图片传上去。
    - **重要**：一定要点击绿色的 **Commit changes** 保存。
2. **修改配置**：
    - 回到仓库根目录，打开 _config.yml。
    - 搜索 avatar:。
    - 修改路径为：codeYaml
        
        `avatar: /assets/img/avatar.jpg`
        
    - 保存提交。等几分钟，刷新博客，头像就变了。

### 在文章中插入图片 (谨记“先上传后引用”)

1. **第一步：上传**
    - 把你想插入的图片重命名（最好用英文，比如 code-demo.jpg）。
    - 像上传头像一样，把它上传到 assets/img/ 文件夹里。
    - *进阶技巧：为了整洁，你可以在 img 下面新建文件夹，比如 assets/img/2024/，但初学者直接放 img 里也没问题。*
2. **第二步：引用**
    - 在你的文章 .md 文件里，想显示图片的地方写：codeMarkdown
        
        `![这里写图片的描述](/assets/img/code-demo.jpg)`
        
    - **注意**：前面的 / 不能少，这代表从根目录开始找。

---

### 3. 在文章中插入视频 (推荐 Bilibili/YouTube)

我不建议你把视频文件（如 mp4）直接上传到 GitHub。

**原因**：GitHub 仓库有容量限制，且视频加载很慢，不仅卡顿还会把你的流量跑光。

**Geek 的做法**：视频传到 B 站或 YouTube，然后把视频“嵌入”进来。

### 插入 Bilibili 视频：

1. 在 B 站打开你的视频。
2. 点击视频下方的 **分享** 按钮（转发图标）。
3. 找到 **“嵌入代码”**，复制那一串以 <iframe 开头的代码。
4. 直接粘贴到你的 Markdown 文章里即可。

*为了让视频在手机上也能自适应宽度，你可以用这段优化的代码包裹它：*

codeHtml

`<style>
.video-container { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; }
.video-container iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
</style>
<div class="video-container">
    <!-- 把你在 B 站复制的 iframe 代码粘贴在这里，去掉原来的 width 和 height 属性 -->
    <iframe src="//player.bilibili.com/player.html?bvid=你的视频ID&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
</div>`

---

### 4. 插入全站背景图 (高阶操作：修改 CSS)

Chirpy 主题设计时是纯净风格（白/黑模式），默认**不支持**背景图。强行加背景图可能会导致文字看不清，破坏黑夜模式的体验。

如果你**非常想加**，需要修改样式代码 (CSS)。

1. **上传壁纸**：
    - 找一张高清壁纸，命名为 bg.jpg。
    - 上传到 assets/img/ 文件夹。
2. **修改 CSS 文件**：codeCSS
    - 在 GitHub 仓库里，找到 assets -> css -> style.scss (或者 jekyll-theme-chirpy.scss，取决于版本，通常是 assets/css 下的那个 .scss 文件)。
    - 点击编辑，**不要动里面已有的代码**。
    - **在文件的最末尾**，按几下回车，粘贴以下代码：
    
    `/* 强制覆盖背景图 */
    body {
      /* 设置背景图路径 */
      background-image: url('/assets/img/bg.jpg');
      /* 让背景图固定不动，且铺满屏幕 */
      background-attachment: fixed;
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
    }
    
    /* 为了让文字能看清，给主要内容区加一个半透明的白色底板 */
    /* 注意：这可能会影响黑夜模式的显示效果 */
    #main-wrapper {
      background-color: rgba(255, 255, 255, 0.9);
      border-radius: 10px;
      padding: 20px;
      margin-top: 20px;
    }`
    
3. **保存提交**。

**⚠️ 警告**：修改 CSS 属于“魔改”，可能会导致博客在手机上或者黑夜模式下变得很难看。如果改完后发现博客排版崩了，请把刚才加在 style.scss 末尾的代码删掉即可恢复。

### 总结你的工作流

1. **找素材** -> 2. **上传到 assets/img** -> 3. **改代码引用** -> 4. **Commit 触发自动部署**。
