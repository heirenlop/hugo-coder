---
title: "SLAM-LIO-SAM"
date: 2024-12-12
draft: false
---

# 一. 程序

源码：<https://github.com/TixiaoShan/LIO-SAM/tree/master?tab=readme-ov-file#sample-datasets>

分支：branch：ros2

# 二. 问题


# 三. 测试

1. 官方的bag分多种，目前我只下载了前两种,根据运行的bag不同，做如下配置文件的修改
(1) 默认配置
config/params.yaml内容保持默认

```yaml
pointCloudTopic: "points_raw"               # Point cloud data
imuTopic: "imu_raw"                         # IMU data
extrinsicRot:    [-1.0,  0.0,  0.0,
                       0.0,  1.0,  0.0,
                        0.0,  0.0, -1.0 ]
extrinsicRPY: [ 0.0,  1.0,  0.0,
                    -1.0,  0.0,  0.0,
                     0.0,  0.0,  1.0 ]
```

(2) 修改配置
config/params.yaml内容修改如下：

```yaml
pointCloudTopic: "/points_raw"                   # Point cloud data
imuTopic: "/imu_correct"                        # IMU data
extrinsicRot:    [1.0,  0.0,  0.0,
                       0.0,  1.0,  0.0,
                       0.0,  0.0, 1.0 ]
extrinsicRPY: [ 1.0,  0.0,  0.0,
                   0.0,  1.0,  0.0,
                    0.0,  0.0,  1.0 ]
```
