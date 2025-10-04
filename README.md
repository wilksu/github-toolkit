# 通用 Git 仓库子目录拆分工具 (Repo Subdirectory Splitter)

这是一个基于 GitHub Actions 的自动化工具，旨在解决一个常见的需求：将一个大型 Git 仓库中的某个子目录，连同其完整的 Git 提交历史，拆分成一个全新的、独立的仓库。

## ✨ 功能特性

- **一键拆分**：只需提供一个目录的 URL 和新仓库名，即可自动化完成所有操作。
- **保留历史**：完整保留该子目录相关的所有 Git 提交历史，不会丢失任何记录。
- **完全在线**：所有操作都在 GitHub 的服务器上完成，无需在本地安装任何工具或克隆大型仓库。
- **高度灵活**：
  - 支持创建**公开 (Public)** 或 **私有 (Private)** 仓库。
  - 支持**仅拆分单个分支**或**保留所有分支**的模式。
- **安全可靠**：使用个人访问令牌 (PAT) 进行授权，与仓库代码安全隔离。

---

## 🚀 开始使用

### 步骤一：准备个人访问令牌 (PAT)

本工具需要授权来在你的账户下创建新仓库。因此，你需要创建一个拥有相应权限的 PAT。

1.  访问 GitHub 的 [个人访问令牌设置页面](https://github.com/settings/tokens/new)。
2.  **Note**: 给令牌起一个描述性的名字，例如 `repo-splitter-action`。
3.  **Expiration**: 设置一个合适的过期时间。
4.  **Scopes**: **务必勾选 `repo`** 这个权限。这将授予令牌创建和写入仓库的权限。
5.  点击 **Generate token** 并 **立即复制** 生成的令牌字符串。

### 步骤二：在仓库中设置 Secret

将复制的 PAT 安全地存储在运行此 Action 的仓库的 Secrets 中。

1.  进入本仓库的 **Settings** -> **Secrets and variables** -> **Actions**。
2.  点击 **New repository secret**。
3.  **Name**: `ACTION_PAT`
4.  **Secret**: 粘贴你刚才复制的 PAT 令牌。
5.  点击 **Add secret**。

### 步骤三：运行工作流

一切准备就绪，现在可以开始拆分仓库了。

1.  进入本仓库的 **Actions** 标签页。
2.  在左侧的菜单中，点击你想运行的工作流，例如 **"Split Subdirectory From URL (V3)"**。
3.  点击 **Run workflow** 按钮。
4.  在弹出的表单中，填写以下参数：
    - **Source dir url**: 你想拆分的子目录的完整 URL。
      - *示例*: `https://github.com/immortalwrt/luci/tree/master/applications/luci-app-zerotier`
    - **New repo name**: 你希望创建的新仓库的名称。
      - *示例*: `luci-app-zerotier-standalone`
    - **Visibility**: 选择新仓库是 `private` (私有) 还是 `public` (公开)。
    - **Branch behavior**: 选择分支处理模式。
      - `single`: 仅保留 URL 中那个分支的历史，并作为 `main` 分支。
      - `all`: 保留所有分支的历史。
5.  点击绿色的 **Run workflow** 按钮，等待任务完成即可。

---

## 🛠️ 可用工作流

本仓库可能包含多个工具。当前可用的工作流如下：

* **[Split Subdirectory From URL (V3)](./.github/workflows/split_repo_from_url.yml)**
    * 功能最全的子目录拆分工具，推荐使用。

* *（未来你可以在这里添加其他 Action 的介绍）*