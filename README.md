## 關於

本項目為 [WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7) 應用於人臉辨識的練習，以卡通哆啦A夢中的人物作為標的，分別在 ***Google Colaboratory**、 **Windows Anaconda** 和 **Linux Docker** 環境中 Inference on image*。  惟因 local端運行 GPU OUT OF MEMORY，故在 Colaboratory 進行模型的訓練與影像辨識(.mp4)。

## 準備

- 圖片標註  (已完成，可略)  
利用 labelImg 標註工具，確認轉換為yolo格式。(共281張圖，約需2小時)  
`pip install labelImg`  
`labelImg`  

- 下載 [WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7) 資料夾並修改  
> 下載此資料夾  **yolov7-custom**  
>> - [x] 將 data 目錄下的 train, val, custom_data.yaml 放入yolov7資料夾的data/目錄下  
    `yolov7/data/train val custom_data.yaml`  
>> - [x] 將 yolov7-custom.yaml 放入yolov7資料夾的cfg/training/目錄下  
    `yolov7/cfg/training/yolov7-custom.yaml`  
>> - [x] 將 requirements.txt, requirements_gpu.txt, yolov7_custom.pt, do_01.jpg, Doraemon.mp4 放入yolov7資料夾的yolov7/目錄下  
    `yolov7/requirements.txt requirements_gpu.txt yolov7_custom.pt do_01.jpg Doraemon.mp4`  



## 平台

### Google Colaboratory

`%cd /content/yolov7`  

- Inference on image  
`!python detect.py --weights yolov7_custom.pt --conf 0.5 --img-size 640 --source do_01.jpg`  

- Inference on video  
`!python detect.py --weights yolov7_custom.pt --conf 0.5 --img-size 640 --source Doraemon.mp4`  

- 結果在 yolov7/runs/detect/exp/  

### Windows Anaconda

`cd yolov7`  

- 安裝套件  
`conda>pip install -r requirements.txt`  
`conda>pip install -r requirements_gpu.txt`  

- Inference on image  
`python detect.py --weights yolov7_custom.pt --conf 0.5 --img-size 640 --source do_01.jpg`  

- 結果在 yolov7/runs/detect/exp/  

### Linux Docker

- 下載 yolov7-custom.zip 到 Linux 並解壓縮  

  `cd yolov7-custom`

- 將 dockerfile 打包成 image  
`docker image build -t yolov7 .`  

- 產生隔離的執行環境 container  
`docker run -it --name doraemon yolov7`  

- Inference on image  
`python detect.py --weights yolov7_custom.pt --conf 0.5 --img-size 640 --source do_01.jpg`  

- 將圖片從 container app/runs/detect/exp/ 中複製到host端，從 host 端:  
`docker cp [container NAMES]:/[container圖片路徑]  [儲存到本機端路徑位址]`  
`docker cp doraemon:/app/runs/detect/exp/do_01.jpg ..`  



## 可能遇到的問題與解決方法  

  - 安裝 requirements.txt 時，出現 Error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/)  
  `安裝 Visual Studio Build-Tools 2022 -> 勾選...c++...`  
  `pip install -r requirements.txt`  

  - Windows anaconda 環境時，圖片若無法顯現偵測框......  
  _torch, torchvision 版本更新_  
  `conda list`  
  `pip install -U torch`  
  `pip install -U torchvision`  
  
  - 若出現錯誤信息: ImportError: libGL.so.1: cannot open shared object file: No such file or directory......  
  _opencv import 有問題_  
  `pip uninstall opencv-python`  
  `pip install opencv-python-headless`  



version https://git-lfs.github.com/spec/v1
oid sha256:bff213b0d31bf492c22cdd3cb266759eb532fd407500fcb6dc19a07004e814ca
size 18  
