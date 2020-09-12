# DBNet

The Pytorch implementation is [DBNet](https://github.com/BaofengZan/DBNet.pytorch).

## How to Run

The CmakeLists.txt provided by this repository is the win version. Please see the last link for Linux version.。

* 1 Generate wts
  Download the code and model from the pytoch repository. After configuring the environment
  
 In tools/predict.py, set the save_wts attribute to True. After running, the wts file will be generated in the tools folder.

  You can also export onnx. Set the onnx property to True.

* 2 cmake generates a VS project, then compile and run. Different parameters passed in the main function have different functions. -s is to generate engin files. -d imgpath stands for running forward.

  ![image-20200807183412846](https://user-images.githubusercontent.com/20653176/89722330-00c36900-da1b-11ea-97f4-c61f9cd196fa.png)

## linux version

https://github.com/wang-xinyu/tensorrtx


## Insufficient

* 1 In the common file, the following two functions can be combined.

```c++
ILayer* convBnLeaky(INetworkDefinition *network, std::map<std::string, Weights>& weightMap, ITensor& input, int outch, int ksize, int s, int g, std::string lname, bool bias = true) 
```

```c++
ILayer* convBnLeaky2(INetworkDefinition *network, std::map<std::string, Weights>& weightMap, ITensor& input, int outch, int ksize, int s, int g, std::string lname, bool bias = true)
```

* 2 There are many differences between the post-processing and the pytorch version, which can be improved.
* 3 Data preprocessing in pyorch is to resize the short side of the image to 1024, scale the long side proportionally, and finally cut the new width and height to a multiple of 32. Resize the image directly to 640*640 in your own repo, which is more crude.
