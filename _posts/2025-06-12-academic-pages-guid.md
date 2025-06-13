---
title: 'Academic Pages 简明双语指南'
date: 2025-06-12
permalink: /posts/2025/06/academic-pages-guide/
tags:
  - handbook
  - guide
  - Github
---

{% include toc %}

Quick Guide for Academic Pages (Chinese-English Bilingual)

本页面为中英双语版。This page provides both Chinese and English instructions.

PS: 有两种常用的 Markdown 静态网站生成工具：Jekyll 和 Hugo。Hugo 与 R 语言的 blogdown 包结合紧密，适合用 R 写网站。但是我对其机器不熟悉，而且大部分设置我也不知道在哪儿找。因此放弃了。而Jekyll的大量设置非常符合我的使用习惯，我可以很好的进行调整和掌控。并且，我也更喜欢 Jekyll 的主题风格。因此使用了基于Jekyll的`Academic Pages template`。此外，还有一个最近流行的新方法：Notion + Github 自动化流。但是我发现，页面相对简单，逐渐不满足我的需求，因此转向了此项目。

## 1. 项目简介 | About this Project

This site uses the [Academic Pages template](https://github.com/academicpages/academicpages.github.io) and is hosted on [GitHub Pages](https://pages.github.com). You can quickly have your own academic website by forking this template, editing a few files, and deploying for free—no coding skills required!

本网站基于 [Academic Pages 模板](https://github.com/academicpages/academicpages.github.io)，托管在 [GitHub Pages](https://pages.github.com) 上。只需 Fork 模板，修改配置文件，就可以免费拥有自己的学术主页，无需复杂编程。

## 2. 快速部署到 GitHub Pages | Deploy to GitHub Pages in Minutes

Deploy:

1. **Create a GitHub account** and verify your email.  
2. **Fork** [this template](https://github.com/academicpages/academicpages.github.io) (“Use this template” > “Create a new repository”).  
3. **Name your repository** as `yourname.github.io`.  
4. **Edit content:** update markdown (.md) files and `_config.yml`.  
5. **Push changes:** edit online or locally, push to GitHub, and it will deploy automatically.  
6. **Visit** `https://yourname.github.io` to see your site!

简单部署：

1. **注册 GitHub 账号** 并验证邮箱。  
2. **Fork** [本模板](https://github.com/academicpages/academicpages.github.io)（点击 "Use this template" > "Create a new repository"）。  
3. **仓库命名为** `yourname.github.io`。  
4. **编辑内容：** 更新 markdown 文件和 `_config.yml`。  
5. **推送修改：** 在线编辑或本地推送，GitHub 会自动部署。  
6. **访问** `https://yourname.github.io` 查看你的站点。


## 3. 修改与维护 | Editing and Maintenance

You can manage your site both online and offline.  
- **Edit online:**  
  - On GitHub, open any file, click the pencil icon to edit, then “Commit changes” to save.
  - You can upload or create new files using the “Add file” button.
  - To delete a file, click the trashcan icon next to it.
- **Edit locally (recommended for batch or advanced edits):**  
  1. Clone your repository:  
     ```bash
     git clone https://github.com/yourname/yourname.github.io.git
     ```
  2. Make changes on your computer (using any text editor).
  3. Save changes, then run:  
     ```bash
     git add .
     git commit -m "Describe your update"
     git push
     ```
  4. Your site will update automatically.
- **Rollback changes:**  
  - If something goes wrong, you can use GitHub’s “History” to revert a file, or use `git revert` locally.
- **Version control:**  
  - Every commit is saved; you can always restore previous versions.
- **Auto-deployment:**  
  - Any change you push will trigger automatic deployment—no extra steps needed.

你可以通过在线和本地两种方式维护网站内容。  
- **在线编辑：**  
  - 在 GitHub 网站中打开任意文件，点击铅笔图标编辑，编辑后点击“Commit changes”保存。  
  - 可通过“Add file”上传或创建新文件。  
  - 删除文件可点右侧垃圾桶图标。
- **本地编辑（适合批量或高级操作）：**  
  1. 克隆仓库到本地：  
     ```bash
     git clone https://github.com/yourname/yourname.github.io.git
     ```
  2. 用文本编辑器修改内容。
  3. 保存后，运行：  
     ```bash
     git add .
     git commit -m "描述你的更新"
     git push
     ```
  4. 推送后网站自动更新，无需手动部署。
- **回滚修改：**  
  - 如遇问题，可在 GitHub 的“History”页面还原文件，也可以本地用 `git revert` 恢复。
- **版本控制：**  
  - 每次提交都会被记录，可随时恢复历史版本。
- **自动部署：**  
  - 每次推送或修改，网站都会自动部署并更新，无需其他操作。

## 4. 网站结构与内容 | Site Structure & Content

Content:
- **Content** is stored as markdown (.md) files in folders like `_publications`, `_talks`, etc.  
- **Site-wide config** is in `_config.yml`.  
- **Navigation bar** can be set in `_data/navigation.yml`.  
- Add files (PDFs etc.) in `files/` folder.

内容:
- **内容**保存在如 `_publications`、`_talks` 等文件夹下的 markdown 文件。  
- **网站配置**在根目录下 `_config.yml` 文件。  
- **导航菜单**在 `_data/navigation.yml` 文件中设置。  
- 可将 PDF 等文件放入 `files/` 文件夹。

## 5. 内容与元数据 | Create Content & Metadata

Each publication, talk, or post is a separate markdown file, with structured metadata (YAML) at the top. This metadata is used to generate pages and lists automatically.

每篇论文、报告、博文等内容都是一个独立的 markdown 文件，文件顶部有结构化的 YAML 元数据。这些元数据会被自动解析，用于生成网页和内容列表。

## 6. Markdown 文件生成工具 | Markdown Generator

The template provides Jupyter notebooks that can convert CSV files into markdown files with the correct format. This is useful if you have many publications or talks recorded in spreadsheets.  
[See the Markdown Generator here.](https://github.com/academicpages/academicpages.github.io/tree/master/markdown_generator)

模板自带 Jupyter Notebook 工具，可以把 CSV 数据批量转换为格式正确的 markdown 文件。如果你有大量的论文或报告信息存在表格中，非常适合使用。  
[Markdown 生成器入口](https://github.com/academicpages/academicpages.github.io/tree/master/markdown_generator)

## 7. 更多帮助 | More Help

- [Configuration guide 配置教程](https://academicpages.github.io/markdown/)  
- [Wiki & FAQ 常见问题 Wiki](https://github.com/academicpages/academicpages.github.io/wiki)  
- [Ask questions 提问 & 交流区](https://github.com/academicpages/academicpages.github.io/discussions)
