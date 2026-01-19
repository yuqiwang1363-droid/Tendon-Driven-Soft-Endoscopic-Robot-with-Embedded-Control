# Encoder Feedback and Safety Constraints

This document describes the encoder-based feedback mechanism and software safety constraints implemented in the embedded control system of the tendon-driven soft endoscopic robot.

The focus is on practical safety enforcement and control reliability rather than high-precision motion control.

---

## 1. Role of Encoders in the System

Incremental rotary encoders are mounted on each DC gear motor to provide relative position feedback for the tendon-driven bending mechanism.

The encoders are used to:

- Estimate relative motor rotation
- Infer bending direction and magnitude
- Enforce software-based angular limits
- Prevent mechanical over-bending of the soft structure

The encoder feedback is not used for closed-loop trajectory tracking, but rather for safety monitoring and motion limiting.

---

## 2. Encoder Signal Processing

Each encoder provides quadrature signals (A/B channels), which are decoded in software to track incremental position changes.

Key characteristics of the implementation:

- Relative position tracking (no absolute reference)
- Position reset during homing operation
- Encoder counts mapped to motor rotation direction
- Separate counters maintained for each bending axis

The system assumes a known mechanical transmission ratio between motor rotation and tendon displacement.

---

## 3. Bending Angle Estimation

Motor encoder counts are mapped to an estimated bending angle using a calibrated conversion factor.

This estimated angle is used only for enforcing safety limits, not for precise geometric reconstruction of the soft body.

The maximum allowable bending angle for each axis is limited to:

- +90 degrees (clockwise / positive direction)
- −90 degrees (counterclockwise / negative direction)

These limits were chosen conservatively to protect the soft structure and tendon routing.

---

## 4. Software Safety Constraints

Software safety constraints are implemented directly in the embedded control logic.

The safety logic includes:

- Blocking motor commands that exceed angular limits
- Allowing motion only if the commanded direction reduces the absolute bending angle
- Immediate motor stop when a limit is reached
- Reset and homing override through a dedicated button

These constraints operate independently for the vertical and horizontal bending axes.
### Software-Enforced Angular Limits

To prevent mechanical over-bending and tendon over-tension,
software safety limits are enforced on each bending axis.

- Maximum bending angle: ±90°
- Limits implemented in encoder count space
- Motor commands are saturated once limits are reached

The following video demonstrates the system reaching the angular limit
and safely rejecting further joystick input in that direction.

**Demonstration Video:**
- `media/safety_limit_demo.mp4`

---

## 5. Homing and Reset Strategy

A reset button is implemented to return the system to a neutral configuration.

During reset:

- Motor commands are driven toward zero encoder count
- Encoder counters are re-initialized
- Safety limits are temporarily relaxed to allow return motion only

This strategy enables safe recovery from unexpected states without requiring absolute position sensors.

---

## 6. Safety-Oriented Design Philosophy

Due to the nature of soft robotic systems and medical-style devices, the control design prioritizes:

- Mechanical safety
- Predictable behavior
- Robustness to user input
- Prevention of irreversible deformation

As a result, conservative software limits are preferred over aggressive control strategies.

---

## 7. Limitations and Future Improvements

Current limitations include:

- Encoder-based relative position only (no absolute bending measurement)
- No force or tension feedback on tendons
- Open-loop motor command within safety bounds

Future improvements may include:

- Integration of force or tension sensors
- Closed-loop position control with PID
- Adaptive safety limits based on material response

---

# 编码器反馈与安全约束（中文）

本文档介绍了牵拉驱动软体内窥镜机器人中基于编码器的反馈机制及软件安全约束设计。

重点在于**安全控制与系统可靠性**，而非高精度运动控制。

---

## 1. 编码器在系统中的作用

每个直流减速电机均配备增量式旋转编码器，用于获取电机相对转动信息。

编码器主要用于：

- 估计电机相对旋转角度
- 判断弯曲方向与幅度
- 实现软件层面的角度限制
- 防止软体结构发生过度弯曲

编码器反馈并未用于精确轨迹跟踪，而是作为安全监测手段。

---

## 2. 编码器信号处理方式

编码器输出为 A/B 相正交信号，通过软件解码获取增量位置变化。

实现特点包括：

- 仅进行相对位置跟踪
- 在回零操作中重置编码器计数
- 根据编码器方向判断电机转向
- 两个弯曲自由度分别维护独立计数器

系统假设电机旋转与牵拉位移之间的机械传动比为已知常量。

---

## 3. 弯曲角度估计

编码器计数通过标定系数转换为估计弯曲角度。

该角度估计仅用于安全限制判断，并不用于软体几何形态的精确重建。

每个弯曲方向的最大允许角度限制为：

- 正方向：+90°
- 负方向：−90°

该限制基于结构安全性进行保守设定。

---

## 4. 软件安全约束机制

安全约束直接嵌入在控制程序中，包括：

- 超出角度限制时禁止继续驱动
- 仅允许向“减小弯曲角度”的方向运动
- 达到极限角度时立即停止电机
- 通过独立按钮执行系统回零

上下弯与左右弯两个自由度独立执行安全判断。

---

## 5. 回零与复位策略

系统设置了专用回零按钮，用于将系统恢复至中性位置。

回零过程中：

- 电机朝编码器零点方向运动
- 编码器计数被重新初始化
- 安全限制仅允许回退方向运动

该策略避免了对绝对位置传感器的依赖。

---

## 6. 面向安全的设计理念

考虑到软体机器人及医疗设备的特性，本系统控制设计强调：

- 结构安全
- 行为可预测性
- 对用户输入的鲁棒性
- 防止不可逆形变

因此采用保守的软件限位策略，而非激进控制方法。

---

## 7. 局限性与改进方向

当前系统的局限性包括：

- 仅使用相对编码器位置
- 未引入牵拉力或张力反馈
- 在安全范围内仍为开环控制

未来可考虑：

- 增加张力或力传感器
- 引入 PID 闭环控制
- 基于材料响应的自适应安全限制
