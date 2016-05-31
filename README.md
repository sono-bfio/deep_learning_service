# mobile_inference_api
Mobile Inference API based on nvidia GPU rest engine

This API is based on: 

https://github.com/NVIDIA/gpu-rest-engine

Example call:
```
host="EC2 instance IP"
curl \
   --verbose \
  -X POST \
   --data-binary @images/1.jpg \
   http://${host}:8000/api/classify
```

## Starting the docker container manually

```
nvidia-docker run \
  --name=gpurestengine \
  --net=host \ # Map ports externally
  --rm \ # remove the container after it is stopped
  -e DEPLOY_PROTEXT="/caffe/models/bvlc_reference_caffenet/deploy.prototxt" \
  -e MODEL_NAME="/caffe/models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel" \
  -e BINARY_PROTO="/caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
  -e SYNSET_WORDS="/caffe/data/ilsvrc12/synset_words.txt" \
  863665633681.dkr.ecr.us-east-1.amazonaws.com/bitfusion/infratech:gpurestengine
```

## Starting the server in different modes:
#this is how we start the server the syntax is 
```
inference \
  {caffe/model/model_name/deploy.prototext} \
  {caffe/model/model_name/model_name.caffemodel} \
  {caffe/data/image_set/*.binaryproto} \
  {caffe/data/image_set/synset_words.txt}
```

#this would start server with bvlc reference caffe model trained with ilsvrc12 dataset. Server listens on port 8000
```
inference \
  "caffe/models/bvlc_reference_caffenet/deploy.prototxt" \
  "caffe/models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel" \
  "caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
  "caffe/data/ilsvrc12/synset_words.txt"
```

#this would start server with bvlc alexnet model trained with ilsvrc12 dataset. Server listens on port 8000
```
inference \
  "caffe/models/bvlc_alexnet/deploy.prototxt" \
  "caffe/models/bvlc_alexnet/bvlc_alexnet.caffemodel" \
  "caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
  "caffe/data/ilsvrc12/synset_words.txt"
```

#this would start server with googlenet alexnet model trained with ilsvrc12 dataset. Server listens on port 8000

```
inference \
"caffe/models/bvlc_googlenet/deploy.prototxt" \
"caffe/models/bvlc_googlenet/bvlc_googlenet.caffemodel" \
"caffe/data/ilsvrc12/imagenet_mean.binaryproto" \
"caffe/data/ilsvrc12/synset_words.txt"

```
# Adding A Model



# Training a model:



