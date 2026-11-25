# ESP32 BLE 开发分支（esp32-ble）

本分支用于 **ESP32-WROOM-32E** 的 BLE 开发与验证，与主分支的机械臂/主控业务解耦。

## 技术选型

| 项目 | 选择 | 原因 |
| --- | --- | --- |
| 框架 | ESP-IDF v5.5.6 | 稳定分支最新 bugfix，教程兼容性最好 |
| 协议栈 | NimBLE | 约 30~50 KB RAM，远小于 Bluedroid 的 100~130 KB |
| GATT 服务 | Nordic UART Service 风格自定义 128 位 UUID | 手机端现成 App 可直接调试 |
| 目标链路 | STM32F103 UART ↔ ESP32 ↔ BLE ↔ 手机/上位机 | 与主控项目对接 |

## 规划目录

```
firmware/     ESP-IDF 工程（GATT Server / UART 透传）
docs/         协议说明、UUID 表、调试记录
tools/        烧写与自检脚本
```

## 进度

- [x] 建立 esp32-ble 分支
- [ ] GATT Server 工程迁入
- [ ] UART ↔ BLE 透传
- [ ] 与 STM32F103 联调
- [ ] 配对绑定与 OTA

## 关键参数（拟）

| 项目 | 值 |
| --- | --- |
| 设备名 | `ESP32-BLE` |
| 服务 UUID | `6E400001-B5A3-F393-E0A9-E50E24DCCA9E` |
| RX（手机→板子） | `6E400002-B5A3-F393-E0A9-E50E24DCCA9E`，Write |
| TX（板子→手机） | `6E400003-B5A3-F393-E0A9-E50E24DCCA9E`，Notify |
| UART | UART2，GPIO16(RX)/GPIO17(TX)，115200 8N1 |
