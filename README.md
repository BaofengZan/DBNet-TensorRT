# DBNet

The Pytorch implementation is [DBNet](https://github.com/BaofengZan/DBNet.pytorch).

## How to Run

本仓库提供的CmakeLists.txt为win版本。Linux版本请看最后的链接。

* 1 生成wts
  从pytoch仓库下载到代码和模型。配置好环境后

  在tools/predict.py中，将save_wts属性置为True，运行后，就在在tools文件夹下生成wts文件。

  同时也可以导出onnx。将onnx属性设置为True即可。

* 2 cmake 生成工程

  ```
  mkdir build
  cd build
  cmake ..
  make
  ./dbnet -s             // serialize model to plan file i.e. 'DBNet.engine'
  ./dbnet -d  ../samples // deserialize plan file and run inference, the images in samples will be processed.
  ```

  ![image-20200807183412846](imgs/image-20200807183412846.png)

## linux版本

https://github.com/wang-xinyu/tensorrtx
