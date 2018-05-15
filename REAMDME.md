A real time face recognition using MobileNet-SSD which includes face detection. As well, I use the Movidius neural compute stick to accerate the calculation.
=======================================================================================================
This is a derived project from https://github.com/fengpingbaustem/realtime-object-detection, I trained my own dataset and convert the param to graph which can
be used by a ncs.

# Run
python ncs_realtime_facedetection.py --graph graphs/mobilenetgraph --display 1
Here the graph is converted by the caffemodel using the guide showed in https://movidius.github.io/ncsdk/
Surely, before running, you need a neural compute stick plugged into your PC or raspberry PI device.

# Train the face dataset
Please follow the guide in https://github.com/fengpingbaustem/MobileNet-SSD/tree/master/mydataset to train face dataset and convert to graph file.

# Notes
## Convertion to graph
You should change the header of the prototxt file from 
*input: "data"*
*input_shape {*
  *dim: 1*
  *dim: 3*
  *dim: 224*
  *dim: 224*
*}*
__to__
*layer {*
  *name: "data"*
  *type: "Input"*
  *top: "data"*
  *input_param {*
    *shape {*
      *dim: 1*
      *dim: 3*
      *dim: 224*
      *dim: 224*
    *}*
  *}*
*}*

