# LED 应用工程

本目录是 `01_led` 分支的完整 STM32F411 应用工程，包含 STM32CubeMX 配置、应用源码、HAL 驱动和 Keil 工程文件。

## 功能与引脚

程序在主循环中轮询 PA0 的输入电平，并让 PC13 输出相同电平。

| 信号 | 引脚 | 配置 |
| --- | --- | --- |
| `KEY` | PA0 | GPIO 输入，内部上拉 |
| `LED` | PC13 | 推挽输出，无上下拉，低速；初始化输出低电平 |

按键采用按下接地的接法时，行为如下：

| 按键状态 | PA0 输入 | PC13 输出 |
| --- | --- | --- |
| 按下 | 低电平 | 低电平 |
| 松开 | 高电平 | 高电平 |

若 LED 为低电平点亮的接法，表现为按住点亮、松开熄灭。实际亮灭取决于 LED 的硬件接法。当前代码直接跟随按键电平，未加入软件消抖或按一次切换状态的逻辑。

## 代码位置

| 文件 | 用途 |
| --- | --- |
| [Core/Src/main.c](Core/Src/main.c) | 初始化、系统时钟配置及按键控制 LED 的主循环 |
| [Core/Src/gpio.c](Core/Src/gpio.c) | PA0 与 PC13 的 GPIO 初始化 |
| [Core/Inc/main.h](Core/Inc/main.h) | `KEY`、`LED` 的引脚与端口定义 |
| [01_led.ioc](01_led.ioc) | STM32CubeMX 工程配置 |
| [MDK-ARM/01_led.uvprojx](MDK-ARM/01_led.uvprojx) | Keil µVision 工程入口 |
| `Drivers/` | CMSIS 与 STM32F4 HAL 驱动 |

## 工程环境

以下版本来自当前工程配置，供配置开发环境时参考。

| 项目 | 配置 |
| --- | --- |
| MCU | STM32F411CEU6（Keil 器件名为 STM32F411CEUx） |
| 系统时钟 | 100 MHz，使用内部 HSI 经 PLL 倍频 |
| 开发工具 | Keil MDK-ARM / µVision |
| 编译器 | ARM Compiler 5.06 update 5 |
| 器件包 | Keil.STM32F4xx_DFP 2.8.0 |
| STM32CubeMX | 6.8.1 |
| STM32Cube 固件包 | STM32Cube FW_F4 V1.27.1 |

## 编译与下载

1. 在 Keil µVision 中打开本目录下的 `MDK-ARM/01_led.uvprojx`。
2. 选择 `01_led` Target，确认已配置工程所需的编译器与器件包。
3. 执行 Rebuild，确认编译结果为 `0 Error(s)`。
4. 连接开发板和调试器，在 Target Options 中按实际硬件设置 Debug 与 Flash Download，然后下载程序。
5. 若使用上述按键和 LED 接法，检查按住点亮、松开熄灭的行为。

工程已启用 HEX 输出，编译产物位于 `MDK-ARM/01_led/`；当前仓库的 `.gitignore` 会忽略 `.hex`、`.axf` 等编译产物。

## 修改与维护

外设配置通过本目录下的 `01_led.ioc` 修改；用户代码写在 `USER CODE BEGIN` 与 `USER CODE END` 区域中，便于 STM32CubeMX 再次生成代码时保留。

移动或复制工程时，一起保留 `Core`、`Drivers`、`MDK-ARM`、`.mxproject` 和 `01_led.ioc`，维持现有相对目录关系。

返回 [仓库说明](../../README.md)。
