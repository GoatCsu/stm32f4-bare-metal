# 嵌入式课程作业报告

## 一、基本信息

- 课程名称：嵌入式课程作业
- 专业班级：计算机科学与技术 2403
- 学号：8208241315
- 项目名称：stm32f4-bare-metal

## 二、作业目标

本次作业主要完成以下两项任务：

1. 在 GitHub 或 Gitee 等平台创建一个公开开源仓库，选择合适的开源协议，并使用 Git 工具完成不少于两次提交。
2. 在 macOS 环境下配置 `arm-none-eabi-gcc` 嵌入式交叉编译环境，编译 STM32F4 裸机项目并生成固件文件。

## 三、实验环境

- 操作系统：macOS
- 交叉编译工具链：Arm GNU Toolchain 15.2.Rel1
- 编译器：`arm-none-eabi-gcc`
- 构建工具：`make`
- 版本管理工具：`git`
- 开源项目：`stm32f4-bare-metal`
- 参考源码仓库：<https://github.com/fcayci/stm32f4-bare-metal>

工具链版本输出见：

- `toolchain-version.txt`

## 四、开源仓库创建与 Git 提交

### 4.1 创建公开仓库

在 GitHub 或 Gitee 上创建一个公开仓库，仓库可命名为 `embedded-lab-demo` 或与作业题目相关的名称，并选择 MIT License 作为开源协议。

本项目建议在报告中写明：

> 本项目采用 MIT 开源协议，允许他人自由使用、修改与分发代码。

需要在此处补充你自己的仓库链接：

- 仓库链接：<https://github.com/GoatCsu/stm32f4-bare-metal>

### 4.2 Git 提交记录

本次作业要求至少完成两次提交。当前已有截图可以作为提交过程与历史记录的证明：

- `screenshots/01-git-commit-operation.png`
- `screenshots/02-git-history.png`

建议在你自己的公开仓库中至少保留如下两次提交：

1. 初始提交，例如 `init project`
2. 更新提交，例如 `add report and build files`

## 五、交叉编译环境配置

本次作业在 macOS 下完成。最初使用其他路径下的 `arm-none-eabi-gcc` 时出现了 `specs` 文件缺失的问题，因此改为使用官方安装的 Arm GNU Toolchain。

官方工具链安装位置为：

```text
/Applications/ArmGNUToolchain/15.2.rel1/arm-none-eabi/bin/arm-none-eabi-gcc
```

在配置过程中，曾出现旧工具链导致的报错，该排错截图已保留：

- `screenshots/03-toolchain-error.png`

最终可正常使用的编译器版本信息见：

- `toolchain-version.txt`

## 六、项目编译过程

本次选用的开源项目为 STM32F4 裸机工程 `stm32f4-bare-metal`。该项目不依赖 HAL 库，直接进行底层寄存器级开发，适合作为嵌入式课程作业示例。

### 6.1 编译命令

在项目目录下进入 `blinky` 示例工程并执行：

```bash
cd projects/blinky
make clean
make
```

### 6.2 环境问题处理

编译过程中发现原始构建配置依赖 `nano.specs`，而当前环境下更适合使用 `nosys.specs`。因此对工程构建文件进行了调整，使其更适配裸机开发环境，并优先识别 macOS 下官方安装的 Arm GNU Toolchain。

### 6.3 编译结果

编译成功后，终端输出如下关键信息：

```text
text = 1164
data = 16
bss  = 1972
dec  = 3152
hex  = c50
Successfully finished...
```

完整构建日志见：

- `build-log.txt`

## 七、生成的固件文件

编译成功后生成的主要文件已整理至 `artifacts/` 目录，包括：

- `artifacts/blinky.elf`
- `artifacts/blinky.bin`
- `artifacts/blinky.map`
- `artifacts/blinky.lst`

其中：

- `blinky.elf` 为可执行固件文件
- `blinky.bin` 为可烧录的二进制固件文件
- `blinky.map` 为链接映射文件
- `blinky.lst` 为反汇编与列表文件

文件清单与大小见：

- `artifacts-list.txt`

## 八、实验结果分析

本次作业完成了从开源项目获取、工具链配置、问题排查到固件编译输出的完整流程，说明当前 macOS 环境已经具备 STM32F4 裸机项目的基本交叉编译能力。

通过本次实验可以看出：

1. `arm-none-eabi-gcc` 是 ARM 裸机开发的核心工具链。
2. 裸机工程通常不依赖操作系统，因此 `nosys.specs` 更适合当前工程构建。
3. STM32F4 裸机项目能够成功生成 `.elf` 与 `.bin` 文件，说明交叉编译环境配置正确。

## 九、总结

本次作业成功完成了以下内容：

1. 选择并使用开源 STM32F4 裸机项目作为实验对象。
2. 在 macOS 环境下配置 ARM 嵌入式交叉编译工具链。
3. 成功编译 `blinky` 示例并生成固件文件。
4. 整理了提交过程截图、工具链版本信息、编译日志和编译产物。

本次实验不仅加深了对 ARM 交叉编译流程的理解，也提高了对嵌入式构建环境问题的定位与处理能力。
