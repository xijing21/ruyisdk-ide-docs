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
    - 在 ruyisdk镜像站 和 github仓库release 提供jar或者zip包

## 开发必备

- 开发启动四件事: **添加许可证**、**DCO**、代码规范、自动化构建
- 相关的代码仓库PR，需要有**两名**以上的员工同意合入 (常见回复：LGTM（Looks Good To Me），即同意合入）
- **开源社区 Commits & Git 使用必读**：

  - https://www.conventionalcommits.org
  - https://git-scm.com/docs/git-interpret-trailers
  - Commits 统一使用英文
- PR（pull request）：

  - 一个pr尽量一个commit；多个commit请合并（ 搜索 git rebase -i 和 squash 关键字了解学习）；
  - 一个pr尽量只做一件事，方便 reviewer 快速审核，避免很多目的的修改掺和一起，增加代码审核难度；
  - pr标题建议英语，简明且尽量说明为什么做了什么，描述详细说明下修改详细信息（如背景原因，主要修改思路/内容，修改后的运行效果截图等），方便 reviewer 理解并快速审核；

  > 语言要求：commit log 强制要求英语；pr标题建议使用英语；pr描述和评论等不做限制；issue不做语言限制；
  >
