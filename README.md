# DAC_2020

---


https://eehoeskrap.tistory.com/352 를 참고했습니다.
2. Convert Yolo v3 model to Keras model
2-1. 방법 1
*잘못된 코드 수정해야함.

darknet 학습을 통해 만들어진 .weights 파일을 텐서플로우에서 실행하기 위하여 keras 파일인 .h5 파일로 변환할 수 있는 github. https://github.com/xiaochus/YOLOv3


---


# 학습시킨 weights 파일을 다운로드
!wget https://pjreddie.com/media/files/yolov3.weights

# git clone 하기
!git clone https://github.com/xiaochus/YOLOv3
# 1. process_image 함수 시작 전 코드 삽입
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
in demo.py

# 2. 오타 수정
col = np.tile(np.arange(0, grid_w), grid_h).reshape(-1, grid_w)

row = np.tile(np.arange(0, grid_h).reshape(-1, 1), grid_w) 

col = col.reshape(grid_h, grid_w, 1, 1).repeat(3, axis=-2) 

row = row.reshape(grid_h, grid_w, 1, 1).repeat(3, axis=-2)


in YOLOv3/model/yolo_model.py

# 3. YOLOv3/cfg/yolo.cfg 파일 수정
우리가 학습시킨 yolo.cfg파일로 수정

# yad2k.py: python file to convert darknet weight file to keras h5 file. 
# The yad2k.py was modifiled from allanzelener/YAD2K
# converted weighted file will be located at ./YOLOv3/data/yolo.h5
!python ./YOLOv3/yad2k.py ./YOLOv3/cfg/yolo.cfg yolov3.weights ./YOLOv3/data/yolo.h5

# run follow command to show the demo. The result can be found in images/res folder
%cd YOLOv3
!dir
!python demo.py

# demo.py 파일 수정
### 1. file = 'data/coco_classes.txt'
우리 class파일로 수정

### 2. for(root, dirs, files) in os.walk('images/test'):
test이미지 파일 경로, images/test

### 3. detect videos 이후 line 제거
