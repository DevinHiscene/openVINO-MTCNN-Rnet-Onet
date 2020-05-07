## Brief
基于openVINO + MTCNN  
本代码实现了在模拟Pnet输出的情况下,正常运行Rnet & Onet  
PS: [openVINO-git](https://github.com/openvinotoolkit/dldt)

## Prepare
* 将**openVINO**中的inference-engine/samples/hello_classification/main.cpp替换为README同级文件夹下的main.cpp
* 增加opencv依赖(用于作图,显示):core highgui imgproc
* det2对应MTCNN-Rnet, det3对应MTCNN-Onet
* piclist.txt需要测试的图片列表
* 模拟Pnet输入,请修改 line 173, main.cpp
* 修改Rnet阈值,请修改 line 103, main.cpp
* 修改Onet阈值,请修改 line 108, main.cpp

## How to run?
```
./hello_classification model/mtcnn/det2.xml piclist.txt CPU
```

## How to change MTCNN model from caffe to openVINO?
[Pay attention of mean and std values settings~](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_Converting_Model_General.html#when_to_specify_mean_and_scale_values)
```
python mo_caffe.py --input_model model/mtcnn/det3.caffemodel --mean_values [127.5,127.5,127.5] --scale_values [127.5,127.5,127.5] --output_dir model/mtcnn/
```

## Important!!!
一些pretrained的mtcnn-caffe模型在训练时,使用的人脸图像是经过转置的,即正脸逆时针旋转90度  
所以在使用基于此类模型转换的openVINO模型时,同样需要对输入图像进行转置操作

## Specially
This repo contains ```.vscode```folder, it will faciliate compiling and debuging in Visual Studio Code editor.
