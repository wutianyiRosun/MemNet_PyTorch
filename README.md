# MemNet-pytorch
An implementation of MemNet: A Persistent Memory Network for Image Restoration, ICCV2017

This is an unofficial implementation of "MemNet: A Persistent Memory Network for Image Restoration (MemNet)", ICCV 2017 in Pytorch. [[Paper]](http://openaccess.thecvf.com/content_ICCV_2017/papers/Tai_MemNet_A_Persistent_ICCV_2017_paper.pdf) 

You can get the official Caffe implementation [here](https://github.com/tyshiwo/MemNet).

This implementation is modified from the implementation of [VDSR](https://cv.snu.ac.kr/research/VDSR/) by [@Jiu XU](https://github.com/twtygqyy/pytorch-vdsr).


## Usage
### Training
```
usage: train_memnet.py [-h] [--batchSize BATCHSIZE] [--nEpochs NEPOCHS]
                       [--lr LR] [--step STEP] [--cuda] [--resume RESUME]
                       [--start-epoch START_EPOCH] [--clip CLIP]
                       [--threads THREADS] [--momentum MOMENTUM]
                       [--weight-decay WEIGHT_DECAY] [--pretrained PRETRAINED]
                       [--gpus GPUS]

PyTorch MemNet

optional arguments:
  -h, --help            show this help message and exit
  --batchSize BATCHSIZE
                        Training batch size
  --nEpochs NEPOCHS     Number of epochs to train
  --lr LR               the initial learning rate is 0.1
  --step STEP           Sets the learning rate is divided 10 every 20 epochs
  --cuda                Use cuda?
  --resume RESUME       Path to checkpoint (default: none)
  --start-epoch START_EPOCH
                        Manual epoch number (useful on restarts)
  --clip CLIP           Clipping Gradients. Default=0.4
  --threads THREADS     Number of threads for data loader to use, Default: 1
  --momentum MOMENTUM   Momentum, Default: 0.9
  --weight-decay WEIGHT_DECAY, --wd WEIGHT_DECAY
                        Weight decay, Default: 1e-4
  --pretrained PRETRAINED
                        path to pretrained model (default: none)
  --gpus GPUS           gpu ids (default: 0,1,2,3)

```

### Evaluation
```
usage: eval.py [-h] [--cuda] [--model MODEL] [--dataset DATASET] [--gpus GPUS]

PyTorch MemNet Eval

optional arguments:
  -h, --help         show this help message and exit
  --cuda             use cuda?
  --model MODEL      model path
  --dataset DATASET  dataset name, Default: Set5
  --gpus GPUS        gpu ids (default: 0)

```
An example of training usage is shown as follows:
```
python eval.py --cuda
```


### Demo
```
usage: demo.py [-h] [--cuda] [--model MODEL] [--image IMAGE] [--scale SCALE]
               [--gpus GPUS]

PyTorch Memnet Demo

optional arguments:
  -h, --help     show this help message and exit
  --cuda         use cuda?
  --model MODEL  model path
  --image IMAGE  image name
  --scale SCALE  scale factor, Default: 4
  --gpus GPUS    gpu ids (default: 0)
```

An example of training usage is shown as follows:
```
python demo.py --cuda
```

### Prepare Training dataset
  - the training data is generated with Matlab Bicubic Interpolation, please refer [Code for Data Generation](/data/SuperResolution/generate_trainingset_x234.m) for creating training files.
  
### Performance
  - We provide a ***rough*** pre-trained MemNet_M6R6 [model](/model) trained on [291](/data/Train_291) images with data augmentation. The model can achieve a better performance with a smart optimization strategy. For the MemNet_M6R6 implementation, you can manually modify the number of Memory blocks [here](/memnet1.py#L26:18).
  - The same adjustable gradient clipping's implementation as original paper.
  - No bias is used in this implementation.
  - No batch normalization is used in this implementation.
  - Performance in PSNR on Set5 
  
| Scale   | MemNet(M6R6) Paper | MemNet(M6R6) PyTorch|
| -------:| ------------------:| -------------------:|
| x2      | 37.74              | 37.69               |
| x3      | 34.03              | 34.02               |
| x4      | 31.68              | 31.70               |

