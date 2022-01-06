# How to Contribute

## Before you get started

### Commit an issue on the github or forum

You are welcome to contribute any code or files to the project. But firstly we suggest you raise an issue on the [github](https://github.com/vesoft-inc/nebula-graph) or the [forum](https://discuss.nebula-graph.io/) to start a discussion with the community. Check through the topic for Github.

### Sign the Contributor License Agreement (CLA)

What is [CLA](https://www.apache.org/licenses/contributor-agreements.html)?

Here is the [vesoft inc. Contributor License Agreement](https://cla-assistant.io/vesoft-inc/).

Click the **Sign in with GitHub to agree** button to sign the CLA.

If you have any questions, send an email to `info@vesoft.com`.

## Modify a single document

This manual is written in the Markdown language. Click the `pencil` icon on the right of the document title to commit the modification.

This method applies to modify a single document only.

## Batch modify or add files

This method applies to contribute codes, modify multiple documents in batches, or add new documents.

## Step 1: Fork in the github.com

The Nebula Graph project has many [repositories](https://github.com/vesoft-inc). Take [the nebula-graph repository](https://github.com/vesoft-inc/nebula) for example:

1. Visit [https://github.com/vesoft-inc/nebula](https://github.com/vesoft-inc/nebula).

2. Click the `Fork` button to establish an online fork.

## Step 2: Clone Fork to Local Storage

1. Define a local working directory.

  ```bash
  # Define the working directory.
  working_dir=$HOME/Workspace
  ```

2. Set `user` to match the Github profile name.

  ```bash
  user={the Github profile name}
  ```

3. Create your clone.

  ```bash
  mkdir -p $working_dir
  cd $working_dir
  git clone https://github.com/$user/nebula-graph.git
  # or: git clone git@github.com:$user/nebula-graph.git

  cd $working_dir/nebula
  git remote add upstream https://github.com/vesoft-inc/nebula.git
  # or: git remote add upstream git@github.com:vesoft-inc/nebula.git

  # Never push to upstream master since you do not have write access.
  git remote set-url --push upstream no_push

  # Confirm that the remote branch is valid.
  # The correct format is:
  # origin    git@github.com:$(user)/nebula-graph.git (fetch)
  # origin    git@github.com:$(user)/nebula-graph.git (push)
  # upstream  https://github.com/vesoft-inc/nebula (fetch)
  # upstream  no_push (push)
  git remote -v
  ```

4. (Optional) Define a pre-commit hook.

  Please link the Nebula Graph pre-commit hook into the `.git` directory.

  This hook checks the commits for formatting, building, doc generation, etc.

  ```bash
  cd $working_dir/nebula-graph/.git/hooks
  ln -s $working_dir/nebula-graph/.linters/cpp/hooks/pre-commit.sh .
  ```

  Sometimes, the pre-commit hook cannot be executed. You have to execute it manually.

  ```bash
  cd $working_dir/nebula-graph/.git/hooks
  chmod +x pre-commit
  ```

## Step 3: Branch

1. Get your local master up to date.

  ```bash
  cd $working_dir/nebula
  git fetch upstream
  git checkout master
  git rebase upstream/master
  ```

2. Checkout a new branch from master.

  ```bash
  git checkout -b myfeature
  ```

  !!! note

        Because the PR often consists of several commits, which might be squashed while being merged into upstream. We strongly suggest you to open a separate topic branch to make your changes on. After merged, this topic branch can be just abandoned, thus you could synchronize your master branch with upstream easily with a rebase like above. Otherwise, if you commit your changes directly into master, you need to use a hard reset on the master branch. For example:

        ```bash
        git fetch upstream
        git checkout master
        git reset --hard upstream/master
        git push --force origin master
        ```

## Step 4: Develop

- Code style

  **Nebula Graph** adopts `cpplint` to make sure that the project conforms to Google's coding style guides. The checker will be implemented before the code is committed.

- Unit tests requirements

  Please add unit tests for the new features or bug fixes.

- Build your code with unit tests enabled

  For more information, see [Install Nebula Graph by compiling the source code](https://github.com/vesoft-inc/nebula-docs/blob/master/docs-2.0/4.deployment-and-installation/2.compile-and-install-nebula-graph/1.install-nebula-graph-by-compiling-the-source-code.md).

  !!! Note

        Make sure you have enabled the building of unit tests by setting `-DENABLE_TESTING=ON`.

- Run tests

  In the root directory of `nebula`, run the following command:

  ```bash
  cd nebula/build
  ctest -j$(nproc)
  ```

## Step 5: Bring Your Branch Update to Date

```bash
# While on your myfeature branch.
git fetch upstream
git rebase upstream/master
```

Users need to bring the head branch up to date after other contributors merge PR to the base branch.

## Step 6: Commit

Commit your changes.

```bash
git commit -a
```

Users can use the command `--amend` to re-edit the previous code.

## Step 7: Push

When ready to review or just to establish an offsite backup, push your branch to your fork on `github.com`:

```bash
git push origin myfeature
```

## Step 8: Create a Pull Request

1. Visit your fork at `https://github.com/$user/nebula-graph` (replace `$user` here).

2. Click the `Compare & pull request` button next to your `myfeature` branch.

## Step 9: Get a Code Review

Once your pull request has been created, it will be assigned to at least two reviewers. Those reviewers will do a thorough code review to make sure that the changes meet the repository's contributing guidelines and other quality standards.

## Add test cases

For detailed methods, see [How to add test cases](https://github.com/vesoft-inc/nebula/blob/master/tests/README.md#how-to-add-test-case).

## Donation

### Step 1: Confirm the project donation

Contact the official Nebula Graph staff via email, WeChat, Slack, etc. to confirm the donation project. The project will be donated to the Nebula Contrib organization.

Email address: info@vesoft.com

WeChat: NebulaGraphbot

Slack: [Join Slack](https://join.slack.com/t/nebulagraph/shared_invite/zt-7ybejuqa-NCZBroh~PCh66d9kOQj45g)

### Step 2: Get the information of the project recipient

The Nebula Graph official staff will give the recipient ID of the Nebula Contrib project.

### Step 3: Donate a project

The user transfers the project to the recipient of this donation, and the recipient transfers the project to the Nebula Contrib organization. After the donation, the user will continue to lead the development of community projects as a Maintainer.

For operations of transferring a repository on GitHub, see [Transferring a repository owned by your user account](https://docs.github.com/en/enterprise-server@3.0/github/administering-a-repository/managing-repository-settings/transferring-a-repository#transferring-a-repository-owned-by-your-user-account).
