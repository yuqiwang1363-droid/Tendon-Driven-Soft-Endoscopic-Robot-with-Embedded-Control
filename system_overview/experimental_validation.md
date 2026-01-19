# Experimental Validation

This document describes the experimental validation performed for the tendon-driven soft endoscopic robot project. The validation focuses on the embedded control system and actuation feasibility using a physical prototype.

The purpose of this stage is to verify control logic, safety constraints, and human-in-the-loop operability, rather than full system integration or clinical-level performance.

---

## 1. Validation Objectives

The primary objectives of the experimental validation are:

- Verify embedded motor control functionality
- Validate encoder-based position monitoring
- Confirm software-enforced safety limits
- Evaluate joystick-based human-in-the-loop control
- Assess repeatability of reset and homing behavior

These objectives are aligned with early-stage prototyping goals for medical and soft robotic systems.

---

## 2. Experimental Setup

A physical prototype was constructed using 3D-printed components to support experimental validation of the control subsystem.

The experimental setup included:

- Arduino Nano as the embedded controller
- DC gear motors with incremental encoders
- L298N motor driver
- Analog joystick for user input
- Push buttons for reset and auxiliary functions
- External power supply for motor actuation

The soft robotic end-effector structure and CMOS vision system were not fully integrated at this stage.
## Physical Prototype and Control Validation

![Physical Prototype](./physical_prototype.jpg)

A physical prototype of the embedded control handle and actuation unit was fabricated
using 3D-printed components and off-the-shelf electronics.

Due to limited availability of Arduino Nano boards during testing, an Arduino Uno was
used as a temporary substitute. The final design fully supports integration of an Arduino Nano
within the enclosure as originally intended.

Joystick-based control, encoder feedback, homing, and safety limit enforcement were
successfully validated on the physical prototype.

---

## 3. Validation Procedures

The following procedures were performed during experimental validation:

### 3.1 Manual Bending Control Test

- Joystick inputs were applied in both vertical and horizontal directions
- Motor response and direction mapping were observed
- Smoothness and responsiveness of bending commands were evaluated

### 3.2 Encoder Feedback Verification

- Encoder counts were monitored during bidirectional motor motion
- Direction consistency between encoder signals and motor commands was confirmed
- Encoder-based position tracking was validated under repeated motion cycles

### 3.3 Safety Limit Enforcement Test

- Motors were driven toward predefined angular limits
- Controller behavior at ±90° boundaries was observed
- Motion blocking beyond safety limits was verified
- Recovery motion back toward the safe region was confirmed

### 3.4 Reset and Homing Test

- Reset button was triggered from multiple bent configurations
- System response during homing motion was observed
- Encoder counters were reinitialized after reaching the neutral position
- Repeatability across multiple reset cycles was verified

---

## 4. Validation Results

Experimental validation demonstrated that:

- Embedded motor control operated reliably under joystick input
- Encoder feedback provided stable and repeatable position information
- Software safety limits effectively prevented over-bending
- Reset and homing behavior consistently restored a known reference state
- Human-in-the-loop operation was intuitive and predictable

No uncontrolled motion or mechanical overload was observed during testing.

---

## 5. Scope and Limitations

The validation scope of this project is intentionally limited to the embedded control and actuation subsystems.

The following aspects were **not** validated at this stage:

- Full integration of the soft robotic body
- Vision-based feedback using a CMOS camera
- Force or tension sensing on tendons
- Closed-loop curvature or position control

These limitations reflect the staged development approach adopted in this project.

---

## 6. Discussion

The experimental results confirm that encoder-based safety constraints and embedded control logic provide a reliable foundation for tendon-driven soft robotic systems.

By validating the control subsystem independently, the project reduces system integration risk and establishes a robust baseline for future extensions.

---

## 7. Future Validation Directions

Future experimental work may include:

- Integration with the complete soft robotic structure
- Vision-assisted closed-loop control
- Force or tension feedback for enhanced safety
- Testing under representative loading conditions

---

# 实验验证（中文）

本文档介绍了牵拉驱动软体内窥镜机器人项目的实验验证内容。本阶段验证重点放在**嵌入式控制系统与执行机构的可行性**，而非完整系统集成或临床级性能。

---

## 1. 验证目标

本阶段实验验证的主要目标包括：

- 验证嵌入式电机控制功能
- 验证基于编码器的位置监测
- 确认软件安全限位的有效性
- 评估基于摇杆的人机交互控制方式
- 验证回零与复位功能的可重复性

上述目标符合医疗软体机器人早期原型验证阶段的工程需求。

---

## 2. 实验平台搭建

实验验证基于 3D 打印构建的实体原型完成，主要实验平台包括：

- Arduino Nano 嵌入式控制器
- 带增量式编码器的直流减速电机
- L298N 电机驱动模块
- 模拟摇杆作为输入接口
- 回零及辅助功能按键
- 外接电源为电机供电

本阶段未集成完整软体末端执行器结构与 CMOS 视觉系统。

---

## 3. 实验流程

实验验证主要包括以下步骤：

### 3.1 手动弯曲控制测试

- 通过摇杆输入控制上下与左右方向弯曲
- 观察电机响应与方向映射关系
- 评估控制过程的平滑性与可控性

### 3.2 编码器反馈验证

- 在双向运动过程中监测编码器计数变化
- 验证编码器方向与电机运动方向的一致性
- 测试多次往复运动下的位置跟踪稳定性

### 3.3 安全限位验证

- 驱动电机向预设弯曲极限运动
- 观察系统在 ±90° 处的控制行为
- 验证超过限位后系统阻止继续驱动
- 确认系统允许向安全区域方向回退

### 3.4 回零与复位测试

- 在不同弯曲状态下触发回零按钮
- 观察系统回零过程与运动方向
- 回零完成后重置编码器计数
- 验证多次回零操作的一致性

---

## 4. 实验结果

实验结果表明：

- 嵌入式电机控制运行稳定
- 编码器反馈提供了可靠的位置监测
- 软件安全限位有效防止了过度弯曲
- 回零功能可重复地恢复系统参考状态
- 人机交互控制方式直观且可预测

实验过程中未观察到异常运动或结构损坏。

---

## 5. 验证范围与局限性

本阶段实验验证范围主要集中于**控制与执行子系统**。

以下内容未在本阶段验证：

- 完整软体机器人结构集成
- 基于 CMOS 摄像头的视觉反馈
- 牵拉绳索的力或张力传感
- 闭环曲率或位置控制算法

上述限制反映了项目采用的分阶段开发策略。

---

## 6. 讨论

实验结果表明，基于编码器的安全约束与嵌入式控制逻辑能够为牵拉驱动软体机器人系统提供可靠的基础。

通过先行验证控制子系统，可有效降低后续系统集成风险。

---

## 7. 后续验证方向

后续实验工作可包括：

- 集成完整软体末端执行器结构
- 引入视觉反馈实现闭环控制
- 增加力或张力反馈以提升安全性
- 在代表性载荷条件下进行测试
