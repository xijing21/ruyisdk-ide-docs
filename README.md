# ruyisdk-ide-docs

- [项目目标](./intro/vision.md)
- [项目组成总览](./intro/overview.md)
- [基础研发模块](./other/module.md)

## IDE

### Common

- [面向RISC-V开发的主要开发需求总览](ide/overview.md)
- [IDE插件需求](ide/requires.md)
- RuyiSDK包管理器介绍

  - 仓库：https://github.com/ruyisdk/ruyi
  - 技术说明：https://github.com/ruyisdk/ruyi/blob/main/docs
  - 接口：https://github.com/ruyisdk/ruyi/blob/main/docs/programmatic-usage.md
  - 使用文档：https://ruyisdk.org/docs/category/ruyi-%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8
  - 补充说明：[ruyi 包管理器本地文件](ide/ruyi.md)

### VSCode 插件

- 资源简介：

  - 仓库：https://github.com/ruyisdk/ruyisdk-vscode-extension
  - 代码规范要求：待补充
- 设计文档：[pdf](./ide/vscode/RISC-V%20VSCode%20插件设计书（修改版）.pdf)
- 发布方式：
  - 上架vscode 插件市场：https://marketplace.visualstudio.com
  - 在 ruyisdk镜像站 和 github仓库release 提供扩展包

### Eclipse 插件

- 资源简介：
  基于eclipse embeded cdt 定制IDE（ruyisdk ide）包括两个部分：一个是打包工程和一个插件仓库：
  - 打包工程仓库：https://github.com/ruyisdk/ruyisdk-eclipse-packages/
  - 插件仓库：https://github.com/ruyisdk/ruyisdk-eclipse-plugins/ 

  - 代码规范：https://github.com/ruyisdk/ruyisdk-eclipse-plugins/blob/main/docs/developer/CONTRIBUTING.md
- 设计文档：

  - [eclipse-ruyi-plugins](./ide/eclipse/eclipse-ruyi.md) 功能构想

- 发布方式：
  - 方式一：将插件打包到IDE中，提供一体化的IDE工具。（适合新用户初装）
  - 方式二：单独提供插件安装和更新（适合插件单独安装/更新场景）
    - 在 Eclipse marketplace 发布（推荐）
    - 在 ruyisdk 镜像站 和 github仓库release 提供jar或者zip包

## 开发必备

- 开发启动四件事: **添加许可证**、**DCO**、代码规范、自动化构建
- 相关的代码仓库PR，需要有**两名**以上的员工同意合入 (常见回复：LGTM（Looks Good To Me），即同意合入）
- **开源社区 Commits & Git 使用必读**：

  - https://www.conventionalcommits.org
  - https://git-scm.com/docs/git-interpret-trailers
  - **Commits 统一使用英文**

- PR（pull request）：
  - 创建PR：PR 标题强烈建议英语，简明且尽量说明为什么做了什么，描述详细说明下修改详细信息（不限于如背景原因，主要修改思路/内容，修改后的运行效果截图等），方便 reviewer 理解并快速审核；
  - PR颗粒度：合理规划 PR 颗粒度，以方便 maintainer/reviewer 审核便捷为目的，建议“一个PR只做一件事”，尽量避免多个目的/事项混在一起增加沟通成本和代码审核难度。
  - PR commit数量：开发前与仓库 maintainer/reviewer 沟通达成一致（是否要求多个commit合并）；

- 语言要求：**commit log 强制要求英语**；PR标题**强烈建议**使用英语；其他鼓励使用英语但不严格限制（如PR描述、评论；issue标题、描述、评论等）；
  > “Commit 信息强制英文是为了保证代码历史对全球开发者永久可读；PR 标题建议英文是为了方便维护者快速管理。我们理解语言的多样性，因此 PR 和 Issue 的讨论不限制语言，以鼓励更深入的交流。”