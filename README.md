# yolov7_kcoco

* 한국형 비전 데이터셋의 객체 검출을 테스트하기 위해 사용함.
* 객체 검출을 위해 사용한 모델은 yolov7임.

## 환경설정
pytorch 설치
``` shell
$ conda create --name env python=3.9.16
$ conda activate env
$ conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch
```
소스
``` shell
$ git clone https://github.com/penguin46/yolov7_kcoco.git
$ cd yolov7_kcoco
$ pip install -r requirements.txt
```

## 학습
단일 GPU
``` shell
$ python train.py --workers 8 --device 0 --batch-size 128 --data data/kcoco.yaml --img 640 640 --cfg cfg/training/yolov7.yaml --weights '' --name yolov7-kcoco --hyp data/hyp.scratch.custom.yaml
```
다중 GPU
``` shell
$ python -m torch.distributed.launch --nproc_per_node 4 --master_port 9527 train.py --workers 8 --device 0,1,2,3 --sync-bn --batch-size 128 --data data/kcoco.yaml --img 640 640 --cfg cfg/training/yolov7.yaml --weights '' --name yolov7-kcoco --hyp data/hyp.scratch.custom.yaml
```
--nproc_per_node : 사용하려는 GPU 수를 지정함.
--batch-size : 전체 배치 사이즈
--data : 데이터 관련
--img : 입력 이미지 사이즈
--cfg : 모델 구조
--hyp : 하이퍼-파라미터 설정
--sync-bn : SyncBatchNorm

## 검증 또는 테스트
``` shell
$ python test.py --data data/kcoco.yaml --img-size 640 --device 0 --batch-size 32 --weights runs/train/yolov7-kcoco6/weights/best.pt --name yolov7-kcoco --task val(test)
```

## 추론
``` shell
$ python detect.py --weights weights/yolov7_kcoco_training.pt --conf 0.5 --source inference/images/car.jpg
```

## 참고
[https://github.com/WongKinYiu/yolov7.git](https://github.com/WongKinYiu/yolov7.git)
## LICENSE
Code released under GPL license.
