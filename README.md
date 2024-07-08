Predicted vis classes and coordinates are put in df_keypoints_test_filled.csv

df_keypoints_corrected.csv is modified base df_keypoints with some data inputations and corrections

TRAINING (on Windows with NVIDIA GPU)

1. Download and unzip or clone YOLOv7 repository from https://github.com/WongKinYiu/yolov7
2. Create Python virtual environment (preferable) or Docker container (follow steps from https://github.com/WongKinYiu/yolov7 then)
3. Remove default requirements.txt from yolov7 folder and paste attached requirements.txt and requirementsGPU.txt (Windows only)
4. Install requirements from requirements.txt and requirementsGPU.txt file in venv (or container)
5. Unzip attached notebook file
6. Put folder with data and unzipped notebook folder in yolov7 folder
7. Put attached yolov7_pitch.yaml in cdf/training folder and pitch_data.yaml in data folder
8. Download YOLOv7 weights from https://github.com/WongKinYiu/yolov7 - under 'Performance' ribbon
8a. If you want to recreate my steps, like correcting errors or labelling keypoint 30, proceed with 1_EDA.ipynb in notebook folder
9. Proceed with 2_Data_Preparation.ipynb - it generates training and validation data and labels.  
10. Remove train and val folders from data folder and place there folders with generated data from notebook folder
11. Run CLI in main folder, paste and run command "python train.py --workers 1 --device 0 --batch-size 8 --epochs 100 --img 640 640 --data data/pitch_data.yaml --hyp data/hyp.scratch.custom.yaml --cfg cfg/training/yolov7_pitch.yaml --name yolov7_pitch_0 --weights yolov7.pt"
12. Your model appears in runs/train/yolov7_pitch_0 folder (or yolov7_pitch_0# where # - any number)
13. Copy best.pt from runs/train/yolov7_pitch_0/pitch and paste it in main yolov7 directory
14. Proceed futher with 3_Training_and_Evaluation.ipynb

INFERENCE

1. Download and unzip or clone YOLOv7 repository from https://github.com/WongKinYiu/yolov7
2. Create Python virtual environment (preferable) or Docker container
3. Install requirements from requirements.txt in yolov7 folder
4. Put attached best_0.pt weights in main folder 
5. Put your images in inference/images folder
6a. Run CLI in main folder, paste and run command "python detect.py --weights best_0.pt --conf 0.5 --img-size 640 --source inference/images --save-txt "
6b. Alternatively unzip attached notebook file, put it in yolov7 folder, and run notebook/0_Inference_on_test_data.ipynb
7. Your inference pops in is in runs/detect/exp

METRICS

In general for visibility classification task I recommend using precision, recall, f1 and MCC (since it takes True Negatives into account). For regression of coordinates I suggest using mean absolute error, or mean squared error if you want to be strict - if the model misses the boundary box by more than a few px, this error skyrockets - see more in Task description.pdf in Section 5.

Additional experiments.pdf contains description of further steps that were taken to improve the model.

