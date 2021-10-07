时间管理插件
时间轴
![[Pasted image 20211006193037.png]]

该命令可用于添加垂直时间线视图，显示当今日规划器的任务，以及显示当前时间的行。`Show the Day Planner Timeline`
------------------------
语法格式

### 晚间计划
- [ ] 19:00 做笔记
- [ ] 20:00 freertos
- [ ] 20:50 开始休息
- [ ] 21:00 高等数学

- [ ] 22:00 END
------------------------------
此存储库包含[黑石](https://obsidian.md/)的插件，用于日规划和管理标记笔记中任务列表中的 pomodoro 定时器。

> 这是插件的早期阿尔法版本，它会在后台持续运行，而黑石是打开的，插件是启用的。**请先尝试测试库中的插件，最重要的是，确保您的笔记在云存储或 Git 中备份。**

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#features)特征

-   每天为您生成一个日规划师，或在您选择的任何注释中创建日规划师。
-   状态条更新进度，并提供当前和下一个任务的信息。您可以单击状态栏来访问当前日规划器的注释。
-   美人鱼甘特图表自动生成从您的任务，并包含在您的日规划师说明。
-   显示垂直时间轴上显示任务的时间轴视图。

[![Day Planner Demo Image](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/day-planner-note-preview.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/day-planner-note-preview.png)

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#usage)用法

安装后，插件将在库根部创建一个名为"日规划器"的文件夹。今天的注意事项将自动创建与文件名格式。`Day Planners/Day Planner-YYYYMMDD.md`

您可以选择使用[命令模式](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#day-planner-mode)，而不是在任何注释中添加当天的日规划器。

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#day-planner-note)日规划师说明

在注释中，您可以创建一个包含时间和任务的检查列表，这些时间和任务将在白天自动跟踪。现在，您可以在任务之间包含标题和其他内容。下面是一个示例：

## Day Planner

This is my plan for the day broken into 3 main sections:
1. Morning Prep
2. Reading
3. Afternoon Review

### Morning Prep

This is where I get ready for work and do my usual prep.

- [ ] 09:30 Setup for work
- [ ] 09:45 Review notes from yesterday
- [ ] 10:30 Create new notes for #article review
- [ ] 11:30 BREAK

### Reading

A section of the day dedicated to reading:

1. Articles.
2. Book chapters assigned for the day.
3. Re-reading past notes.
   
- [ ] 12:00 Reading
  - [ ] Article 1
  - [ ] Article 2
  - [ ] Article notes review
- [ ] 12:25 BREAK
- [ ] 12:30 Reading
- [ ] 14:00 BREAK

### Afternoon Review

I use this time to review what I have done earlier in the day and complete any tasks to prepare for the next day.

- [ ] 15:00 Review notes and update daily note [[20201103]]
- [ ] 15:45 Walk
- [ ] 16:30 Reading
- [ ] 17:20 Prep for tomorrow's meetings
- [ ] 18:00 END

这也是作为文件在[day-planner-example.md](https://github.com/lynchjames/obsidian-day-planner/blob/main/examples/day-planner-example.md)提供。

日规划器标题和规则用于确定日规划器的程度。标题必须使用，但可以，或。`---``#``##``###``####`

任务列表项目的格式很重要，因为这是用于计算每个任务的时间和任务之间的间隔。使用的格式应为：

`- [ ] HH:mm Task text`

**应使用 24 小时时间。**

嵌套清单项目或子弹现在也支持捕获时间任务的子任务。定时任务必须在复选框列表的顶层。

`BREAK`并且是定义任务中断和时间跟踪结束的关键字。它们对案例不敏感，因此也可以使用。两个关键字都是可配置的，可以在日规划器设置选项卡中进行自定义。`END``break``end``BREAK``END`

`END`用作一个项目，有时间给出最后一个任务的准确时间间隔，"_为明天的会议准备"_在17：00在本示例中。

注释将自动更新：将检查过去的任务并标记为已完成。

使用以上示例，在 14：30 时，注释将自动更新为：

## Day Planner

This is my plan for the day broken into 3 main sections:
1. Morning Prep
2. Reading
3. Afternoon Review

### Morning Prep

This is where I get ready for work and do my usual prep.

- [x] 09:30 Setup for work
- [x] 09:45 Review notes from yesterday
- [x] 10:30 Create new notes for #article review
- [x] 11:30 BREAK

### Reading

A section of the day dedicated to reading:

1. Articles.
2. Book chapters assigned for the day.
3. Re-reading past notes.
   
- [x] 12:00 Reading
  - [ ] Article 1
  - [ ] Article 2
  - [ ] Article notes review
- [x] 12:25 BREAK
- [x] 12:30 Reading
- [ ] 14:00 BREAK

### Afternoon Review

I use this time to review what I have done earlier in the day and complete any tasks to prepare for the next day.

- [ ] 15:00 Review notes and update daily note [[20201103]]
- [ ] 15:45 Walk
- [ ] 16:30 Reading
- [ ] 17:20 Prep for tomorrow's meetings
- [ ] 18:00 END

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#timeline-view)时间轴视图

该命令可用于添加垂直时间线视图，显示当今日规划器的任务，以及显示当前时间的行。`Show the Day Planner Timeline`

[![Day Planner Timeline](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/day-planner-timeline.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/day-planner-timeline.png)

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#status-bar)状态栏

黑石的状态栏也将显示当前任务的进展或与剩余时间中断。单击状态栏项目将带您到日规划师说明。

#### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#task-status)任务状态

当有一个活跃的任务时显示的状态：

[![Task Status](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/task-status.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/task-status.png)

#### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#break-status)中断状态

休息期间显示的状态：

[![Break Status](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/break-status.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/break-status.png)

#### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#end-status)结束状态

到达任务结束时显示的状态：

[![End Status](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/end-status.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/end-status.png)

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#configuration)配置

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#day-planner-mode)日规划模式

有 2 种模式使用日规划器插件：

**文件模式**

插件会自动在日规划器文件夹内生成每天的日规划器笔记。

**命令模式**

命令用于在任何注释中插入今天的日规划器，以及将今天的日规划师与其当前注释脱钩。

> 注：要将日规划师添加到当前注释中，您首先需要通过运行命令"日规划师：将今天的日规划师链接到当前注释"或"日规划师：从命令调色板中将今天的日规划师模板添加到当前注释"来将日规划器链接到当前注释中。

只要使用所提供的格式，日规划师就可以放置在注释中的任意位置。只有笔记中的日规划器部分将随着时间的推进而更新。

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#complete-past-planner-items)完整的过去规划器项目

您可以选择插件是否会自动标记过去规划器项目是否完整，或者允许您自己勾选它们。

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#mermaid-gantt)美人鱼甘特

您可以选择在日规划仪中包含动态生成的[美人鱼甘特图表](https://mermaid-js.github.io/mermaid/#/gantt)。

任务和休息将显示在单独的部分，以帮助可视化您的计划一天。

[![Mermaid Gantt Chart Example](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/mermaid-gantt.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/mermaid-gantt.png)

甘特图表的颜色可以覆盖自定义CSS和有[美人鱼文档](https://mermaid-js.github.io/mermaid/#/gantt?id=styling)的类。提供了带有任务和中断部分示例的 CSS 文件：

[美人鱼 - 甘特的例子.css](https://github.com/lynchjames/obsidian-day-planner/blob/main/examples/mermaid-gantt-example.css)

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#status-bar---circular-progress)状态栏 - 循环进度

您可以选择使用圆形饼图进度栏在状态栏中显示进度，以节省水平空间。

[![Circular Progress Bar](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/circular-progress.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/circular-progress.png)

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#status-bar---now-and-next)状态栏 - 现在和下一个

您可以选择显示当前和下一个任务的文本的时间和开始。

[![Now and Next](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/now-and-next.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/now-and-next.png)

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#task-notification)任务通知

当新任务开始时，您可以选择有应用内通知显示屏。

### [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#timeline-zoom-level)时间轴缩放级别

这是显示时间线的变焦级别。数字越高，每个任务的垂直空间就越大。

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#commands)命令

使用插入式命令模式，2 个命令可用于链接和解链接日规划器。

[![Plugin Commands](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/commands.png)](https://raw.githubusercontent.com/lynchjames/obsidian-day-planner/main/images/commands.png)

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#compatibility)兼容性

自定义插件仅适用于黑石 v0.9.7+。

本回购的当前 API 针对黑石**v0.9.10。**

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#installing)安装

从[黑石的0.9.7](https://forum.obsidian.md/t/obsidian-release-v0-9-7-insider-build/7628)版本，这个插件可以直接安装在应用程序内。插件可在社区插件目录中找到，可从第三方插件下的"设置窗格"访问。

## [](https://github.com/lynchjames/obsidian-day-planner/blob/main/README.md#manual-installation)手动安装

1.  下载[最新版本](https://github.com/lynchjames/obsidian-day-planner/releases/latest)
2.  将黑石日规划文件夹从拉链中提取到金库的插件文件夹：  
    注意：在某些机器上，文件夹可能被隐藏。在 MacOS 上，您应该能够按压以显示 Finder 中的文件夹。`<vault>/.obsidian/plugins/``.obsidian``Command+Shift+Dot`
3.  重新加载黑石
4.  如果提示有关安全模式，您可以禁用安全模式并启用插件。