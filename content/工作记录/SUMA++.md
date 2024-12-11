---
title: "SLAM-SUMA++"
date: 2024-12-11
draft: false
---

# 问题

1. tensorRT解析ONNX超时

(1) 问题输出

```bash
WARNING: ONNX model has a newer ir_version (0.0.4) than this parser was built against (0.0.3).
 ----- Parsing of ONNX model src/rangenet_lib/model/darknet53//model.onnx is Done ---- 
Success picking up ONNX model
Failure creating engine from ONNX model
Current trial size is 8589934592
Failure creating engine from ONNX model
Current trial size is 4294967296
Failure creating engine from ONNX model
Current trial size is 2147483648
Failure creating engine from ONNX model
Current trial size is 1073741824
Failure creating engine from ONNX model
Current trial size is 536870912
Failure creating engine from ONNX model
Current trial size is 268435456
Failure creating engine from ONNX model
Current trial size is 134217728
Failure creating engine from ONNX model
Current trial size is 67108864
Failure creating engine from ONNX model
Current trial size is 33554432
Failure creating engine from ONNX model
Current trial size is 16777216
Failure creating engine from ONNX model
Current trial size is 8388608
Failure creating engine from ONNX model
Current trial size is 4194304
Failure creating engine from ONNX model
Current trial size is 2097152
Failure creating engine from ONNX model
Current trial size is 1048576
terminate called after throwing an instance of 'std::runtime_error'
  what():  ERROR: could not create engine from ONNX.
Aborted (core dumped)
```

(2) 问题详细链接：<https://github.com/PRBonn/rangenet_lib/issues/15>

(3) 解决方案：

程序的dockerfile中默认的镜像以及默认的对应版本的驱动和模型

```bash
FROM nvcr.io/nvidia/tensorrt:19.08-py3 #CUDA 10.1.243, cuDNN 7.6.2, TensorRT 5.1.5
```

我的显卡是4060Ti，与 TensorRT 5.1.5不兼容

修改镜像以及对应驱动和模型为

```bash
FROM nvcr.io/nvidia/tensorrt:21.11-py3 #CUDA 11.3、cuDNN 8.2.1 和 TensorRT 8.2.1
```

# 测试
