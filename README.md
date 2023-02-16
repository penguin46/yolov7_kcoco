# yolov7_kcoco

* 한국형 비전 데이터셋의 객체 검출을 테스트하기 위해 사용함.
* 객체 검출을 위해 사용한 모델은 yolov7임.

## Training
단일 GPU
``` shell
$ python train.py --workers 8 --device 0 --batch-size 128 --data data/kcoco.yaml --img 640 640 --cfg cfg/training/yolov7.yaml --weights '' --name yolov7-kcoco --hyp data/hyp.scratch.custom.yaml
```


## 참고
[https://github.com/WongKinYiu/yolov7.git](https://github.com/WongKinYiu/yolov7.git)
## LICENSE
Code released under GPL license.
