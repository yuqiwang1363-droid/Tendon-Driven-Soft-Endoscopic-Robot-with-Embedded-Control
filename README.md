# Tendon-Driven Soft Endoscopic Robot with Embedded Control

## Project Overview

This project presents the design and embedded control validation of a **tendon-driven soft endoscopic robot**
inspired by continuum and medical soft robotics systems.
The robot features a **2-DOF bending soft end-effector** capable of bending in both vertical (up/down)
and horizontal (left/right) directions, enabling steerable motion similar to endoscopic devices.

The primary focus of this project is **embedded control system design and experimental validation**
using a physical prototype fabricated via 3D printing.
System integration with the full soft robotic body and visual feedback was outside the scope of this phase.

---

## Motivation and Background

Medical endoscopic and catheter-based robotic systems often require:

- High flexibility and compliance for safe interaction with tissue
- Remote actuation to keep rigid components away from the patient
- Intuitive human–machine interfaces for precise maneuvering

Tendon-driven soft robotic mechanisms are widely adopted in medical robotics
due to their ability to transmit actuation forces from a remote location
while maintaining a compliant and compact distal end.

This project explores the **control feasibility and safety constraints**
of a tendon-driven soft robotic end-effector
as an early-stage prototype toward medical endoscopic applications.

---

## System Description

### Mechanical Structure

- **Tendon-driven soft end-effector** with two independent bending axes:
  - Vertical bending (up / down)
  - Horizontal bending (left / right)
- Tendons are actuated by **geared DC motors with encoders**
- Structural components were fabricated using **3D printing**
- Mechanical geometry limits the maximum bending angle to **±90° per axis**

---

### Embedded Control Hardware

- **Microcontroller:** Arduino Nano  
- **Motor Driver:** L298N dual H-bridge  
- **Actuators:** Encoder-equipped DC geared motors  
- **User Interface:**
  - Joystick for continuous 2-DOF bending control
  - Reset button for automatic return-to-home
  - Cleaning button to trigger a water spray for CMOS lens cleaning (system-level provision)

---

## Control Strategy

### Manual Bending Control

- Joystick inputs are mapped to **velocity-based motor commands**
- Velocity control was selected instead of direct position control
  to improve robustness against non-linear tendon–structure interactions
- A deadband is applied near the joystick center to prevent unintended motion

---

### Encoder Feedback and Safety Constraints

- Incremental encoders provide real-time displacement feedback
- Based on mechanical design analysis:
  - Maximum allowable bending angle: **±90°**
  - Corresponding encoder displacement: **±942 counts**
- **Software end-stops** are enforced at ±942 counts on both axes
  to prevent over-pulling and mechanical damage

---

### Return-to-Home Function

- A dedicated reset button triggers an automatic homing routine
- The controller drives both axes back toward zero displacement
  using encoder feedback
- Homing is terminated when both axes are within a small tolerance band
- A timeout mechanism is included for safety

---

## Experimental Validation

A **physical prototype** was fabricated using 3D printing techniques,
and the embedded control system was experimentally validated.

Validated aspects include:

- Real-time joystick-based 2-DOF bending control
- Encoder-based displacement feedback
- Software-enforced safety limits
- Reliable automatic return-to-home behavior
- CMOS cleaning actuation sequence (pump + servo)

**Note:**  
This validation focused on the **control subsystem and actuation feasibility**.
Integration with the full soft robotic body and closed-loop visual feedback
were intentionally excluded from this phase.

---

## My Contributions

This project was conducted at **UCR RAMS Lab** as a self-initiated research project.
I was fully responsible for the **embedded control subsystem**, including:

- Control logic design
- Circuit design and hardware integration
- Microcontroller programming (Arduino)
- Encoder feedback processing
- Safety constraint implementation
- Experimental testing and validation

---

## Limitations and Future Work

Current limitations include:

- No integration with the complete soft robotic body
- No closed-loop visual servoing using the CMOS camera
- No force or tactile feedback

Planned future extensions:

- Integration with the full soft robotic continuum body
- Closed-loop visual servoing using onboard CMOS imaging
- Model-based or learning-based bending control
- Miniaturization of actuation and control electronics

---

## Keywords

Soft robotics, medical robotics, tendon-driven mechanisms,
embedded control, continuum robots, mechatronics


# 基于牵拉驱动的软体内窥镜机器人及其嵌入式控制验证

## 项目简介

本项目设计并验证了一种**基于牵拉驱动（tendon-driven）的软体内窥镜机器人原型**，
该系统属于连续体机器人与医疗软体机器人（medical soft robotics）方向。
软体末端执行器具备 **二维弯曲自由度（2-DOF）**，
可在垂直方向（上 / 下）与水平方向（左 / 右）实现可控弯曲，
运动形式与内窥镜等医疗导管系统相似。

本项目的重点在于**嵌入式控制系统的设计与实体验证**。
通过 3D 打印制造物理原型，
完成了牵拉驱动机构与控制策略的可行性验证。
完整软体机器人本体与视觉闭环控制未纳入本阶段范围。

---

## 研究背景与动机

在医疗机器人领域，内窥镜、导管及介入式机器人系统通常需要满足以下要求：

- 高柔顺性与安全性，以避免对组织造成损伤  
- 驱动与控制单元远离患者，减少刚性结构暴露  
- 直观的人机交互方式，实现精确操控  

牵拉驱动的软体机器人结构能够将驱动力从近端传递至远端柔性执行器，
在保证末端柔顺性的同时实现有效控制，
因此被广泛应用于医疗连续体机器人系统中。

本项目以**控制可行性与安全性验证**为目标，
探索牵拉驱动软体末端执行器在内窥镜应用场景下的工程实现方式。

---

## 系统组成

### 机械结构设计

- **牵拉驱动软体末端执行器**
- 具备两个独立弯曲自由度：
  - 垂直方向弯曲（上 / 下）
  - 水平方向弯曲（左 / 右）
- 牵拉腱索由**带编码器的减速直流电机**驱动
- 结构件采用 **3D 打印** 制作
- 机械设计限制单轴最大弯曲角度为 **±90°**

---

### 嵌入式控制硬件

- **微控制器**：Arduino Nano  
- **电机驱动**：L298N 双 H 桥  
- **执行器**：带编码器的减速直流电机  
- **人机交互接口**：
  - 摇杆：实现连续二维弯曲控制  
  - 回位按钮：触发自动回零  
  - 清洁按钮：触发喷水动作，用于 CMOS 镜头清洁（系统级预留功能）

---

## 控制策略设计

### 人工操控与弯曲控制

- 摇杆输入映射为**速度控制指令**
- 相较于直接位置控制，速度控制在牵拉驱动系统中
  对非线性结构与摩擦变化具有更好的鲁棒性
- 在摇杆中立位置引入死区，避免误触发运动

---

### 编码器反馈与安全限制

- 使用增量式编码器获取实时位移信息
- 根据机械结构分析：
  - 单轴最大允许弯曲角度：**±90°**
  - 对应编码器位移：**±942 counts**
- 在控制程序中实现**软件限位（software end-stops）**，
  防止过度牵拉导致机构损坏

---

### 自动回位功能

- 回位按钮触发自动回零流程
- 控制系统基于编码器反馈驱动各轴向零位运动
- 当位移进入容差范围时停止运动
- 设置回位超时机制以保证系统安全

---

## 实体验证

本项目通过 **3D 打印原型** 完成了实体系统搭建，
并对嵌入式控制系统进行了实验验证。

已验证内容包括：

- 实时摇杆控制的二维弯曲运动  
- 编码器反馈下的位移感知  
- 软件限位对最大弯曲角度的约束  
- 自动回位功能的稳定性  
- CMOS 镜头清洁动作（喷水 + 舵机）的执行逻辑  

**说明：**  
本阶段验证主要集中于**牵拉驱动与控制子系统的可行性**，
未集成完整软体机器人本体及视觉闭环控制。

---

## 个人贡献说明

本项目在 **UCR RAMS Lab** 完成，为本人主动联系导师开展的研究型工程项目。
本人独立负责以下内容：

- 嵌入式控制系统整体设计  
- 电路设计与硬件集成  
- Arduino 程序开发  
- 编码器反馈处理  
- 安全约束与回位逻辑实现  
- 实体验证与调试  

---

## 局限性与未来工作

当前系统的主要局限包括：

- 尚未集成完整软体连续体机器人本体  
- 尚未实现基于 CMOS 的视觉闭环控制  
- 未引入力或触觉反馈  

未来可扩展方向包括：

- 完整软体内窥镜机器人系统集成  
- 基于 CMOS 图像的闭环视觉伺服控制  
- 建立弯曲角度与牵拉位移的模型  
- 引入模型驱动或学习型控制策略  
- 控制系统与执行机构的小型化设计  

---

## 关键词

软体机器人，医疗机器人，牵拉驱动，
连续体机器人，嵌入式控制，机电一体化
