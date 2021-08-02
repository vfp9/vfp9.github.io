---
layout: page
permalink: /admin/
---

## 管理员须知

### 设置

- 克隆GitHub Pages仓库，地址是<a href="https://github.com/VFPX/VFPX.github.io" target="_blank">https://github.com/VFPX/VFPX.github.io</a>，这样你就可以编辑VFPX的文档。

- 告诉Git关于GitHub仓库的信息。

        git remote add origin https://github.com/VFPX/VFPX.github.io.git

### 在VFPX下添加一个项目

- 进入<a href="https://github.com/VFPX" target="_blank">https://github.com/VFPX</a>。

- 点击绿色的 "新建 "按钮。

- 输入版本库的名称和描述（如果是以前的CodePlex项目，你可以从CodePlex的描述中复制和粘贴）。

- 打开 "用README初始化此版本库"。

- 点击创建版本库。

- 点击该仓库的设置图标，然后选择合作者和团队。

- 输入项目经理的GitHub用户名，点击添加合作者。

- 如果这是前六个项目之一（只有六个项目可以被钉在上面），在VFPX页面，点击 "自定义被钉的仓库"，在出现的对话框中，打开新的仓库，关闭另一个仓库。然后，在钉住的列表中，拖动新的版本库，使其按字母顺序位于正确的位置。

- 编辑 _data 文件夹中的 projects.json，为新项目添加一个条目（如果是从 CodePlex 迁移过来的项目，编辑 URL 设置为新仓库），然后提交并推送。

- 创建一个关于项目的新帖子（见创建帖子部分）。

### 添加一个独立的项目

- 编辑_data文件夹中的projects.json，为新项目添加一个条目，然后提交并推送。

- 创建一个关于这个项目的新帖子（见创建帖子部分）。

### 创建一个帖子

- 在你的GitHub Pages仓库的_posts文件夹下创建一个新的MD文件。文件名应该是 YYYY-MM-DD-title.md，其中 YYYY-MM-DD 是帖子的日期，title 应该是一个简短的标题，用破折号代替空格。

- 内容应该以这个标题开始。

        ---
        layout: post
        title:  "The title of the post"
        date:   YYYY-MM-DD HH:MM:SS -0500
        categories: vfpx update
        ---

    使用适当的GMT偏移量来代替-0500。你可以使用其他的关键词作为类别。

- 在标题之后，放入任何你想要的内容。

- 编辑完文件后，在 Notepad++ 中打开，从编码菜单中选择转换为 UTF-8（在旧版本的 Notepad++ 中选择转换为无 BOM 的 UTF-8）；不这样做，页面就不会在 GitHub 上正确显示。

- 将文件添加到仓库，提交，然后推送。
