# mpc_ctrl_based_opt 项目介绍

## 项目概述
`mpc_ctrl_based_opt` 是一个基于模型预测控制（MPC）的优化控制项目，主要面向无人机等移动设备的控制与导航场景。项目基于ROS（机器人操作系统）开发，集成了控制算法实现、可视化工具、位姿处理及消息定义等功能模块，提供了从算法到可视化的完整解决方案。

## 核心功能模块

### 1. 控制核心模块
- **mpc_ctrl**：项目核心功能包，实现模型预测控制相关算法
  - 包含 `JPCM_node` 主节点，负责控制逻辑执行
  - 集成 GTSAM 库进行状态估计与优化（包含因子定义、边缘化等模块）
  - 提供 `FakeGPS_IMU_fusion_node` 用于传感器数据融合测试
  - 支持轨迹测试脚本（{insert\_element\_1\_YGZpeGVkX3BvaW50X2FuZF9jaXJjbGVfdGVzdC5weWA=}）

### 2. 工具类模块
- **cmake_utils**：提供CMake工具函数，避免多包重复编写配置文件，简化构建流程
  - 依赖 `catkin`、`roscpp` 和 `cmake_modules`
  - 采用 LGPLv3 许可证

- **uav_utils**：无人机常用工具函数集合
  - 包含导航、状态处理等通用功能
  - 提供单元测试支持（基于gtest）
  - 采用 LGPLv3 许可证

- **pose_utils**：位姿处理工具函数库
  - 提供位姿转换、计算等基础功能
  - 支持 ROS 环境下的位姿数据交互
  - 维护者：Shaojie Shen、william.wu
  - 采用 LGPLv3 许可证

### 3. 可视化与交互模块
- **rviz_plugins**：RViz 可视化插件包
  - 提供 `Goal3DTool` 工具，支持通过RViz界面交互设置无人机目标位姿
  - 发布 `geometry_msgs/PoseStamped` 和 `quadrotor_msgs/GoalSet` 消息
  - 支持3D空间中的位置、姿态和高度设置，通过箭头可视化目标位姿
  - 采用 LGPLv3 许可证

### 4. 分解与消息模块
- **decomp_ros_msgs**：分解相关的ROS消息定义
- **decomp_ros_utils**：分解相关的ROS工具函数
  - 两者均采用 BSD 3-Clause 许可证（版权所有者：sikang）

- **quadrotor_msgs**：四旋翼无人机专用消息定义
  - 包含 `GoalSet` 等目标设置相关消息类型
  - 采用 BSD 许可证

## 技术依赖
- 操作系统：Linux（兼容ROS支持的发行版）
- 核心框架：ROS（支持Indigo等版本）
- 构建系统：catkin
- 主要库依赖：
  - Eigen3：矩阵运算
  - GTSAM：状态估计与优化
  - OGRE：3D渲染（用于可视化插件）
  - YAML-CPP：配置文件处理
  - gtest：单元测试

## 编译与使用
1. 将仓库克隆到ROS工作空间的`src`目录
   ```bash
   cd ~/catkin_ws/src
   git clone <仓库地址>
   
## 编译工作空间
1. 将仓库克隆到ROS工作空间的`src`目录
   ```bash
   cd ~/catkin_ws
   catkin_make
   source devel/setup.bash

## 运行核心功能(仿真)
1. 启动您的px4仿真
   ```bash
   roslaunch px4 indoor1.launch
2. 启动控制器
   ```bash
   roslaunch mpc_ctrl run_ctrl.launch
3. 启动轨迹生成器
   ```bash
   roslaunch mpc_ctrl pub_cmd.launch
3. mpc控制效果可视化脚本
   ```bash
   python3 ~/catkin_ws/src/your_pkg/mpc_ctrl/scripts/controller_vis.py  # 轨迹跟踪结果分析可视化
   python3 ~/catkin_ws/src/your_pkg/mpc_ctrl/scripts/opt_vis.py # 优化结果分析可视化
