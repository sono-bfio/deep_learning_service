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



# Adding A Model



# Training a model:



