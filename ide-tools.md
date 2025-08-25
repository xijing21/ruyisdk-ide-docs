# RuyiSDK 工具

## RISC-V 分析工具

### CrashDecoder

崩溃解码器，这是一种用于分析和解码应用程序崩溃日志的工具。当应用程序发生崩溃时，它会生成一个崩溃日志（也称为“崩溃转储”或“崩溃报告”），CrashDecoder 可以帮助开发人员更深入地了解崩溃的原因，从而修复问题。

### RVPerfMon & Vis

RVPerfMon（RISC-V Performance Monitor）一款性能监控工具，它可以用于监控和记录系统中的关键性能指标，如CPU使用率、内存使用情况、磁盘I/O操作、网络流量等。通过PerfMon，用户可以实时查看这些指标的数据，以及通过图表化的界面来直观地理解系统性能的变化趋势。此外，PerfMon还支持性能日志的记录，可以将监控数据保存为不同的格式。

“Vis”是什么？

### CodeSize Analyzer

代码大小分析器。这是一种工具，用于分析和测量软件项目的代码大小。开发人员可以使用 CodeSize Analyzer 来确定代码的体积，以及如何优化和减小代码大小，从而提高软件的性能和可维护性。

这个工具主要用于对编译工具链编译构建的代码大小进行分析，从而评估编译器在编译方面对代码大小的优化效率。

### Device Watcher

设备监视器。这是一个用于监控和管理连接到计算机上的设备的工具。Device Watcher 可以跟踪设备的连接和断开，以及其他与设备相关的操作，例如设备的启用、禁用、更新等。这对于开发人员来说是一个有用的工具，因为他们需要确保他们的软件能够正确地识别和与各种设备进行交互。

## IDE 工具

### RISC-V Solution CodeBase

RISC-V Solution CodeBase简单来说是一种包含各种RISC-V相关软件和硬件解决方案的代码库。这些代码可以是从网上抓出来很多基于RISC-V的代码。

RISC-V Solution CodeBase开源代码实现包括的一个小的CPU怎么实现，和RISC-V相关的一些软件的代码示例怎么做，这其实就是当做是一个可以帮助新人学习的一个巨大的代码库。通过这个代码库是能够推荐出来通过AI的方式能够汇总和推荐出来一些代码示例的。那么这就是RISC-V Solution CodeBase这个名字对应的内涵，它其实就是从网上抓取了一个巨大的代码库，这个代码库包含RISC-V的芯片设计代码（主要是Chisel和RISC-V的一些常用的编译器使用的一些示例代码，主要是C和C++程序）。

### Device DriverWell

Device DriverWell 在IDE当中以向导提示的方式提示、询问开发者要去支持哪些RISC-V开发板（比如用户使用的是哪些RISC-V相关的硬件），然后RuyiSDK会维护一个巨大的、尽可能全面的RISC-V的硬件设备的列表或者是仓库。

Device DriverWell就是相当于能够让用户很方便的，通过相似代码对新的RISC-V设备去撰写，根据它的功能点去进行一些这个代码的提示 甚至是整个代码的自动化生成。

### TaiFu Knowledge Miner

TaiFu Knowledge Miner 其实就是对整个代码做一段摘要、中文摘要描述。就比如说用户导入了一个新的项目之后，TaiFu Knowledge Miner可以去尝试解释这段RISC-V相关的代码：它在做什么，然后用到了哪些RISC-V相关的扩展。就相当于给代码做一段摘要、中文摘要描述。

### RISC-V SpecRiver

RISC-V SpecRiver 其实就是一个专门的搜索引擎，用来搜索RISC-V相关的标准草案的工作。我们想做的最大的特点是在于它不仅能够搜索当前版本的RISC-V指令及手册，还能够找到这个手册当中的历史版本当中的变更情况。river的一个目标就是我们希望能够在RuyiSDK当中能够搜索到一个标准的某一个技术实现细节是如何提出和演变，变成现状的。

### Syntax Highlighter

Syntax Highlighter 语法高亮器。这是一个用于在代码编辑器中突出显示和显示不同语法元素的工具，以便开发人员可以更容易地阅读和理解代码。

### StaticSec Checker

静态安全检查器。这是一个用于检查代码中的潜在安全漏洞的工具，它可以在代码运行之前发现和修复这些问题。

属于外部集成。

### License Complainer

一个用于检查软件许可证合规性的工具，它可以识别和报告任何违反许可证条款的行为。

1. **许可合规性检查器**：一个工具或脚本，用于检查软件许可是否符合特定的合规性要求，例如GPL（GNU General Public License）或其他开源许可证。
2. **许可问题报告器**：一个用于报告软件许可问题的工具，它可以帮助开发者或组织识别和解决与软件许可相关的潜在问题。
3. **许可管理器**：一个用于管理软件许可证的工具，它可以帮助用户跟踪、更新和维护许可证信息。
4. **合规性审计工具**：用于审计软件或系统以符合特定许可协议的工具。
   如果你在寻找与性能监控相关的特定工具或功能，可能需要更多的上下文信息来确定"License Complainer"的确切含义。如果你有更多的信息或者上下文，我可以尝试提供更具体的解释。

属于外部集成。

### IntelliError Searcher

IntelliError Searcher 智能错误搜索器是在对程序编译构件的输出的log进行搜索和识别代码中错误和问题的工具。当我编译的时候，如果出现了错误，最基本的编译器是定位到这个错误最后一次发生的位置，但是错误的根源、错误背后的逻辑错误，我希望通过一些更加智能的方式去分析。

### Compatibility Recognizor

Compatibility Recognizor，兼容性识别器，用于检查软件或硬件组件之间兼容性的工具，它可以识别和报告任何兼容性问题。

在RISC-V领域，现在比较知名的有这样的一个场景：一个代码当中用了vector的指令，它用的是vector的0.7的版本还是1.0的版本、然后跟内部的代码是不是有重叠的，或者说是不是兼容的。有可能是不兼容的，有可能这个代码导入的时候是1.0的版本，但是是混合的，目标设备是0.7，那么跑上去一定会crash，这个时候IDE要能给出这样的一个提示。

vector是一个最著名的例子，除此之外其实还有很多不同的版本的问题。包括RVI的profiles的相关的版本的支持。所以这个第71行可以理解为是一个对源代码的分析工具。这个分析工具是跟目标设备的配置直接相关的。

### AI-Enhanced Indexer

AI-Enhanced Indexer 人工智能增强索引器，一个使用人工智能技术来提高索引效率和准确性的工具。

### Remind Rehearsal

提醒排练，这可能是一个用于设置和接收提醒的工具，以便在特定时间或事件发生时进行排练。

# 工具调研

| 工具名称 外部集成        | 研发类型 | 是否有近似开源软件 | 开源软件实现现状 | 开源软件改进意见 |
| ------------------------ | -------- | ------------------ | ---------------- | ---------------- |
| CrashDecoder             | 自主研发 |                    |                  |                  |
| RVPerfMon & Vis          | 自主研发 |                    |                  |                  |
| CodeSize Analyzer        | 自主研发 |                    |                  |                  |
| Device Watcher           | 自主研发 |                    |                  |                  |
| RISC-V Solution CodeBase | 自主研发 |                    |                  |                  |
| Device DriverWell        | 自主研发 |                    |                  |                  |
| TaiFu Knowledge Miner    | 自主研发 |                    |                  |                  |
| RISC-V SpecRiver         | 自主研发 |                    |                  |                  |
| Syntax Highlighter       | 自主研发 |                    |                  |                  |
| StaticSec Checker        | 外部集成 |                    |                  |                  |
| License Complainer       | 外部集成 |                    |                  |                  |
| IntelliError Searcher    | 自主研发 |                    |                  |                  |
| Compatibility Recognizor | 自主研发 |                    |                  |                  |
| AI-Enhanced Indexer      | 外部集成 |                    |                  |                  |
| Remind Rehearsal         | 自主研发 |                    |                  |                  |
