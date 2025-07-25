# Electricity-Theft-Detection-and-Localization

## 项目简介

本项目设计了一套基于 STM32 的电能数据采集与窃电检测定位系统，具备数据采集、远程上报、云端分析与移动端展示等功能。系统可用于配电网末端节点的电能监测与异常行为识别，具备良好的可部署性和扩展性。

---

## 技术实现

### 1. 硬件设计
- 使用嘉立创 EDA 专业版绘制 STM32 + RN8302B 电能采集装置的原理图及 PCB；
- 完成打板、焊接、调试，确保采集电路精度与稳定性。

### 2. 嵌入式软件开发
- KEIL 环境下采用 C 语言编程， 基于 FreeRTOS 实现多任务调度；
- 实现 RN8302B 与 STM32 的 SPI 通信，采集电流、电压、频率等数据；
- 驱动 BC20 模块，通过 AT 指令进行 NB-IoT 激活、注册和联网；
- 使用 MQTT 协议将采集数据上报至云端服务器，并接收移动端下发的控制指令。

### 3. 云服务器部署
- 在京东云部署 EMQX 服务器和 MySQL 数据库；
- 实现数据转发、存储，支撑移动端查询与远程控制功能。

### 4. 窃电检测算法开发
- 使用 Python 实现基于互相关的拓扑重构算法；
- 构建 LSTM 神经网络模型判断主子节点电能守恒关系；
- 检测结果存入 MySQL，供前端系统调用。

---

## 项目结构与功能模块

### 1. 采集端
- **主控芯片：** STM32F103C8T6
- **电能采集芯片：** RN8302B，SPI 通信
- **通信模块：** Quectel BC20（NB-IoT），通过串口发送 AT 指令
- **数据采集类型：** 电压、电流、频率
- **硬件设计文件：** Electricity-Theft-Detection-and-Localization.eprj（嘉立创EDA专业版）

### 2. 云服务器端
- **平台：** 京东云
- **组件部署：**
  - EMQX：处理 MQTT 消息收发
  - MySQL：存储历史数据与窃电检测结果
  - Python：运行互相关 + LSTM 窃电检测算法
- **后台管理系统：** 实现用户授权、设备管理与数据可视化（配合小程序使用）

### 3. 移动端（微信小程序）
- 采集设备安装与管理（扫码 + 地图定位）
- 设备远程控制（控制报警器）
- 电能数据可视化查询
- 窃电检测结果展示

---

## 项目成果

- 实测采集精度误差小于 1%；
- 成功检测出异常用户约 50 户；
- 挽回经济损失超 5 万元。
