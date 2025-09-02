# Ruyi包管理器插件-Eclipse IDE Plugins

> 文档为功能的初步的规划，仅供内部交流使用。后续开发实现会有调整（文档未必能及时更新），实际以代码为准。

## 启动和关闭

### RuyiSDK IDE（定制化eclipse ide）启动之后，按照如下顺序安装和更新ruyi：

1. 在ruyisdk ide启动时，自动检查是否安装ruyi，并获取本地ruyi版本；

   - 是否按照：设定的ruyi安装路径下是否有ruyi文件（默认的ruyi安装路径初始值为XDG规范标准目录）
   - 本地ruyi版本：执行 `ruyi -V` 获取版本返回值
2. 获取网上ruyi最新版本：

   - 检查方式：搜索 https://mirror.iscas.ac.cn/ruyisdk/ruyi/releases/ 获取所有的子目录名，也就是版本号
   - 获取最大版本号latestversion（版本格式：A.XX.B）：版本大小对比规则：A最大则是最大。A相等 XX 最大则是最大；A和XX都相等，B最大则版本最大；
3. 判断：本地ruyi 返回的版本 == 网上ruyi 最新版本，则跳出结束。否则继续执行第4步
4. 获取当前的设备架构信息，从而定义ruyi文件后缀 suffix：

   1. x86_64 :  suffix=amd64
   2. arm：suffix=arm64
   3. riscv：suffix=riscv64
5. 下载ruyi并操作：

   1. 如果存在ruyi文件，重命名 `ruyi` 为 `ruyi.日期`
   2. 按照如下下载最新版本：`https://mirror.iscas.ac.cn/ruyisdk/ruyi/releases/<latestversion>/ruyi.<suffix>` 到 /usr/local/bin 目录下，并存储为ruyi这个文件名
   3. 修改权限：赋予可执行权限（如 sudo chmod +x ruyi）
   4. 自调用，正常到第步跳出。
6. 执行ruyi安装后的常见操作：

   1. 是否在ide启动时自动检测ruyi环境（安装和本地版本）
   2. 遥测功能开启提醒：询问用户是否同意开启遥测功能。
      - 文字：为了帮助改进产品，我们将开启遥测功能，遥测将收集您的系统信息和操作，比如执行了哪些ruyi命令，按照了哪些包等，不会收集与您的身份有关的任何信息。而且信息将在本地匿名化后上传到服务器。主要用于统计ruyi 命令使用情况，安装的软件包的情况。详见[隐私政策](https://ruyisdk.org/docs/legal/privacyPolicy)
        感谢您的支持，如果您反对数据的上传，您可以点击“拒绝”按钮，数据将不会被收集。
        遥测状态label：用于显示当前的遥测状态，显示 执行 `ruyi telemetry status` 的结果
        按钮：“同意” 、“拒绝”
        点击“同意”按钮，执行 `ruyi telemetry consent`，并更新遥测状态label的显示；
        点击“拒绝”按钮，执行 `ruyi telemetry optout`，并更新遥测状态label的显示；
   3. 执行 `ruyi update ` 更新软件索引
      - 如果执行成功，则提示用户：更新成功；
      - 如果执行失败，则判断是否是网络不通，若是则提醒用户切换到备用软件源：提供按钮【切换软件源】
      - 按钮【切换软件源】执行： `ruyi config set repo.remote "https://mirror.iscas.ac.cn/git/ruyisdk/packages-index.git " `
   4. 加载显示“新闻窗口”，展示产品新闻。具体功能详见“新闻展示”章节的需求描述。新闻展示除了开机自动加载，还需要支持菜单栏命令查看方式。
   5. 自扩展更多操作

### 退出 ruyisdk ide时：

1. 执行：`ruyi telemetry upload`上传遥测数据；

---

java实现:

1. 初始检测：
   1.1 是否安装ruyi：执行ruyi -V看是否有返回值；或者在path路径下搜索遍历ruyi；
   1.2 本地执行 `ruyi -V`版本信息
   1.3 网上软件源中最新ruyi版本信息：从 Constants.NetAddress.MIRROR_RUYI_RELEASES 的路径下，遍历所有目录名，版本为A.B，A最大的为当前最高版本，A相同的B最大为最高版本；

IDE启动时，检验系统是否安装ruyi，如果没有安装ruyi：弹出dialog窗口：提示用户开始安装ruyi，默认安装路径为"~/.local/bin/"，并给与修改路径的选项，可供用户修改默认安装路径。
用户确定后，将上面的默认安装路径赋值到Constants类的Ruyi 类的 DEFAULT_PATH ；用于保存用户设置；

执行安装：

1. 从 Constants.Ruyi.DEFAULT_PATH 获取路径ruyi的安装路径。默认是"~/.local/bin/"
2. 从 Constants.NetAddress.MIRROR_RUYI_RELEASES 的路径下获取最新的安装安装版本（0.XX），下载与系统架构匹配的安装程序到1中的路径下。如ruyi.amd64;
3. 修改ruyi.amd64为ruyi；
4. 为ruyi赋予可执行权限；
5. 执行 ruyi -V检验安装是否成功。
   ```
      String lastestVersion = "0.32.0";
      String archSuffix = SystemInfo.detectArchitecture().getSuffix();  //"amd64";
      String lastestFileName = "ruyi."+archSuffix;

      //ruyiDownloadUrl = "https://mirror.iscas.ac.cn/ruyisdk/ruyi/releases/0.32.0/ruyi.amd64"
      String ruyiDownloadUrl = Constants.NetAddress.MIRROR_RUYI_RELEASES + "/"+lastestVersion+"/"+lastestFileName;
      String ruyiInstallPath = Paths.get(installPath, lastestFileName).toString();
   ```

---

## 新闻展示

设置开机时是否自动展示新闻选项，默认为是；用户可以修改为否（在启动时不默认展示新闻）
在ide启动时，默认执行命令 `ruyi --porcelain news list` 获取未读的新闻，并通过窗口展示。未读新闻可能有很多条，列出未读新闻总条数。并默认按照顺序ord的值，先显示最小的ord对应的信息。

- 窗口标题：RuyiSDK News （index/total）:index表示当前阅读的新闻是第几条，total是未读新闻总条数；
- 新闻标题：display_title
- 新闻内容：content
- 按钮：【下一条】【全部已读】
- 点击【下一条】：执行 `ruyi news read <ord>` 标记当前新闻已读；新闻窗口自动切换显示下一条的新闻。窗口标题的index更新；
- 点击【全部已读】：执行 `ruyi news read` 标记所有新闻已读，并关闭窗口。

---

## 设备管理

- 用户可以有多个RISC-V设备
- 用户的RISC-V设备管理：设备将添加到 `~/.config/ruyisdkide/devices.properties `(默认路径)配置文件
- devices.properties 文件格式要求参考如下格式去定义，以方便用户去添加、修改、删除开发板列表

  ```
  # devices.properties 配置文件

  # 定义开发板列表
  device.1.name=milkv duo
  device.1.chip=CV1800B
  device.1.vendor=MilkV
  device.1.version=0.1

  device.2.name=Pioneer Box
  device.2.chip=SG2042
  device.2.vendor=MilkV
  device.2.version=1.2

  device.3.name=LicheePi 4A
  device.3.chip=TH1520
  device.3.vendor=Sipeed
  device.3.version=1.0

  device.4.name=CanMV K230
  device.4.chip=k230
  device.4.vendor=Canaa
  device.4.version=1.2

  device.5.name=HiFive Unmatched
  device.5.chip=U740
  device.5.vendor=SiFive
  device.5.version=1.1

  # 设置默认开发板
  default_device=device.2
  ```

4. 自定义"用户RISC-V开发板"窗口。方便用户通过手动操作打开设备管理窗口。
5. 当用户还未设置为默认设备的时候，提示并引导用户添加设备，并设置默认设备。
6. 用户设备管理窗口：

   - 提示信息：
     - 无开发板的，提示信息为：您还未添加任何RISC-V开发板。提示用户添加开发板
     - 有开发板，但是未设置默认开发板的，提示信息为：您还未设置默认开发板，请设置一款开发板为默认开发板。设置后IDE将按照开发板型号为您推荐合适的开发资源。
     - 有开发板且已经设置默认开发板的，提示信息为：您的设备信息如下
   - 设备列表：
     - 表格表头：开发板型号、SOC、厂商、版本（全部为字符格式）、状态
   - 操作按钮：
     - [button:Add]：用来添加一个开发板。点击后弹出添加开发板的新窗口。
     - [button:Edit]：用来修改一个开发板。开发板列表为空时为disable状态；点击后弹出添加开发板的新窗口。
     - [button:Delete]：用来删除一个开发板。开发板列表为空时为disable状态；点击后将table中选中的开发板从table中删除，删除前弹出确认窗口。
     - [button:SetDefault]：用来定义默认开发板。将table中选中的开发板设置为默认开发板。
     - [button:Save]：保存窗口设置，将变更存到devices.properties 文档；
     - [button:Close]：关闭窗口，放弃修改，不保存。
     - 校验：当有开发板，没有设置默认开发板的时候，提示用户设置默认开发板。
7. 添加、修改设备窗口：

   - 界面中的开发板属性包含：开发板型号、SOC、厂商、版本（全部为字符格式）信息（待定）。
     - milkv duo 64M、CV1800B、MilkV、0.1
     - Pioneer Box、SG2042、MilkV、1.2
     - LicheePi 4A、TH1520、Sipeed、1.0
     - CanMV K230、k230、Canaa、1.2
     - HiFive Unmatched、U740、SiFive、1.1
   - 设备从ruyi接口中获取（package-index仓库中有设备信息）
     ```
     # 获取所有未读的news
     ruyi --porcelain news list
     ```

要求：

1. 实现上述窗口、子窗口界面；以及窗口和子窗口的所有交互事件
2. 模块化实现，后续修改用户默认开发板设置功能将在其它地方调用。我希望在其它模块中，点击一个诸如“修改默认开发板”按钮，可以调出该窗口衔接起来。
3. 扩展性：未来很多与设备有关的功能讲基于设备列表展开，需要有良好的扩展性
   - 设备连接设置，设备连接状态
   - 设备镜像，烧录镜像

## 软件包资源管理

开发一个Eclipse插件，主要用于展示ruyisdk软件源的软件包资源。

1. ruyi软件源提供的软件包资源数据结构通过 `ruyi list --related-to-entity device:sipeed-lpi4a `命令获取（sipeed-lpi4a是设备型号，可以修改）。
   设想的接口返回数据大致会按照类型进行分类，可能是这样的：

   ```
   toolchain
      gnu-upstream 14.2  upstream  https://www.gnu.org/
      gnu-upstream 15  upstream  https://www.gnu.org/
      gnu-plct 14.2  plct  https://github.com/ruyisdk/riscv-gnu-toolchain
      gnu-plct 15  plct  https://github.com/ruyisdk/riscv-gnu-toolchain
      llvm-upstream 17  upstream  https://llvm.org/
      llvm-upstream 19  upstream  https://llvm.org/
      llvm-plct 17  plct  https://github.com/ruyisdk/llvm-project
      llvm-plct 19  plct  https://github.com/ruyisdk/llvm-project
      ........
   emulator
      qemu-upstream 7.8   upstream  https://www.qemu.org/
      qemu-plct 8  plct  https://github.com/ruyisdk/qemu
      ........
   demo
      Helloworld  1.0 plct  https://github.com/ruyisdk/demo/helloworld
      coremark 1.0 plct  https://github.com/ruyisdk/demo/coremark
      ........
   工具
      DynamoRIO   1.0 plct  https://github.com/ruyisdk/dynamorio
      Box64   1.0 plct  https://github.com/ptitSeb/box64
      ........
   ```

   ===接口实现后，实际数据获取===
   包管理器命令行使用：

   ```
   # 首先启用实验模式
   export RUYI_EXPERIMENTAL=true

   # 然后即可使用实验性功能
   ruyi entity describe device:sipeed-lpi4a
   ruyi list --related-to-entity device:sipeed-lpi4a

   # 机器方便读取的输出方式
   ruyi --porcelain list --related-to-entity device:sipeed-lpi4a

   ```

   ```
   # 设备型号
   ruyi --porcelain entity list -t device

   # 根据设备型号查看使用设备的软件包
   RUYI_EXPERIMENTAL=x 
   ruyi --porcelain list --related-to-entity device:<deviceName>

   ```
2. 自定义“RuyiSDK软件包窗口”，该窗口主要用于展示ruyisdk软件源中管理的编译器、模拟器、调试器、应用示例等软件包。

   Eclipse 插件开发中，使用树状目录等可展开/折叠 展示效果来展示软件包资源。并且要求同时实现：

   1. 需要在每个节点前加checkbox。从本地缓存中查看软件包是否已经下载缓存在本地，如果是，怎checkbox为check状态，并且设置为disable，表示不用再下载；如果本地无缓存（没下载过），则checkbox为空，且able可选。
   2. 每个节点需要展示的信息后续可能扩展成多属性：如gnu-upstream 14.2，有好多信息，如 gnu-upstream 、版本 14.2、发行单位 upstream、参考文档：linkurl等；
   3. 整个软件包资源树结构要控制在一定的显示区域内，超过部分通过滚动条控制显示。
   4. 点击确认的时候，会检验编译器、应用示例这两类是否至少勾选了一个节点，比如编译工具链必须勾选一个工具链gnu-upstream 14.2，否则提醒用户勾选。
      资源数据结构主要包含包名、版本，大致如下：
   5. 按钮：

      - [Radio Button]：显示[Lable:默认开发板]适用（默认选中）
      - [Radio Button]：显示所有
      - [Button：下载]：点击后开始下载被选中的资源，在后台依次执行下载，并在RuyiSDK控制台同步显示下载安装的进度和情况。在日志窗口显示下载日志。
   6. 右键：

      - 卸载指定软件包
      - 查看指定软件包安装位置
      - 查看缓存位置
      - 清除本地缓存（所有缓存）
3. 安装软件包（并获取安装路径）：通过执行命令行程序：'ruyi install <软件包名>'完成软件包的安装。
4. 安装时，将ruyi install安装过程信息在 ruyisdk 控制台输出；并将日志记录到 ruyisdk日志中。完成后能否获取输出信息？
5. 注意：ruyi install 本身有常规的默认缓存路径，遵循 XDG 规范

## 整体要求

插件采用模块化设计，主要包含以下模块：

1. **核心模块**：负责Ruyi包管理器的安装、检测和更新
2. **配置模块**：处理XDG规范路径和配置文件管理
3. **新闻模块**：处理新闻展示和标记已读功能
4. **设备管理模块**：管理RISC-V开发板信息
5. **软件包管理模块**：展示和安装软件包资源
6. **UI模块**：提供用户界面和交互
7. 统一的日志/console管理：通过自定义 RuyiSDK控制台的方式输出后台操作。并且在日志窗口中输出操作日志。
