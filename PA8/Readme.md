
# Programming Assignment 8: CNN Forward Layer GPU Implementation Optimization

## Objective

This is the third part of a three part project implementing and optimizing the forward pass of a convolution layer using CUDA. Convolutional layers are the primary building blocks of convolutional neural networks (CNNs), which are used for tasks like image classification, object detection, natural language processing and recommendation systems. 

You will be working with a modified version of the LeNet5 architceture shown bellow:

![LenetImage](https://lh5.googleusercontent.com/84RlneM7JSDYDirUr_ceplL4G3-Peyq5dkLJTe2f-3Bj9KuWZjsH2A9Qq5PO5BRLrVfWGPnI3eQu8RkTPgyeUf9ZOWY9JbptVJy9LceAyHRn-O0kbzprx88yb82a5dnCR7EDP7n0)

You can read about the original network:

*Source: http://yann.lecun.com/exdb/publis/pdf/lecun-01a.pdf*

Your optimized CUDA implementation of the convolutional layer will be used to perform inference for layers C1 and C3 (shown in red) in the figure above. This leverages the [mini-dnn-cpp](https://github.com/iamhankai/mini-dnn-cpp) (Mini-DNN) framework for implementing the modified LeNet-5.

## Input Data

The network will be tested on the [Fashion MNIST dataset](https://github.com/zalandoresearch/fashion-mnist) which contains 10,000 single channel images each of dimensions 86x86 but we will only use 1000 of these at a time. The output layer consists of 10 nodes, where each node represents the likelihood of the input belonging to one of the 10 classes (T-shirt, dress, sneaker, boot, etc).

## Instructions

At this point you have already completed a GPU implementation of your convolutional layer.

Here is a list of possible optimizations:
* Shared Memory convolution
* Weight matrix (kernel values) in constant memory
* Tuning with restrict and loop unrolling (considered as one optimization only if you do both)
* Sweeping various parameters to find best values (block sizes, amount of thread coarsening)
* Exploiting parallelism in input images, input channels, and output channels.
* Multiple kernel implementations for different layer sizes
* Input channel reduction: tree
* Input channel reduction: atomics
* Fixed point (FP16) arithmetic
* Using Streams to overlap computation with data transfer
* Kernel fusion for unrolling and matrix-multiplication
* An advanced matrix multiplication algorithm (register-tiled, for example)
* Using Tensor Cores to speed up matrix multiplication
* ...
If you wish to use an optimization not listed here, please consult a course staff member.

## How to Compile

The `src/layer/custom/new-forward.cu` file contains the code for the programming assignment. There is a Makefile included which compiles it and links it with the libgputk CUDA library automatically. It can be run by typing `make m2` from the PA8 folder. It generates a `m2` output executable.

## How to test

Use the `make run` command to test your program which will run your program on a batch size of 1000 images. This will automatically compile your source (equivilent to executing `make m2` and then running `./m2 1000`).

## Test Output 

You will need to checkout a GPU for this assignment, but please avoid editing while accessing a device. For timing consistency check out a 1080ti as in the following command. However, for testing you can use any device you please. 
`launch.sh -g 1 -s -i ucsdets/nvcr-cuda:latest -v 1080ti`

The accuracy of your implementation should meet the 0.886 that our implementation does.

## Report

In lieu of a quiz you will writeup your optimizations, their motivations, pointers or copy of relevent code, and what they accomplish.

## Submission and Grading

Submit the src/layer/custom/new-forward.cu file on gradescope as well as your writeup. This is the only file you should have modifed. The performance of your code will be the basis of 60% of the total grade on PA8, with the remaining 40% accounted for by your writeup. The top 25% performance students will receive full credit, and the remaining students will be assigned equal or less credit depending on performance compared to top 25%.  

## Credit

This project is originally from UIUC ECE408 and builds off a number of open source projects including the Fashion MNIST dataset, mini-dnn-cpp, and the Eigen project.
