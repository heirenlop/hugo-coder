---
title: "LIO-SAM"
date: 2024-12-12
draft: false
---

# 一. 程序

源码：<https://github.com/TixiaoShan/LIO-SAM/tree/master?tab=readme-ov-file#sample-datasets>

分支：ros2

# 二. 流程

1. 官方的bag分多种，目前我只下载了campus和park,根据运行的bag不同，做如下配置文件的修改

(1) 默认配置

config/params.yaml内容保持默认

```yaml
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
imuTopic: "/imu_correct"                        # IMU data
extrinsicRot:    [1.0,  0.0,  0.0,
                       0.0,  1.0,  0.0,
                       0.0,  0.0, 1.0 ]
extrinsicRPY: [ 1.0,  0.0,  0.0,
                   0.0,  1.0,  0.0,
                    0.0,  0.0,  1.0 ]
```

# 三. 问题

官方只有ros1的bag，测试ros2需要自己转换，测试了如下两仓的转换效果

**(1) rosbags**

安装并测试：
```bash
apt-get update
apt-get install python3-pip
pip install rosbags
rosbags-convert --src <path_to_rosbag1_filename> --dst <path_to_ros2bag_filename> #转换bag
```
结果：rosbags转bag后，imu频率从500hz降到250hz，不可用。

**(2) ros1_bridge**

安装并测试：写了一个docker镜像，参考： <https://github.com/heirenlop/ros1_bridge_docker>。

结果：无降频问题，可用。

# 四. 测试

可复现