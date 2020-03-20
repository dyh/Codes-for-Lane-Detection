
tips

-----
不要用 PyTorch 0.3.0，代码已经升级到1.3.0了。conda的环境配置见最后。
重点：
pytorch                   1.3.0           py3.7_cuda10.0.130_cudnn7.6.3_0    pytorch
pillow                    6.1.0            py37h6b7be26_1    conda-forge
cudatoolkit               10.0.130                      0    defaults
opencv                    3.4.2            py37h6fd60c2_1    defaults
torchvision               0.4.1                py37_cu100    pytorch

-------------------------------------------------------------------------------
ERFNet_trained.tar文件，不用解压
-----
no cuda capable device is detected
test_erfnet.sh文件，需要更改，内容如下：
（1）gpus，原来是5、6、7、8 GPU。
（2）test_img，更改目录。

python3 -u test_erfnet.py CULane ERFNet train test_img \
                          --lr 0.01 \
                          --gpus 0 \
                          --resume trained/ERFNet_trained.tar \
                          --img_height 208 \
                          --img_width 976 \
                          -j 10 \
                          -b 5

-----
sync_bn 错误，如果不训练model，可以注释 from models import sync_bn
如果训练model，自行下载syncbn。
-----
pil错误，7.0没有此方法，降级到6.1，
conda install pillow==6.1
-----

AttributeError: 'NoneType' object has no attribute 'astype'
图片路径需要更改，形成如下路径
/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/test_img/list   【test_img.txt】
/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/test_img/driver_37_30frame/05181432_0203.MP4   【里面有各种图片】

-----
voc_aug.py错误，更改路径：
/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/dataset/voc_aug.py

def __init__(self, dataset_path='/root/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch/test_img/list', data_list='train', transform=None):

-----


-------------------------------------------------------------------------------

conda list 环境：

(erfnet) root@linux:~/Codes-for-Lane-Detection/ERFNet-CULane-PyTorch# conda list
# packages in environment at /root/anaconda3/envs/erfnet:
#
# Name                    Version                   Build  Channel
_libgcc_mutex             0.1                 conda_forge    conda-forge
_openmp_mutex             4.5                      1_llvm    conda-forge
bzip2                     1.0.8                h516909a_2    conda-forge
ca-certificates           2019.11.28           hecc5488_0    conda-forge
cairo                     1.14.12           h80bd089_1005    conda-forge
certifi                   2019.11.28       py37hc8dfbb8_1    conda-forge
cffi                      1.14.0           py37hd463f26_0    conda-forge
cudatoolkit               10.0.130                      0    defaults
ffmpeg                    4.0.2                ha0c5888_2    conda-forge
fontconfig                2.13.1            he4413a7_1000    conda-forge
freeglut                  3.0.0             hf484d3e_1005    conda-forge
freetype                  2.10.0               he06d7ca_2    conda-forge
gettext                   0.19.8.1          hc5be6a0_1002    conda-forge
giflib                    5.2.1                h516909a_2    conda-forge
glib                      2.56.2            had28632_1001    conda-forge
gmp                       6.1.2             hf484d3e_1000    conda-forge
gnutls                    3.5.19               h2a4e5f8_1    conda-forge
graphite2                 1.3.13            hf484d3e_1000    conda-forge
harfbuzz                  1.9.0             he243708_1001    conda-forge
hdf5                      1.10.2               hc401514_3    conda-forge
icu                       58.2              hf484d3e_1000    conda-forge
jasper                    2.0.14               habb8e15_1    conda-forge
jpeg                      9c                h14c3975_1001    conda-forge
ld_impl_linux-64          2.34                 h53a641e_0    conda-forge
libblas                   3.8.0               16_openblas    conda-forge
libcblas                  3.8.0               16_openblas    conda-forge
libffi                    3.2.1             he1b5a44_1007    conda-forge
libgcc-ng                 9.2.0                h24d8f2e_2    conda-forge
libgfortran               3.0.0                         1    conda-forge
libgfortran-ng            7.3.0                hdf63c60_5    conda-forge
libglu                    9.0.0             hf484d3e_1000    conda-forge
libiconv                  1.15              h516909a_1005    conda-forge
liblapack                 3.8.0               16_openblas    conda-forge
libopenblas               0.3.9                h5ec1e0e_0    conda-forge
libopencv                 3.4.2                hb342d67_1    defaults
libpng                    1.6.37               hed695b0_0    conda-forge
libstdcxx-ng              9.2.0                hdf63c60_2    conda-forge
libtiff                   4.1.0                hc7e4089_5    conda-forge
libuuid                   2.32.1            h14c3975_1000    conda-forge
libwebp                   1.1.0                h56121f0_2    conda-forge
libwebp-base              1.1.0                         2    conda-forge
libxcb                    1.13              h14c3975_1002    conda-forge
libxml2                   2.9.9                h13577e0_2    conda-forge
llvm-openmp               9.0.1                hc9558a2_2    conda-forge
lz4-c                     1.8.3             he1b5a44_1001    conda-forge
mkl                       2020.0                      166    conda-forge
ncurses                   6.1               hf484d3e_1002    conda-forge
nettle                    3.3                           0    conda-forge
ninja                     1.10.0               hc9558a2_0    conda-forge
numpy                     1.18.1           py37h95a1406_0    conda-forge
olefile                   0.46                       py_0    conda-forge
opencv                    3.4.2            py37h6fd60c2_1    defaults
openh264                  1.8.0             hdbcaa40_1000    conda-forge
openssl                   1.1.1e               h516909a_0    conda-forge
pcre                      8.44                 he1b5a44_0    conda-forge
pillow                    6.1.0            py37h6b7be26_1    conda-forge
pip                       20.0.2                     py_2    conda-forge
pixman                    0.34.0            h14c3975_1003    conda-forge
pthread-stubs             0.4               h14c3975_1001    conda-forge
py-opencv                 3.4.2            py37hb342d67_1    defaults
pycparser                 2.20                       py_0    conda-forge
python                    3.7.6           h357f687_4_cpython    conda-forge
python_abi                3.7                     1_cp37m    conda-forge
pytorch                   1.3.0           py3.7_cuda10.0.130_cudnn7.6.3_0    pytorch
readline                  8.0                  hf8c457e_0    conda-forge
setuptools                46.0.0           py37hc8dfbb8_2    conda-forge
six                       1.14.0                     py_1    conda-forge
sqlite                    3.30.1               hcee41ef_0    conda-forge
tk                        8.6.10               hed695b0_0    conda-forge
torchvision               0.4.1                py37_cu100    pytorch
wheel                     0.34.2                     py_1    conda-forge
x264                      1!152.20180806       h14c3975_0    conda-forge
xorg-fixesproto           5.0               h14c3975_1002    conda-forge
xorg-inputproto           2.3.2             h14c3975_1002    conda-forge
xorg-kbproto              1.0.7             h14c3975_1002    conda-forge
xorg-libice               1.0.10               h516909a_0    conda-forge
xorg-libsm                1.2.3             h84519dc_1000    conda-forge
xorg-libx11               1.6.9                h516909a_0    conda-forge
xorg-libxau               1.0.9                h14c3975_0    conda-forge
xorg-libxdmcp             1.1.3                h516909a_0    conda-forge
xorg-libxext              1.3.4                h516909a_0    conda-forge
xorg-libxfixes            5.0.3             h516909a_1004    conda-forge
xorg-libxi                1.7.10               h516909a_0    conda-forge
xorg-libxrender           0.9.10            h516909a_1002    conda-forge
xorg-renderproto          0.11.1            h14c3975_1002    conda-forge
xorg-xextproto            7.3.0             h14c3975_1002    conda-forge
xorg-xproto               7.0.31            h14c3975_1007    conda-forge
xz                        5.2.4             h14c3975_1001    conda-forge
zlib                      1.2.11            h516909a_1006    conda-forge
zstd                      1.4.4                h3b9ef0a_1    conda-forge

-------------------------------------------------------------------------------






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

