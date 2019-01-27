# GAN-assisted model compression (GAN-MC)

**Related link: [Codes to compute Compression Score](https://github.com/RuishanLiu/Compression-Score)**

Codes for paper [Model Compression with Generative Adversarial Networks](https://arxiv.org/pdf/1812.02271.pdf).

### Introduction 

In a typical compression setting, as much data as possible has been dedicated to training the highly accurate teacher model, leaving little fresh data for training the student model.

To boost student performance and compression efficiency, we propose a simple solution applicable to tabular and image data alike: augment the compression set with synthetic feature vectors generated by a high-quality GAN. These synthetic feature vectors are then labeled with the true outputted teacher class probabilities or logits. We call this approach GAN-assisted model compression (GAN-MC).
  
## Run

### Random Forest GAN-MC on Tabular Data
```bash
python tabular.py
```
We explore how GAN-MC performs when used to compress large random forests for binary classification. 
* The teacher is a random forest classifier with 500 trees, and the student is a regression random forest with one to 20 trees.
* For illustration, here we use MAGIC Gamma Telescope datasets from the UCI Machine Learning Repository. The original dataset can be found at https://archive.ics.uci.edu/ml/datasets/magic+gamma+telescope. 
* The result is compared with MUNGE data augmentation strategy [4].


### Deep Neural Network for GAN-MC on CIFAR-10
```bash
python cifar10.py --p_fake 0.8 --model_path models/cifar10/netG_keras.h5
```
We investigate how GAN-MC performs when used to compress convolutional deep neural network (CNN) classifiers trained on the CIFAR-10 dataset. Codes are built based on https://github.com/chengshengchan/model_compression.

#### Usage
* --p_fake: The mixture of training and GAN data is realized by generating GAN data with probability p_fake

* --model_path: Path to the saved GAN model

#### GAN Model
We have two trained AC-GAN models for people to try
1. models/cifar10/netG_keras.h5: Keras model from https://github.com/King-Of-Knights/Keras-ACGAN-CIFAR10
2. models/cifar10/netG_pytorch.pth: Pytorch model from https://github.com/gitlimlab/ACGAN-PyTorch

Feel free to try your own models. Remember to check the cifar10.py file for specific changes. 

## References

[1] Ba, J. and Caruana, R. Do deep nets really need to be deep? In NIPS 2014.

[2] Hinton, G. E., Vinyals, O., and Dean, J. Distilling the knowledge in a neural network. arXiv 2015.

[3] Odena A, Olah C, Shlens J. Conditional image synthesis with auxiliary classifier gans. arXiv 2016.

[4] Cristian Bucila, Rich Caruana, and Alexandru Niculescu-Mizil. Model compression. In Proceedings of the Twelfth ACM SIGKDD International Conference on Knowledge Discovery and Data Mining, Philadelphia, PA, USA, August 20-23, 2006, pp. 535–541, 2006.

