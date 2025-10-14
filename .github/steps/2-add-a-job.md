## Step 2: 为你的工作流添加一个 job

_干得漂亮! :tada: 你已经创建了一个 Workflow 文件！_

我们先来看看 `welcome-workflow` 分支里 `welcome.yml` 文件中的内容分别代表什么：

* `name: Post welcome comment`
  声明工作流名字。它会显示在仓库的 Actions 页面中。
* `on: pull_request: types: [opened]`
  定义触发条件。表示只要有人在这个仓库里新建一个 pull request，这个工作流程就会被触发。
* `permissions`
  用来设置该工作流在仓库里的操作权限。
* `pull-requests: write`
  授予此工作流 pull request 的写权限，这用于之后自动发表评论。


接下来我们需要告诉该流程要运行哪些 job。

**什么是 _job_?**: job 可以翻译为 "任务"或“作业”。一个 job 可以理解为在同一台 runner（服务器）上执行的一组步骤。

* 一个工作流可以包含多个 job（任务）
* 每个 job 又由若干个按顺序执行的步骤（step）组成
* 步骤之间是互相关联的
  你稍后会继续往这个 workflow 里添加步骤。想深入了解 job，可以参考文档 “[Jobs](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#jobs)”。

这一节里，我们会添加一个名为 `build` 的 job，并指定它运行在 `ubuntu-latest` 这个 runner 上 —— 这是速度最快、成本最低的选项。如果你想知道为什么选它，可以看看这篇文章中对 `runs-on: ubuntu-latest` 的解释：“[Understanding the workflow file](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#understanding-the-workflow-file)”。

### :keyboard: 实操环节: 为你的流程添加一个 job

1. 确认自己处于 `welcome-workflow` 分支，然后打开 `.github/workflows/welcome.yml` 文件。
2. 修改文件内容为以下内容：

   ```yaml copy
   name: Post welcome comment
   on:
     pull_request:
       types: [opened]
   permissions:
     pull-requests: write
   jobs:
     build:
       name: Post welcome comment
       runs-on: ubuntu-latest
   ```
3. 在编辑器右上角点击 **Commit changes**。
4. 输入提交信息，并直接提交到 `welcome-workflow` 分支。
5. 等待大约20秒，然后刷新当前课程页面。[GitHub Actions](https://docs.github.com/en/actions) 会自动检测并进入下一步。