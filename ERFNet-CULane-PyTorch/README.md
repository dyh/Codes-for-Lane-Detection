
tips

#### 不要用 PyTorch 0.3.0，代码已经升级到1.3.0了。conda的环境配置见《conda-envs.yaml》。
导入conda配置，使用：conda env create -f conda-envs.yaml

#### ERFNet_trained.tar文件，不用解压

#### no cuda capable device is detected
test_erfnet.sh文件，需要更改，内容如下：
1. gpus，原来是5、6、7、8 GPU。
2. test_img，更改目录。
3. 删除了--npb参数。

python3 -u test_erfnet.py CULane ERFNet train test_img \
                          --lr 0.01 \
                          --gpus 0 \
                          --resume trained/ERFNet_trained.tar \
                          --img_height 208 \
                          --img_width 976 \
                          -j 10 \
                          -b 5

#### sync_bn 错误，如果不训练model，可以注释 from models import sync_bn
如果训练model，自行下载syncbn。

#### pil错误，7.0没有此方法，降级到6.1，
conda install pillow==6.1


#### AttributeError: 'NoneType' object has no attribute 'astype'
图片路径需要更改，形成如下路径
/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/test_img/list   【test_img.txt】
/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/test_img/driver_37_30frame/05181432_0203.MP4   【里面有各种图片】

#### voc_aug.py错误，更改路径：
/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/dataset/voc_aug.py

def __init__(self, dataset_path='/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/test_img/list', data_list='train', transform=None):


-------------------------------------------------------------------------

### Requirements
- [PyTorch 0.3.0](https://pytorch.org/get-started/previous-versions/).
- Matlab (for tools/prob2lines), version R2014a or later.
- Opencv (for tools/lane_evaluation), version 2.4.8 (later 2.4.x should also work).

### Before Start

Please follow [list](./list) to put CULane in the desired folder. We'll call the directory that you cloned ERFNet-CULane-PyTorch as `$ERFNet_ROOT`.

### Testing
1. Download our trained models to `./trained`
    ```Shell
    cd $ERFNet_ROOT/trained
    ```
   The trained model has already been there.

2. Run test script
    ```Shell
    cd $ERFNet_ROOT
    sh ./test_erfnet.sh
    ```
    Testing results (probability map of lane markings) are saved in `experiments/predicts/` by default.

3. Get curve line from probability map
    ```Shell
    cd tools/prob2lines
    matlab -nodisplay -r "main;exit"  # or you may simply run main.m from matlab interface
    ```
    The generated line coordinates would be saved in `tools/prob2lines/output/` by default.

4. Calculate precision, recall, and F-measure
    ```Shell
    cd $ERFNet_ROOT/tools/lane_evaluation
    make
    sh Run.sh   # it may take over 30min to evaluate
    ```
    Note: `Run.sh` evaluate each scenario separately while `run.sh` evaluate the whole. You may use `calTotal.m` to calculate overall performance from all senarios.  
    By now, you should be able to reproduce the result (F1-measure: 73.1).
    
### Training
1. Download the pre-trained model
    ```Shell
    cd $ERFNet_ROOT/pretrained
    ```
   The pre-trained model has already been there.
2. Training ERFNet model
    ```Shell
    cd $ERFNet_ROOT
    sh ./train_erfnet.sh
    ```
    The training process should start and trained models would be saved in `trained` by default.  
    Then you can test the trained model following the Testing steps above. If your model position or name is changed, remember to set them to yours accordingly.

