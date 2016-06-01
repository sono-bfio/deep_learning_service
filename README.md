# Bitfusion Mobile Inference API

This API is based on: 

https://github.com/NVIDIA/gpu-rest-engine

To Summarize:
GPUs are efficient parallel processors that can deliver low-latency response times for services responding to arbitrary incoming requests.

The NVIDIA GPU REST Engine (GRE) is a critical component for developers building low-latency web services. GRE includes a multi-threaded HTTP server that presents a RESTful web service and schedules requests efficiently across multiple NVIDIA GPUs. The overall response time depends on how much processing you need to do, but GRE itself adds very little overhead and can process null-requests in as little as 10 microseconds.



Example call:
```
host="EC2 instance IP"
curl \
   --verbose \
  -X POST \
   --data-binary @images/1.jpg \
   http://${host}:8000/api/classify
```
## Starting the GPU Rest Engine via init script:

```
sudo service gpurestengine start
```

For the example model provided on the system you can select one of the training models:
 * CaffeNet
 * AlextNet
 * GoogleNet
 
If you have trained your own model you can update the variables to point to your definitions.

Example "/etc/default/gpurestengine" provided:

```
# Caffe Model - Default
DEPLOY_PROTEXT="caffe/models/bvlc_reference_caffenet/deploy.prototxt"
CAFFE_MODEL="caffe/models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel" \
MEAN="caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
SYNSET_WORDS="caffe/data/ilsvrc12/synset_words.txt"

# Alexnet Model
#DEPLOY_PROTEXT="caffe/models/bvlc_alexnet/deploy.prototxt"
#CAFFE_MODEL="caffe/models/bvlc_alexnet/bvlc_alexnet.caffemodel"
#MEAN="caffe/data/ilsvrc12/imagenet_mean.binaryproto"
#SYNSET_WORDS="caffe/data/ilsvrc12/synset_words.txt"

# Googlenet Model
#DEPLOY_PROTEXT="caffe/models/bvlc_googlenet/deploy.prototxt" \
#CAFFE_MODEL="caffe/models/bvlc_googlenet/bvlc_googlenet.caffemodel" \
#MEAN="caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
#SYNSET_WORDS="caffe/data/ilsvrc12/synset_words.txt"
```

## Starting GPU Rest Engine via docker



This would start server with bvlc reference caffe model trained with ilsvrc12 dataset. Server listens on port 8000

```
nvidia-docker run --name=gpurestengine --net=host --rm \
  863665633681.dkr.ecr.us-east-1.amazonaws.com/bitfusion/infratech:gpurestengine \
    inference \
      "caffe/models/bvlc_reference_caffenet/deploy.prototxt" \
      "caffe/models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel" \
      "caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
      "caffe/data/ilsvrc12/synset_words.txt"
```

This would start server with bvlc alexnet model trained with ilsvrc12 dataset. Server listens on port 8000

```
nvidia-docker run --name=gpurestengine --net=host --rm \
  863665633681.dkr.ecr.us-east-1.amazonaws.com/bitfusion/infratech:gpurestengine \
    inference \
      "caffe/models/bvlc_alexnet/deploy.prototxt" \
      "caffe/models/bvlc_alexnet/bvlc_alexnet.caffemodel" \
      "caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
      "caffe/data/ilsvrc12/synset_words.txt"
```

This would start server with googlenet alexnet model trained with ilsvrc12 dataset. Server listens on port 8000
```
nvidia-docker run --name=gpurestengine --net=host --rm \
  863665633681.dkr.ecr.us-east-1.amazonaws.com/bitfusion/infratech:gpurestengine \
    inference \
      "caffe/models/bvlc_googlenet/deploy.prototxt" \
      "caffe/models/bvlc_googlenet/bvlc_googlenet.caffemodel" \
      "caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
      "caffe/data/ilsvrc12/synset_words.txt"

```

# Adding A Model

A person could train ther own model and deploy it in a similar fashion. Good place to start is the following for training with imagenet: http://caffe.berkeleyvision.org/gathered/examples/imagenet.html


# Training a model:

To train on your own dataset you can follow the steps outlined here: https://github.com/BVLC/caffe/issues/550


