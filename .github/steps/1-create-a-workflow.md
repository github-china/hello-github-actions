## Step 1: 创建工作流(Workflow)文件

_欢迎来到 “Hello GitHub Actions”课程! :wave:_

**什么是 _GitHub Actions_?**: GitHub Actions 是一种高度灵活的自动化方式，覆盖软件开发的方方面面。包括自动化测试、CI/CD持续部署、自动化代码审查、管理问题和拉取请求，等等。 最棒的是，这些工作流配置以代码的形式保存在您的git仓库中，可以很方便的在团队之间共享和重用。
- 功能介绍页面：[GitHub Actions](https://github.com/features/actions)
- 用户文档：[GitHub Actions](https://docs.github.com/actions)

**什么是 _工作流(workflow)_?**: 工作流是一可配置的自动化过程，可以运行一个或多个 job（任务）。它们写在仓库中 `.github/workflows` 目录下的特定文件里，并根据设定的事件触发。本练习中，我们会使用 `pull_request` 事件。

- 想了解更多关于 workflow、job 和事件的内容，请看 “[Understanding GitHub Actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)”
- 如果你想先看看 `pull_request` 事件的详细信息，请参考 “[pull_request](https://docs.github.com/en/developers/webhooks-and-events/webhooks/webhook-events-and-payloads#pull_request)”

为了帮你起步，系统已经在你的仓库里运行了一个 Actions 工作流，并为你创建了一个用于操作的分支，名为 `welcome-workflow`。

### :keyboard: 实操环节：创建一个工作流文件

1. 打开一个新的浏览器标签页，方便一边操作一边阅读本教程。
2. 先创建一个 Pull Request，这个 PR 将包含你在本阶段中所有的修改。操作如下:

   - 点击 **Pull Requests** tab
   - 点击 **New pull request**
   - 将 `base` 设为 `main`，`compare` 设为 `welcome-workflow`
   - 点击 **Create pull request**，再点击一次确认创建

3. 回到 **Code** 页面。
4. 在分支下拉菜单中，切换到 **welcome-workflow** 分支。
5. 进入 `.github/workflows/` 目录，点击 **Add file** → **Create new file**。
6. 在 “Name your file” 输入框中填写：`welcome.yml`
7. 将以下内容添加到 `welcome.yml` 文件中：

   ```yaml copy
   name: Post welcome comment
   on:
     pull_request:
       types: [opened]
   permissions:
     pull-requests: write
   ```

8. 点击 **Commit changes** 进行提交。
9. 输入提交信息，选择 **Commit directly to the welcome-workflow branch**，然后点击 **Commit changes**。
10. 等待大约20秒，然后刷新当前课程页面。[GitHub Actions](https://docs.github.com/en/actions) 会自动检测并进入下一步。