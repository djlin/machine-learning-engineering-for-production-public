# Things to fix to make it work

* /Users/[user id]/miniforge3/envs/mlep-w1-lab/lib/python3.9/site-packages/cvlib/object_detection.py
 
1. Fix (line 30)
        def get_output_layers(net):
    
            layer_names = net.getLayerNames()
            # output_layers = [layer_names[i[0] - 1] for i in net.getUnconnectedOutLayers()]
            output_layers = [layer_names[i - 1] for i in net.getUnconnectedOutLayers()]

2. Fix 

        def detect_common_objects(image, confidence=0.5, nms_thresh=0.3, model='yolov4', enable_gpu=False):
            indices = cv2.dnn.NMSBoxes(boxes, confidences, confidence, nms_thresh)

            # for i in indices:
            #     i = i[0]
            #     box = boxes[i]
            #     x = box[0]
            #     y = box[1]
            #     w = box[2]
            #     h = box[3]
            for i in indices.flatten():
                (x, y) = (boxes[i][0], boxes[i][1])
                (w, h) = (boxes[i][2], boxes[i][3])

** Same fix for

        def detect_objects(self, image, confidence=0.5, nms_thresh=0.3,
            enable_gpu=False):

3. Fix

        class YOLO:

            def __init__(self, weights, config, labels, version='yolov3'):

                # self.output_layers = [layer_names[i[0] - 1] for i in self.net.getUnconnectedOutLayers()]
                self.output_layers = [layer_names[i - 1] for i in self.net.getUnconnectedOutLayers()]

