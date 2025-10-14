## Step 3: 为工作流添加一个 step

_你已经成功添加了一个 job，干得很棒！:dancer:_

接下来我们继续完善它, 在 job 中加入一个 step。

**什么是 *step（步骤）*？** 在 workflow 中，一个 job 由多个 step 组成。step 会**从上到下按顺序执行**，并且**每一步必须成功，下一步才会继续运行**。

每个 step 要么运行一段 shell 脚本，要么调用一个可复用的 action（小写的 “action” 指的是一段可复用的代码逻辑）。关于自定义 actions，可以参考文档 “[Finding and customizing actions](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions)”，但这一步我们不需要 action，而是直接用 shell 脚本。

我们现在要更新 workflow，让它自动在新的 pull request 下发表评论。这里会用到：

* [Bash](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) 脚本
* [GitHub CLI](https://cli.github.com/)

### :keyboard: 实操环节: 添加一个 step 到工作流中

1. 仍在 `welcome-workflow` 分支下，打开你的 `welcome.yml` 文件。
2. 将文件内容更新为以下内容：

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
       steps:
         - run: gh pr comment $PR_URL --body "Welcome to the repository!"
           env:
             GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
             PR_URL: ${{ github.event.pull_request.html_url }}
   ```

   **说明：** 我们添加的这个步骤使用 GitHub CLI (`gh`) 在 pull request 创建时发布一条评论。
   - `GITHUB_TOKEN`：通过 `secrets.GITHUB_TOKEN` 提供，用来授权 CLI 发表评论。这是 GitHub 在运行 workflow 时自动生成的token。详情可参考 “[Automatic token authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)”。
   - `PR_URL`：通过 `${{ github.event.pull_request.html_url }}` 获取当前 pull request 的地址，供脚本使用。

3. 在右上角点击 **Commit changes**。
4. 输入提交信息并将修改直接提交到当前分支。
5. 等待大约20秒，然后刷新当前课程页面。[GitHub Actions](https://docs.github.com/en/actions) 会自动检测并进入下一步。
