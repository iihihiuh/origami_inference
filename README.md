# origami_inference
Private inference using hardware enclaves
## Folder Structure
Folder|Description|
---|---
slalom| Contains code for baselines and Origami
cGAN-reconstruct-image/split_layer6 |  Contains code for collecting intermediate feature maps used for training c-GAN
cGAN-reconstruct-image/code_split_layer6 | contains code for training c-GAN networks

## Prerequisites
```
Hardware: Intel processor equipped with SGX, Nvidia GPU
Software: Python3.6, TensorFlow, Keras, Intel SGXSDK
```

### To collect intermediate feature maps
```
cd cGAN-reconstruct-image/split_layer6
python36 split_vgg16.py -p "path to the image dataset"
```

### To train the c-GAN networks on intermediate feature maps
```
cd cGAN-reconstruct-image/code_split_layer6
python36 main.py --gpu 0 -i "path to intermediate feature maps"
```
### To run slalom/privacy
```
cd slalom
python -u -m python.slalom.scripts.eval_slalom_base vgg_16 --batch_size=32 --max_num_batches=1 --blinding --use_sgx

```
### To run Origami
```
cd slalom
python -u -m python.slalom.scripts.eval_slalom vgg_16 --batch_size=32 --max_num_batches=1 --blinding --use_sgx
```

### References
```
The code in this project related to Intel SGX is built on top of [Slalom] (https://github.com/ftramer/slalom)
```
