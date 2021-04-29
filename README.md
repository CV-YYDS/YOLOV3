# YOLOv3
---
## 准备工作

### 1、将 YOLOV3 克隆到本地
```Bash
git clone https://github.com/Peterisfar/YOLOV3.git
```
更新yolov3_config_voc.py中的`"PROJECT_PATH"`.
```Bash
＃安装软件包
pip3 install -r requirements.txt --user
```

### 2、下载数据集
* 下载Pascal VOC数据集: [VOC 2012_trainval](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar) 、[VOC 2007_trainval](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar)、[VOC2007_test](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtest_06-Nov-2007.tar).将它们全部放入data文件夹中，并且更新yolov3_config_voc.py中的`"DATA_PATH"`.
* 转换数据格式，将Pascal VOC * .xml格式转换为自定义格式(Image_path0 &nbsp; xmin0,ymin0,xmax0,ymax0,class0 &nbsp; xmin1,ymin1...)

```bash
cd YOLOV3 && mkdir data
cd utils
python3 voc.py # 在data/中获取train_annotation.txt和test_annotation.txt
```

### 3、下载权重文件
* Darknet预训练权重:  [darknet53-448.weights](https://pjreddie.com/media/files/darknet53_448.weights) 

在YOLOV3文件夹中创建`weight/`文件夹，并将下载好的权重文件放入其中.

---
## 训练

运行以下命令以开始训练，并在`config/yolov3_config_voc.py`中查看更多参数配置信息

```Bash
WEIGHT_PATH=weight/darknet53_448.weights

CUDA_VISIBLE_DEVICES=0 nohup python3 -u train.py --weight_path $WEIGHT_PATH --gpu_id 0 > nohup.log 2>&1 &

```

`Notes:`

* 可以运行`"cat nohup.log"`来输出训练步骤.
* 它支持通过添加`--resume`来恢复训练过程，这将会自动加载`last.pt`.

---
## 测试
应该自定义权重文件路径 `WEIGHT_FILE` 和测试数据的路径`DATA_TEST`
```Bash
WEIGHT_PATH=weight/best.pt
DATA_TEST=./data/test # 你自己的图片

CUDA_VISIBLE_DEVICES=0 python3 test.py --weight_path $WEIGHT_PATH --gpu_id 0 --visiual $DATA_TEST --eval

```
图片可以在`data/`中进行查看


---
## 参考
* pytorch : https://github.com/ultralytics/yolov3

