## Ruyi包管理器插件

### 主要需求

1. **Ruyi包管理器管理**
   - **安装检测**：检测Ruyi包管理器是否安装，并提供安装引导。
   - **版本检测**：检测当前安装的Ruyi包管理器版本
   - **安装/升级**：提供包管理器的安装功能(升级当前即为安装ruyi最新版本覆盖本地ruyi即可)
   - **配置**：允许用户配置包管理器的相关设置。且所有配置项的值对应用户配置文档，根据用户配置的值执行（用户默认配置为系统设定的默认配置）
     - 启动时是否自动检测ruyi安装情况和本地安装版本
     - 后台自动升级ruyi
     - 安装路径配置
     - 软件源配置（支持自定义软件源）
     - 遥测模式配置
   - **本地路径管理**
     - 使用XDG规范定义IDE相关配置路径
     - 提供XDG工具类，自动检测环境变量并创建默认目录
   - **启动与关闭流程**
     - IDE启动时自动检查并更新Ruyi
     - IDE退出时上传遥测数据
2. **新闻展示**
   - 可配置是否启动时自动展示新闻
   - 新闻展示：提供启动时展示新闻、菜单命令展示新闻两种操作方式
   - 未读新闻提示：未读新闻条数、未读新闻条目
   - 新闻浏览：提供新闻浏览和标记已读功能
   - 标记全部已读
3. **设备管理**
   - 用户设备管理：通过本地配置文件管理用户设备信息
   - 支持添加、编辑、删除开发板（从包管理器接口获取设备信息，添加到用户设备）
   - 设置默认开发板
   - 预留扩展：设备连接状态（设备连接配置）、目标设备镜像（镜像烧录）等状态显示和操作入口；
4. **软件包资源管理**
   - 展示ruyisdk软件源中的软件包资源：树状结构？
   - 支持按开发板筛选软件包：根据指定的设备展示设备使用的软件包资源
   - 提供软件包下载和安装功能
   - 能体现软件包本地安装状态
   - 提供软件包的卸载功能

### 技术需求

1. 使用插件开发框架
2. 模块化设计，便于扩展和维护
3. 遵循XDG规范管理配置文件
4. 在自定义控制台视图、和日志视图、日志文件中输出重要的状态和过程信息
5. ruyi包管理器插件能够上架插件中心/软件市场，**在ide的插件市场中搜索并安装**

---

### 部分技术细节约定

#### 本地路径设置

使用XDG 规范来定义定制化eclipse ide（ruyisdkide）的相关配置路径。
为插件提供XDG工具类，能够自动检测是否存在环境变量，并判断和创建ide的默认目录 ruyisdkide

XDG 规范标准目录：

| 环境变量             | 默认路径            | 用途                                    | ruyisdkide目录                |
| -------------------- | ------------------- | --------------------------------------- | ----------------------------- |
| `$XDG_CONFIG_HOME` | `~/.config/`      | 用户配置文件（如 `.json`, `.conf`） | `~/.config/ruyisdkide`      |
| `$XDG_CACHE_HOME`  | `~/.cache/`       | 缓存文件（临时数据，可删除）            | `~/.cache/ruyisdkide`       |
| `$XDG_DATA_HOME`   | `~/.local/share/` | 持久化数据（如数据库、设备配置）        | `~/.local/share/ruyisdkide` |
| `$XDG_STATE_HOME`  | `~/.local/state/` | 应用程序状态（如历史记录、日志）        | `~/.local/state/ruyisdkide` |

- ruyi.properties：
  - 默认路径：/.config/ruyisdkide/ruyi.properties
  - 文档结构：示例
    ```
    #Ruyi Configuration
    automatic.detection=on
    ruyi.install.path=/home/phebe/.local/bin
    ruyi.mirror.custom=
    ruyi.mirror.custom.checked=0
    ruyi.mirror.github.checked=1
    ruyi.mirror.iscas.checked=1
    ruyi.telemetry.status=on

    ```
- devices.properties：
  - 默认路径：/.config/ruyisdkide/devices.properties
  - 文档结构：示例
    ```
    #RuyiSDK Devices Configuration
    default_device=device.2
    device.1.chip=CV1008
    device.1.name=milkv duo
    device.1.vendor=milkv
    device.1.version=1.0
    device.2.chip=SG2000
    device.2.name=milkv duos
    device.2.vendor=milkv
    device.2.version=1.1

    ```

