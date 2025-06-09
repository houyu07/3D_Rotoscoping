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

