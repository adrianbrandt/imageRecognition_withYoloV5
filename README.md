### Working YoloV5 on windows 10

#### How to install & run YOLOv5 on windows10

#### Step1
##### Installing python
Make sure you have python installed. Any versionb newer than python 3.9 should work fine.

#### Step2
##### Installing cuda
Install CUDA - Head over to https://developer.nvidia.com/cuda-downloads and download Version OS-Windows|Architecture-x86_64|Version-10|type-exe(local)

#### Step3
##### Installing pytorch
Install pytorch - open CMD with admin privilages and enter the command: pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113
This will install torch,torchvision and torchaudio for you.

#### Step4
##### installing deppendencies
Open CMD from yolov5-master folder and enter the following - pip install -r requirements.txt

##### Note
You'll likely get a big red error message during this stage telling you to install Visual Studio.
If you get this, you can download it here. (The error is related to PyCOCOTools.)
IF ERROR APPEARED(
pip install git+https:﻿//github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
now run in CMD again pip install -r requirements.txt
)

#### Step5
##### Editing yaml file for your computer
Edit the data.yaml file in the coco folder and edit the train/val path to your computer's absolute path of the image fodlers.

#### Step6
##### Starting the trainer.
Use CMD from master folder and enter the command: python train.py --img 128 --cfg ./models/yolov5s.yaml --batch 32 --epochs 200 --data ./data/coco/data.yaml --weights yolov5s.pt --workers 2 --name yolov5s_results --cache

#### Step7
##### Retraining YOLO.
Use CMD with the same command as last step but with the last sessions best result as the new weights: in my example: 
python train.py --img 128 --cfg ./models/yolov5s.yaml --batch 32 --epochs 100 --data ./data/coco/data.yaml --weights C:\yolov5-master\runs\train\yolov5s_results\weights\best.pt --workers 2 --name yolov5s_results --cache

#### Step8
##### Detection! For this example i have moved all the test images to the folder "test_row"
Use the cmd and enter command: python detect.py --weights runs/train/yolov5s_results"Latest"/weights/best.pt --img 128 --conf 0.4 --source test_row

#### Step9
##### Redo step 7-8
Redo steps 7-8 with the latest best weights until you get a result you enjoy! Depending on the amount of epochs you take, the results may be different.

#### Step10
##### Completed
Go to folder Runs/detect/exp(last) and see the results of the latest detection run

##### latest tested & working training:
python train.py --img 128 --cfg ./models/yolov5s.yaml --batch 805 --epochs 200 --data ./data/coco/data.yaml --weights C:\yolov5-master\runs\train\yolov5s_results15\weights\best.pt --workers 4 --name yolov5s_results --cache
