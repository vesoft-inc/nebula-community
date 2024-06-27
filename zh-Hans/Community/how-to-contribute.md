# 如何贡献代码和文档

## 开始之前

### GitHub 或社区提交问题

欢迎为项目贡献任何代码或文档，但是建议先在 [GitHub](https://github.com/vesoft-inc/nebula) 或[社区](https://discuss.nebula-graph.io/)上提交一个问题，和大家共同讨论。

### 签署贡献者许可协议（CLA）

什么是 [CLA](https://www.apache.org/licenses/contributor-agreements.html)？

签署协议链接：[vesoft inc. Contributor License Agreement](https://cla-assistant.io/vesoft-inc/)

单击按钮 **Sign in with GitHub to agree** 签署协议。

如果有任何问题，请发送邮件至`info@vesoft.com`。

## 修改单篇文档

Nebula Graph 文档以 Markdown 语言编写。单击文档标题右侧的铅笔图标即可提交修改建议。

该方法仅适用于修改单篇文档。

## 批量修改或新增文件

该方法适用于贡献代码、批量修改多篇文档或者新增文档。

### Step 1：通过 GitHub fork 仓库

Nebula Graph 项目有很多[仓库](https://github.com/vesoft-inc)，以 [nebula-graph 仓库](https://github.com/vesoft-inc/nebula)为例：

1. 访问 [github.com/vesoft-inc/nebula](https://github.com/vesoft-inc/nebula)。

2. 在右上角单击按钮`Fork`，然后单击用户名，即可 fork 出 nebula-graph 仓库。

### Step 2：将分支克隆到本地

1. 定义本地工作目录。

  ```bash
  # 定义工作目录。
  working_dir=$HOME/Workspace
  ```

2. 将`user`设置为 GitHub 的用户名。

  ```bash
  user={GitHub 用户名}
  ```

3. 克隆代码。

  ```bash
  mkdir -p $working_dir
  cd $working_dir
  git clone https://github.com/$user/nebula-graph.git
  # 或：git clone git@github.com:$user/nebula-graph.git
  cd $working_dir/nebula
  git remote add upstream https://github.com/vesoft-inc/nebula.git
  # 或：git remote add upstream git@github.com:vesoft-inc/nebula.git
  # 由于没有写访问权限，请勿推送至上游主分支。
  git remote set-url --push upstream no_push
  # 确认远程分支有效。
  # 正确的格式为：
  # origin    git@github.com:$(user)/nebula-graph.git (fetch)
  # origin    git@github.com:$(user)/nebula-graph.git (push)
  # upstream  https://github.com/vesoft-inc/nebula (fetch)
  # upstream  no_push (push)
  git remote -v
  ```

4. （可选）定义 pre-commit hook。

  请将 Nebula Graph 的 pre-commit hook 连接到`.git`目录。

  hook 将检查 commit，包括格式、构建、文档生成等。

  ```bash
  cd $working_dir/nebula-graph/.git/hooks
  ln -s $working_dir/nebula-graph/.linters/cpp/hooks/pre-commit.sh .
  ```

  pre-commit hook 有时候可能无法正常执行，用户必须手动执行。

  ```bash
  cd $working_dir/nebula-graph/.git/hooks
  chmod +x pre-commit
  ```

### Step 3：分支

1. 更新本地主分支。

  ```bash
  cd $working_dir/nebula
  git fetch upstream
  git checkout master
  git rebase upstream/master
  ```

2. 从主分支创建并切换分支：

  ```bash
  git checkout -b myfeature
  ```

  !!! Note

        由于一个 PR 通常包含多个 commits，最终合入 upstream/master 分支时，我们会将这些 commits 挤压（squash）成一个 commit 进行合并。因此强烈建议创建一个独立的分支进行更改，这样在合入时才容易被挤压。合并后，这个分支可以被丢弃。如果未创建单独的分支，而是直接将 commits 提交至 origin/master，在合入时，可能会出现问题。
        若未创建单独的分支（或是 origin/master 合并了其他的分支等），导致 origin/master 和 upstream/master 不一致时，用户可以使用 hard reset 强制两者进行一致。例如：

        ```bash
        git fetch upstream
        git checkout master
        git reset --hard upstream/master
        git push --force origin master
        ```

### Step 4：开发

- 代码风格

  **Nebula Graph** 采用`cpplint`来确保代码符合 Google 的代码风格指南。检查器将在提交代码之前执行。

- 单元测试要求

  请为新功能或 Bug 修复添加单元测试。

- 构建代码时开启单元测试

  详情请参见[使用源码安装 Nebula Graph](https://github.com/vesoft-inc/nebula-docs-cn/blob/245716cff6822d9c7324facb756b249a3cdb8441/docs-2.0/4.deployment-and-installation/2.compile-and-install-nebula-graph/1.install-nebula-graph-by-compiling-the-source-code.md)。

  !!! Note

        请确保已设置`-DENABLE_TESTING = ON`启用构建单元测试。

- 运行所有单元测试

  在`nebula`根目录执行如下命令：

  ```bash
  cd nebula/build
  ctest -j$(nproc)
  ```

### Step 5：保持分支同步

```bash
# 当处于 myfeature 分支时。
git fetch upstream
git rebase upstream/master
```

在其他贡献者将 PR 合并到基础分支之后，用户需要更新 head 分支。

### Step 6：Commit

提交代码更改：

```bash
git commit -a
```

用户可以使用命令`--amend`重新编辑之前的代码。

### Step 7：Push

需要审核或离线备份代码时，可以将本地仓库创建的分支 push 到 GitHub 的远程仓库。

```bash
git push origin myfeature
```

### Step 8：创建 pull request

1. 访问 fork 出的仓库`https://github.com/$user/nebula-graph` （替换此处的用户名`$user`)。

2. 单击`myfeature`分支旁的按钮`Compare & pull request`。

### Step 9：代码审查

pull request 创建后，至少需要两人审查。审查人员将进行彻底的代码审查，以确保变更满足存储库的贡献准则和其他质量标准。

## 添加测试用例

添加测试用例的方法参见 [How to add test cases](https://github.com/vesoft-inc/nebula/blob/master/tests/README.md#how-to-add-test-case)。

## 捐赠项目

### Step 1：确认项目捐赠

通过邮件、微信、Slack 等方式联络 Nebula Graph 官方人员，确认捐赠项目一事。项目将被捐赠至 [Nebula Contrib](https://github.com/nebula-contrib) 组织下。

* 邮件地址：info@vesoft.com

* 微信：NebulaGraphbot

* Slack：[Join Slack](https://join.slack.com/t/nebulagraph/shared_invite/zt-7ybejuqa-NCZBroh~PCh66d9kOQj45g)

### Step 2：获取项目接收人信息

由 Nebula Graph 官方人员给出 Nebula Contrib 的项目接收者 ID。

### Step 3：捐赠项目

由您将项目转移至本次捐赠的项目接受人，并由项目接收者将该项目转移至 [Nebula Contrib](https://github.com/nebula-contrib) 组织下。捐赠后，您将以 Maintain 角色继续主导社区项目的发展。

GitHub 上转移仓库的操作，请参见 [Transferring a repository owned by your user account](https://docs.github.com/en/enterprise-server@3.0/github/administering-a-repository/managing-repository-settings/transferring-a-repository#transferring-a-repository-owned-by-your-user-account)。 
