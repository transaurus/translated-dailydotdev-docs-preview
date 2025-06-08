---
sidebar_position: 5
description: "Learn how to save, organize, and sync daily.dev bookmarks across devices and share them on GitHub for seamless access and integration."
---

# 书签功能

## 书签的重要性

**daily.dev** 的书签功能可帮助您保存并整理文章供稍后阅读，让您能按自己的节奏管理有价值的内容。

### 书签的优势

1. **稍后阅读**：为无法立即阅读的文章添加书签，方便随时查阅。
2. **整理阅读清单**：通过文件夹或标签按兴趣、偏好或需求分类文章，便于检索。
3. **多设备同步**：书签会同步到您账户关联的所有设备，实现无缝阅读切换。
4. **个性化内容**：构建与您专业兴趣相关的专属阅读清单，提升专注力与职业成长。

## 如何添加书签

- **通过书签按钮**：点击文章上的**书签**按钮。
- **侧边栏工具**：使用[侧边栏工具中的书签图标](https://app.daily.dev/posts/6IVMj7uuS)快速保存。
- **文章讨论页**：在文章讨论页的[操作栏](https://app.daily.dev/posts/yc3ZVzfLY)点击书签按钮。

![daily.dev书签功能示意图](https://daily-now-res.cloudinary.com/image/upload/v1724398568/docs-v2/9ff96218-b88c-4c45-94b6-e087cf2d6810.png)

以上方法确保您在daily.dev获得流畅的书签体验。

## 书签提醒

添加书签后，文章可能会在信息流中显示，提醒您及时阅读。

![书签提醒示意图](https://github.com/user-attachments/assets/30f793c0-a1d2-469f-9f5c-f0249c257676)

## 多设备同步

只需在所有设备上登录同一账户即可同步书签。

## 书签公开模式

公开模式会生成书签的公开RSS订阅链接，便于分享或集成。例如，您可将书签集成到GitHub README中。请参照以下教程进行设置。

## [教程] 在GitHub分享书签

### 将daily.dev书签集成至GitHub

- 在书签版块选择**分享书签**
- 启用公开模式并复制RSS订阅链接
- 在GitHub创建与您账户同名的仓库
- 创建`.github`文件夹，并在其中添加`workflows`子文件夹
- 添加名为`daily.dev-bookmarks.yml`的文件，内容如下：

```yaml
name: daily.dev Bookmarks
on:
  schedule:
    # Runs every hour
    - cron: '0 * * * *'
  workflow_dispatch:

jobs:
  daily-dev-bookmarks:
    name: Update this repo's README with latest bookmarks from daily.dev
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: gautamkrishnar/blog-post-workflow@master
        with:
          comment_tag_name: "daily.dev BOOKMARKS"
          feed_list: "<YOUR BOOKMARKS RSS FEED LINK HERE>"


**Important:** You need to replace the `<YOUR BOOKMARKS RSS FEED LINK HERE>` with your own RSS feed.

- Commit the `daily.dev-bookmarks.yml` file. Your file should look like this:

![Example of daily.dev-bookmarks.yml file setup](https://daily-now-res.cloudinary.com/image/upload/v1644219700/docs/bookmarksGithub6.png)

- Open the `README.md` file in your profile repository (this repository should be named the same as your GitHub account).

![GitHub profile repository README setup](https://daily-now-res.cloudinary.com/image/upload/v1644219700/docs/bookmarksGithub7.png)

- Add these lines at the end of the `README.md` file:

```markdown
<!-- daily.dev BOOKMARKS:START -->
<!-- daily.dev BOOKMARKS:END -->

```

- 提交Readme.md文件
- 检查README文件是否已更新
- 运行工作流`daily-dev-bookmarks`

![启动daily.dev GitHub工作流](https://daily-now-res.cloudinary.com/image/upload/v1644219700/docs/bookmarksGithub9.png)

![更新后的GitHub README显示daily.dev书签](https://daily-now-res.cloudinary.com/image/upload/v1644219700/docs/bookmarksGithub11.png)

GitHub Action默认每小时运行一次。您可通过修改`daily.dev-bookmarks.yml`文件中的cron设置调整频率。

![配置GitHub Action执行计划](https://daily-now-res.cloudinary.com/image/upload/v1644219700/docs/bookmarksGithub12.png)

恭喜！您的daily.dev书签已成功集成至GitHub。