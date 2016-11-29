## deeplab-ver2-docker

This repository contains a standalone dockerfile to correctly install GPU executable image for [deeplab-public-ver2](https://bitbucket.org/aquariusjay/deeplab-public-ver2).
The image can be built by running:

```
nvidia-docker build -t caffe_dl:gpu standalone/dl_gpu
```

The image requires a CUDA 7.5 capable driver to be installed on the system and [nvidia-docker](https://github.com/NVIDIA/nvidia-docker) for running the Docker containers.

For more information on how to run Caffe using the docker image please refer to the [Caffe guide](https://github.com/BVLC/caffe/blob/master/docker/README.md).

For more information on capabilities of deeplab-public-ver2, please refer to the [source code](https://bitbucket.org/aquariusjay/deeplab-public-ver2), or to the following paper:

    @article{CP2016Deeplab,
      title={DeepLab: Semantic Image Segmentation with Deep Convolutional Nets, Atrous Convolution, and Fully Connected CRFs},
      author={Liang-Chieh Chen and George Papandreou and Iasonas Kokkinos and Kevin Murphy and Alan L Yuille},
      journal={arXiv:1606.00915},
      year={2016}
    }
