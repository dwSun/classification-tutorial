# TensorFlow/pyTorch/mxnet 的分类模型训练教程

这个教程源于 TFv2.0 官方的两个教程，做完了 TF 的版本之后，不过瘾，就顺手又撸了 pyTorch 和 mxnet 的版本。

# 文件说明

- [inference-mxnet.ipynb](inference-mxnet.ipynb) mxnet 版本模型应用
- [inference-torch.ipynb](inference-torch.ipynb) pyTorch 版本模型应用
- [inference.ipynb](inference.ipynb) TensorFlow V2.0 版本模型应用
- [readme.md](readme.md) 
- [train-mxnet.ipynb](train-mxnet.ipynb)  mxnet 版本模型训练
- [train-torch.ipynb](train-torch.ipynb)  pyTorch 版本模型训练
- [train.ipynb](train.ipynb)  TensorFlow V2.0 版本模型训练

# 一点心得

三个框架发展了这些年，各有千秋，就目前的教程内容看，似乎 TF 展现出来的易用性是最高的，pytorch 的静态图不是很方便，mxnet 虽然是混合图，但是本身有很多常用功能没有实现，远不如 pytorch 和 TF 的社区庞大。但是 mxnet 1.6 版本发布了 numpy 的兼容 api 可以让很多框架无缝集成，优化 GPU 的使用， 这是一个很有意思的点，前途不可估量。

写教程的过程中，各个框架模型收敛速度有区别，所以轻度刨根问底了一下，结论如下：
- 看起来完全一样的默认参数未必是一样的
  - 教程使用的模型结构代码上完全一致
    - 对于 batchnormal 等，各框架实现细节不同（跟朋友交谈得知，未确认）
    - 对于取整的操作有区别，TF 是向上取整，mxnet 是向下取整，pytorch 没确认
  - 优化器默认参数一致，但是各框架优化器实现细节有区别（跟朋友交谈得知，未确认）
  - 模型默认初始化方式不同
    - TF 统一使用 glorot_uniform(也叫 xavier_uniform) 初始化
    - mxnet 统一使用了 unform 初始化，收敛速度一定会比较慢，所以一定要自己指定初始化
    - pytorch 使用的是 kaiming_uniform(也称MSRA_uniform)初始化

# 关于框架选择

TF真香，挺好用的，整个生态也比较完整，但是 API 整体设计比较无语，倒是一些细节做的很好，如果没有特殊理由，选 TF 没错。
pytorch，个人认为，完完全全看不出来好用在哪里，为啥学术圈那么多人用，倒是发现很多比较新的学术成果，pytorch 官方的代码里面竟然都有实现，也就是 pytorch 跟学术成果跟的最紧，生态也很不错。
mxnet，心情复杂，API 是最好用的，但是生态实在是太小，一些功能缺失，如果能做到跟 pytorch 一样的生态，估计就没别的框架什么事情了。但是这还真是一个鸡生蛋蛋生鸡的问题，有人用就会生态好，生态好才有人用，我希望有一天 mxnet 能真的火起来。

结论是，没有结论。

最近由于用 mxnet 资源实在不好找，考虑换到 pytorch 了，毕竟能够省一些力气，而且很多产品也对 pytorch 提供很好的支持。但我不会放弃 mxnet 的。
