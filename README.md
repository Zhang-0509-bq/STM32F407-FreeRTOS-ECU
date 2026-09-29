# STM32F407 + FreeRTOS ECU Controller

基于 STM32F407 和 FreeRTOS 开发的车载 ECU 控制器项目，主要用于学习和实践 MCU 实时系统、CAN 通信、故障管理及 Bootloader 等嵌入式软件开发内容。

## 功能

- FreeRTOS 多任务
  - 数据采集
  - 控制
  - CAN 通信
  - 故障检测
  - Watchdog

- ADC + DMA 多通道采集
  - 滑动平均滤波
  - 阈值检测

- CAN 通信
  - 周期报文收发
  - Signal 编解码
  - Alive Counter
  - CRC
  - Timeout 检测
  - Bus-Off 恢复

- Fault Manager
  - 过温
  - 过压
  - 传感器异常
  - 故障防抖
  - 故障锁存与恢复

- Watchdog
  - Task Heartbeat
  - IWDG

- Bootloader
  - 固件接收
  - Flash 擦写
  - CRC 校验
  - APP Jump

## 硬件

- STM32F407ZGT6
- TJA1050 CAN Transceiver
- USB-CAN
- NTC 10K Temperature Sensor
- 5 V Fan + MOSFET Driver
- 5 V Relay Module
- Potentiometer

## 软件架构

Application
├── ECU State Machine
├── Control
└── Fault Manager

Service
├── CAN Manager
├── Signal Manager
├── Watchdog Manager
└── NVM Manager

BSP
├── ADC / DMA
├── CAN
├── UART
├── Timer / PWM
├── Flash
└── IWDG

## CAN Matrix

| CAN ID | Signal | Cycle |
|---|---|---|
| 0x100 | Vehicle Speed | 10 ms |
| 0x101 | Motor Speed | 10 ms |
| 0x102 | Temperature | 100 ms |
| 0x200 | ECU Status | 100 ms |
| 0x201 | Fault Status | 100 ms |

## 项目目录

ECU/
├── BSP/
├── Driver/
├── Service/
├── Application/
├── Bootloader/
└── README.md

## 测试

项目通过 USB-CAN 和串口日志进行功能验证，包括：

- CAN 周期报文测试
- CAN Timeout 测试
- CRC / Alive Counter 异常测试
- Bus-Off 恢复测试
- 传感器故障注入
- Task Heartbeat / IWDG 测试
- Bootloader 固件升级测试

## 开发环境

- STM32F407ZGT6
- STM32CubeMX / STM32CubeIDE
- FreeRTOS
- C
- Git
