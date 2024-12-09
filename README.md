该项目的目标是使用U-Net模型，创建一个图像分割工具，用于从输入的三维场景图像中提取形状、背景和4种不同的色调值。该项目旨在解决动画领域中的自动抠像问题，通过将3D视觉内容转化为2D表现形式。

以下是一个示例输出：

[示例图像](Examples/example_Shape6_input.gif "示例")
[示例图像](Examples/example_Shape6_output.gif "示例")

为了训练模型，这里使用Cinema4D的多通道渲染器创建了一个定制的数据集，包含已分割的图像。

如果想要自己测试，可以将待测试的图像放到`./data/test_images`目录中。

## 文件结构
- `./UnprocessedImages`：包含所有从Cinema4D多通道渲染器导出的原始图像。
- `./ProcessedImages`：包含所有经过`pixel_processing.py`处理后的编辑图像。
- `./data`：包含测试用的图像和部分训练图像。
- `./Eaxmples`：包含几个输入和输出的gif示例。
- `./weights`：包含训练生成的权重。
- `compression.py`：包含帮助裁剪和调整大小的函数。
- `unet.py`：包含U-Net模型以及训练循环和预测功能,并将结果转换成gif图片。
- `segmentation_dataset.py`：包含用于训练和加载图像的类。
- `pixel_processing.py`：包含所有的预处理函数，可以应用于从Cinema4D输出的多通道图层。
- `compression.py`：包含帮助裁剪和调整大小的函数。
- `util.py`：包含其他实用功能，如文件组织以及将帧重新拼接成GIF。

## 依赖库
- pytorch
- torchvision
- pillow
- numpy
- matplotlib

## 运行方式

在组织好文件后，运行`unet.py`文件。

如果需要重新训练，选择“y”。由于我没有上传数据集到国科大系统，所以这一步暂时无法实现，可以在我的github上下载包含数据集的完整项目。

如果需要直接使用已经训练好的模型进行测试，选择“n”，并选择你希望加载的训练模型的epoch（推荐输入40，输入范围0~49）。接下来，程序会自动加载模型并使用`./data/test_images`文件夹中的图像进行处理。模型推理后的输出将保存在`./data/test_results`文件夹中，合成的gif图片将直接保存在`./data/output_result.gif`。如果你想试试其他输入图像，可以在`./data/images`中选择一个文件夹中的全部图片放入`./data/test_images`中再次测试，之前`./data/test_results`中生成的结果将自动删除，无需自己操作。


如果只想看看模型效果，请查看`Examples`文件夹中的几个示例


## 训练过程

PS D:\project\3D_Rotoscoping> & D:/Software/anaconda/envs/pytorch/python.exe d:/project/3D_Rotoscoping/unet.py
Using device: cuda
Do you want to train the model? (y/n): y
Training on  23  batches for  50  epochs
Training started

Epoch 1/50 started at 02:04:17
Epoch 1 finished. Train Loss: 1.2062, Val Loss: 1.3058 at 02:10:51 (Took 393.66 seconds to run)

Epoch 2/50 started at 02:04:17
Epoch 1 finished. Train Loss: 1.0031, Val Loss: 1.0656 at 02:17:54 (Took 423.36 seconds to run)

Epoch 3/50 started at 02:18:02
Epoch 3 finished. Train Loss: 0.7436, Val Loss: 0.6610 at 02:25:20 (Took 438.29 seconds to run)

Epoch 4/50 started at 02:25:20
Epoch 4 finished. Train Loss: 0.6732, Val Loss: 0.6195 at 02:32:42 (Took 441.24 seconds to run)

Epoch 5/50 started at 02:32:42
Epoch 5 finished. Train Loss: 0.6202, Val Loss: 0.5768 at 02:40:10 (Took 447.91 seconds to run)

Epoch 6/50 started at 02:40:10
Epoch 6 finished. Train Loss: 0.5763, Val Loss: 0.5431 at 02:47:49 (Took 459.00 seconds to run)

Epoch 7/50 started at 02:47:50
Epoch 7 finished. Train Loss: 0.5342, Val Loss: 0.4976 at 02:55:30 (Took 460.38 seconds to run)

Epoch 8/50 started at 02:55:31
Epoch 8 finished. Train Loss: 0.4944, Val Loss: 0.4586 at 03:03:03 (Took 452.69 seconds to run)

Epoch 9/50 started at 03:03:04
Epoch 9 finished. Train Loss: 0.4662, Val Loss: 0.4916 at 03:10:46 (Took 462.30 seconds to run)

Epoch 10/50 started at 03:10:47
Epoch 10 finished. Train Loss: 0.4394, Val Loss: 0.4188 at 03:18:36 (Took 469.14 seconds to run)

Epoch 11/50 started at 03:18:36
Epoch 11 finished. Train Loss: 0.4073, Val Loss: 0.3892 at 03:26:19 (Took 462.96 seconds to run)

Epoch 12/50 started at 03:26:20
Epoch 12 finished. Train Loss: 0.3794, Val Loss: 0.3549 at 03:34:09 (Took 469.03 seconds to run)

Epoch 13/50 started at 03:34:09
Epoch 13 finished. Train Loss: 0.3538, Val Loss: 0.3471 at 03:42:00 (Took 470.99 seconds to run)

Epoch 14/50 started at 03:42:01
Epoch 14 finished. Train Loss: 0.3327, Val Loss: 0.3257 at 03:49:35 (Took 454.15 seconds to run)

Epoch 15/50 started at 03:49:35
Epoch 15 finished. Train Loss: 0.3149, Val Loss: 0.3046 at 03:57:09 (Took 454.05 seconds to run)

Epoch 16/50 started at 03:57:10
Epoch 16 finished. Train Loss: 0.2920, Val Loss: 0.2967 at 04:04:41 (Took 450.78 seconds to run)

Epoch 17/50 started at 04:04:41
Epoch 17 finished. Train Loss: 0.2746, Val Loss: 0.2608 at 04:12:05 (Took 444.14 seconds to run)

Epoch 18/50 started at 04:12:06
Epoch 18 finished. Train Loss: 0.2573, Val Loss: 0.2459 at 04:19:36 (Took 450.40 seconds to run)

Epoch 19/50 started at 04:19:36
Epoch 19 finished. Train Loss: 0.2441, Val Loss: 0.2416 at 04:27:07 (Took 450.46 seconds to run)

Epoch 20/50 started at 04:27:07
Epoch 20 finished. Train Loss: 0.2286, Val Loss: 0.2182 at 04:34:31 (Took 444.07 seconds to run)

Epoch 21/50 started at 04:34:32
Epoch 21 finished. Train Loss: 0.2161, Val Loss: 0.2129 at 04:42:03 (Took 450.53 seconds to run)

Epoch 22/50 started at 04:42:03
Epoch 22 finished. Train Loss: 0.2022, Val Loss: 0.1909 at 04:49:33 (Took 450.06 seconds to run)

Epoch 23/50 started at 04:49:34
Epoch 23 finished. Train Loss: 0.1923, Val Loss: 0.1865 at 04:56:59 (Took 445.26 seconds to run)

Epoch 24/50 started at 04:56:59
Epoch 24 finished. Train Loss: 0.1832, Val Loss: 0.1752 at 05:04:31 (Took 451.71 seconds to run)

Epoch 25/50 started at 05:04:32
Epoch 25 finished. Train Loss: 0.1725, Val Loss: 0.1633 at 05:12:02 (Took 450.22 seconds to run)

Epoch 26/50 started at 05:12:02
Epoch 26 finished. Train Loss: 0.1653, Val Loss: 0.1536 at 05:19:27 (Took 444.17 seconds to run)

Epoch 27/50 started at 05:19:27
Epoch 27 finished. Train Loss: 0.1550, Val Loss: 0.1501 at 05:26:58 (Took 450.62 seconds to run)

Epoch 28/50 started at 05:26:58
Epoch 28 finished. Train Loss: 0.1488, Val Loss: 0.1427 at 05:34:29 (Took 451.11 seconds to run)

Epoch 29/50 started at 05:34:30
Epoch 29 finished. Train Loss: 0.1427, Val Loss: 0.1385 at 05:41:54 (Took 444.28 seconds to run)

Epoch 30/50 started at 05:41:54
Epoch 30 finished. Train Loss: 0.1377, Val Loss: 0.1315 at 05:49:25 (Took 450.64 seconds to run)

Epoch 31/50 started at 05:49:25
Epoch 31 finished. Train Loss: 0.1302, Val Loss: 0.1275 at 05:56:56 (Took 450.17 seconds to run)

Epoch 32/50 started at 05:56:56
Epoch 32 finished. Train Loss: 0.1415, Val Loss: 0.1520 at 06:04:20 (Took 444.24 seconds to run)

Epoch 33/50 started at 06:04:21
Epoch 33 finished. Train Loss: 0.1328, Val Loss: 0.1236 at 06:11:51 (Took 450.65 seconds to run)

Epoch 34/50 started at 06:11:52
Epoch 34 finished. Train Loss: 0.1217, Val Loss: 0.1151 at 06:19:22 (Took 450.17 seconds to run)

Epoch 35/50 started at 06:19:22
Epoch 35 finished. Train Loss: 0.1154, Val Loss: 0.1090 at 06:26:47 (Took 444.11 seconds to run)

Epoch 36/50 started at 06:26:47
Epoch 36 finished. Train Loss: 0.1096, Val Loss: 0.1070 at 06:34:18 (Took 451.27 seconds to run)

Epoch 37/50 started at 06:34:19
Epoch 37 finished. Train Loss: 0.1054, Val Loss: 0.1018 at 06:41:49 (Took 450.20 seconds to run)

Epoch 38/50 started at 06:41:49
Epoch 38 finished. Train Loss: 0.1015, Val Loss: 0.0974 at 06:49:14 (Took 445.09 seconds to run)

Epoch 39/50 started at 06:49:15
Epoch 39 finished. Train Loss: 0.0975, Val Loss: 0.0934 at 06:56:46 (Took 451.45 seconds to run)

Epoch 40/50 started at 06:56:47
Epoch 40 finished. Train Loss: 0.0942, Val Loss: 0.0962 at 07:04:17 (Took 450.23 seconds to run)

Epoch 41/50 started at 07:04:18
Epoch 41 finished. Train Loss: 0.0918, Val Loss: 0.0898 at 07:11:42 (Took 444.14 seconds to run)

Epoch 42/50 started at 07:11:42
Epoch 42 finished. Train Loss: 0.0889, Val Loss: 0.0842 at 07:19:13 (Took 450.74 seconds to run)

Epoch 43/50 started at 07:19:13
Epoch 43 finished. Train Loss: 0.0868, Val Loss: 0.0856 at 07:26:44 (Took 450.13 seconds to run)

Epoch 44/50 started at 07:26:44
Epoch 44 finished. Train Loss: 0.0839, Val Loss: 0.0810 at 07:34:08 (Took 444.14 seconds to run)

Epoch 45/50 started at 07:34:09
Epoch 45 finished. Train Loss: 0.0820, Val Loss: 0.0782 at 07:41:40 (Took 451.38 seconds to run)

Epoch 46/50 started at 07:41:40
Epoch 46 finished. Train Loss: 0.0784, Val Loss: 0.0750 at 07:49:12 (Took 451.38 seconds to run)

Epoch 47/50 started at 07:49:12
Epoch 47 finished. Train Loss: 0.0772, Val Loss: 0.0789 at 07:56:37 (Took 444.27 seconds to run)

Epoch 48/50 started at 07:56:37
Epoch 48 finished. Train Loss: 0.0745, Val Loss: 0.0726 at 08:04:08 (Took 450.64 seconds to run)

Epoch 49/50 started at 08:04:08
Epoch 49 finished. Train Loss: 0.0718, Val Loss: 0.0726 at 08:11:38 (Took 450.09 seconds to run)

Epoch 50/50 started at 08:11:39
Epoch 50 finished. Train Loss: 0.0704, Val Loss: 0.0704 at 08:19:03 (Took 444.17 seconds to run)
Training complete
Average time taken per epoch:  449.13 seconds
