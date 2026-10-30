# STM32F411 学习作业：LED 控制

本仓库用于保存 STM32F411 学习工程与作业。当前分支为 `01_led`，实现读取 PA0 按键输入，并控制 PC13 的 LED 输出。

## 分支与模板

- `master`：基础目录模板，供后续作业使用；本地放在 `00_base` 文件夹。
- `01_led`：LED 作业；本地放在 `01_led` 文件夹，完整工程位于 `03_Firmware/02_APP`。

两个本地文件夹分别是同一远程仓库的独立克隆，各自保留 Git 配置和工作目录。

## 目录结构

```text
.
├─00_Project_Management/     # 需求、风险、开发与项目管理文档
├─00_Reference/              # 参考资料
│  └─01_Docs/
├─01_Function_Map/           # 功能需求与流程图
├─02_Hardware/               # 硬件参考资料与设计工程
│  ├─00_Ref/00_HDK/
│  └─01_Project/
├─03_Firmware/               # 嵌入式固件工程
│  ├─01_Bootloader/          # 预留，目前未实现
│  └─02_APP/                # LED 应用完整工程
│     ├─Core/               # 应用代码与头文件
│     ├─Drivers/            # CMSIS 与 STM32 HAL 驱动
│     ├─MDK-ARM/            # Keil 工程与启动文件
│     ├─.mxproject
│     ├─01_led.ioc          # STM32CubeMX 配置
│     └─README.md           # 引脚、功能与编译说明
├─04_Software/               # 预留的软件资料与源码
│  ├─00_Ref/00_SDK/
│  └─01_Source_Code/
├─05_Mechanical/             # 机械结构资料
├─06_FCT/                    # 工厂测试相关资料与工具
├─07_Tools/                  # 开发辅助工具
├─.gitignore
└─README.md
```

模板中的子目录与 `.gitkeep` 保留，用于保存完整目录结构；当前 LED 工程集中放在 `03_Firmware/02_APP`。

## 打开工程

1. 使用 Keil µVision 打开 [01_led.uvprojx](03_Firmware/02_APP/MDK-ARM/01_led.uvprojx)。
2. 选择 `01_led` Target，执行 Rebuild，检查编译结果。
3. 根据实际调试器连接配置下载程序。

引脚配置、程序行为及开发环境见 [LED 应用说明](03_Firmware/02_APP/README.md)。需要修改外设配置时，使用 STM32CubeMX 打开 [01_led.ioc](03_Firmware/02_APP/01_led.ioc)。

## 仓库与目录来源

- [Gitee 仓库](https://gitee.com/L-ml_0920/stm32f411-homework)
- [GitHub 仓库](https://github.com/LML-920/stm32f411-homework)
- 目录参考 [EmbeddedProject-Folder-Template](https://gitee.com/xing_mou/EmbeddedProject-Folder-Template)，在 `03_Firmware` 下增加 Bootloader 与应用工程目录。
