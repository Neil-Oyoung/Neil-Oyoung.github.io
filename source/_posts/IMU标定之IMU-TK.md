---
title: IMU标定之IMU-TK
date: 2018-10-26 20:53:04
tags: [imu_tk, IMU标定]
---

# IMU标定之IMU-TK

使用IMU前往往需要标定其内在参数，如尺度因子，轴安转误差和零偏，[imu_tk](https://bitbucket.org/alberto_pretto/imu_tk)是其中一款标定工具。

为了方便ROS用户，我个人为它加了简单的ROS封装，代码见`https://github.com/Neil-Oyoung/imu_tk`。