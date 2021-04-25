# YOLOv3
---
## Prepared work

### 1、Git clone YOLOV3 repository
```Bash
git clone https://github.com/Peterisfar/YOLOV3.git
```
update the `"PROJECT_PATH"` in the params.py.
### 2、Download dataset
* Download Pascal VOC dataset : [VOC 2012_trainval](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar) 、[VOC 2007_trainval](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar)、[VOC2007_test](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtest_06-Nov-2007.tar). put them in the dir, and update the `"DATA_PATH"` in the params.py.
* Convert data format : Convert the pascal voc *.xml format to custom format (Image_path0 &nbsp; xmin0,ymin0,xmax0,ymax0,class0 &nbsp; xmin1,ymin1...)

```bash
cd YOLOV3 && mkdir data
cd utils
python3 voc.py # get train_annotation.txt and test_annotation.txt in data/
```

### 3、Download weight file
* Darknet pre-trained weight :  [darknet53-448.weights](https://pjreddie.com/media/files/darknet53_448.weights) 
* This repository test weight : [best.pt](https://pan.baidu.com/s/1MdE2zfIND9NYd9mWytMX8g)

Make dir `weight/` in the YOLOV3 and put the weight file in.

---
## Train

Run the following command to start training and see the details in the `config/yolov3_config_voc.py`

```Bash
WEIGHT_PATH=weight/darknet53_448.weights

CUDA_VISIBLE_DEVICES=0 nohup python3 -u train.py --weight_path $WEIGHT_PATH --gpu_id 0 > nohup.log 2>&1 &

```

`Notes:`

* Training steps could run the `"cat nohup.log"` to print the log.
* It supports to resume training adding `--resume`, it will load `last.pt` automaticly.

---
## Test
You should define your weight file path `WEIGHT_FILE` and test data's path `DATA_TEST`
```Bash
WEIGHT_PATH=weight/best.pt
DATA_TEST=./data/test # your own images

CUDA_VISIBLE_DEVICES=0 python3 test.py --weight_path $WEIGHT_PATH --gpu_id 0 --visiual $DATA_TEST --eval

```
The images can be seen in the `data/`

---
## TODO

* [ ] Mish
* [ ] OctConv
* [ ] Custom data


---
## Reference

* tensorflow : https://github.com/Stinky-Tofu/Stronger-yolo
* pytorch : https://github.com/ultralytics/yolov3
* keras : https://github.com/qqwweee/keras-yolo3
