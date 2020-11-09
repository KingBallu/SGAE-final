# SGAE-final

## Auto-Encoding Scene Graphs for Image Captioning 

Graph R-CNN :  pytorch 1.0 버전에서만 동작

SGAE :  pytorch 1.5 버전에서 동작 확인 

### 코드 

cider-master    : score 측정

coco-caption    : score 측정 

graph_rcnn      : scene graph 생성

models          : 모델

scripts         : 스크립트 파일들 


### 실행 방법 

* Graph R-CNN (Scene graph 생성) \

    ```
    cd graph_rcnn/data_tools/data
    ```
    1. 데이터 셋 \
    
        데이터 다운로드 \
        [MS COCO](https://cocodataset.org/#download)
        ```
        train2014/
        val2014/
        test2014/
        ```
        [Split MetaData](https://drive.google.com/drive/folders/1GvwpchUnfqUjvlpWTYbmEvhvkJTIWWRb)
        ```
        cocobu2.json
        ```
       [VOCAB data](https://github.com/danfeiX/scene-graph-TF-release/tree/master/data_tools)
       ```
        VG-SGG-dict.json
        VG_SGG.h5
       mv VG-SGG-dict.json ../../datasets/vg_bm
       mv VG_SGG.h5 ../../datasets/vg_bm
       ``` 
    
    2. 이미지 전처리
       ```
       cd ..
       bash ./create_imdb.sh
       ```
       결과 파일 (**COCO_imdb_1024.h5**) 생성 
       
       Directory 이동 
       ```
        mv data_tools/VG/COCO_imdb_1024.h5 datasets/vg_bm
       ```
    
    3. Scene Graph 생성
        ```
        bash ./eval.sh
        ```
        results 에 graph_rcnn 결과 파일 생성
        
        
* SGAE (Image Captioning)

    ```
    cd ..
    ```
    SGAE-final/
    
    1. Graph R-CNN 결과 전처리 
        ```
        bash ./scripts/prepro_graph_rcnn.sh
        ```
       결과 파일 *_att, *_box, *_fc 이동 \
       ex)
       ```
        mv *_att, *_box, *_fc ../data  
       ```
        SGAE_project/data 에 *_att, *_box, *_fc 이동 

    2. Train
        ```
        bash ./train.sh
        ```
    
    3. Eval
        ```
        bash ./eval.sh
        ```
