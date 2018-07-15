title: 图像识别ImageAI入门
date: 2018-07-15 20:57:21
tags:
categories:
- 图像识别
---
# 1 ImageAI简介
ImageAI是一个python的库，它能使开发人员用简单几行代码构建具有深度学习和计算机视觉功能的应用程序和系统。它是由Moses Olafenwa和John Olafenwa两位开发并维护。 
具体git地址：https://github.com/OlafenwaMoses/ImageAI 
# 2 安装
首先当然是python，imageai暂时只支持3.5.1或之后的版本,一般都是用3.6吧 
还有以下这些: 
Tensorflow>=1.4.0 
Numpy >=1.13.1 
SciPy >=0.19.1 
OpenCV 
Pillow 
Matplotlib 
h5py 
Keras 2.x
做好准备工作后就是安装了，可以直接使用pip3安装 如下
    pip3 install https://github.com/OlafenwaMoses/ImageAI/releases/download/2.0.1/imageai-2.0.1-py3-none-any.whl 
当然也可以将imageai-2.0.1-py3-none-any.whl下载之后安装
    pip3 install C:\User\MyUser\Downloads\imageai-2.0.1-py3-none-any.whl
# 3 入门 
    from imageai.Detection import ObjectDetection
    import os

    execution_path = os.getcwd()


    detector = ObjectDetection()
    detector.setModelTypeAsRetinaNet()
    # resnet50_coco_best_v2.0.1.h5下载地址https://github.com/OlafenwaMoses/ImageAI/releases/download/1.0/resnet50_coco_best_v2.0.1.h5，准确度，比其他的都高

    detector.setModelPath( os.path.join(execution_path , "resnet50_coco_best_v2.0.1.h5"))
    detector.loadModel()


    detections, objects_path = detector.detectObjectsFromImage(input_image=os.path.join(execution_path , "timg.jpeg"), output_image_path=os.path.join(execution_path , "image3new.jpg"), extract_detected_objects=True)


    for eachObject, eachObjectPath in zip(detections, objects_path):
        print(eachObject["name"] + " : " + eachObject["percentage_probability"] )
    
    运行会提示
# 4 去除识别标签以及准确度
    在实际使用中我们可能不需要将识别出来的物体标签化以及显示，这里需要修改源码部分
    https://github.com/OlafenwaMoses/ImageAI/blob/master/imageai/Detection/__init__.py
    注释掉draw_caption方法即可