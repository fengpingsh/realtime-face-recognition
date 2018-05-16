Real time face recognition
=======================================================================================================
This is a sister project with the realtime-object-detection, in this project MobileNet-SSD + ncs are used for face detection and recognition. 
Please take a glance at the README in that project first.

# Run
python ncs_realtime_facedetection.py --graph graphs/mobilenetgraph --display 1
--graph: required, point to a graph file that can be loaded by Intel Movodius Netural Compute Stick. You can find more information in 
https://movidius.github.io/ncsdk/  
--confidence: optional, default value is 0.5  
--display: optioanl, default value is zero which means do not display the real time video.  

# Train your own dataset
Please follow the guide in https://github.com/fengpingbaustem/MobileNet-SSD/tree/master/mydataset to train face dataset. After trained the model,
please refer the command provided by https://movidius.github.io/ncsdk/tools/compile.html to convert the model to graph file which can be loaded for NCS.

# Notes
## Convertion to graph
To avoid format error, you should change the header of the prototxt file from 
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

## Reload the graph file
I noticed that after running the object detection(load the graph in realtime-object-detection), if you load the face detection model to perform face 
recognition, you will find no face will be detected at all. But if you load another graph file(vgg model for example), then it works normally, So, I guess
the graph will be stored in ncs and do not load the new one if name are all the same? Just guess :)
