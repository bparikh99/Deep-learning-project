# Face Mask Detection Using faster_r_cnn


## Installation

Preferable Environment for Tensorflow==1.14 & Python==3.7

Clone repo https://github.com/tensorflow/models

Install labelimg tool https://tzutalin.github.io/labelImg/

Download Model to working directory https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf1_detection_zoo.md

Creat Your dataset using & label using https://github.com/tzutalin/labelImg

# Steps To Create Model:

## xml to csv
python xml_to_csv.py

## To generate tf records
### Training
python generate_tfrecord.py --csv_input=images/train_labels.csv --image_dir=images/train --output_path=train.record

### Testing
python generate_tfrecord.py --csv_input=images/test_labels.csv --image_dir=images/test --output_path=test.record


### Model training 

python models/research/model_main.py --logtostderr --model_dir=training/ --pipeline_config_path=training/faster_rcnn_inception_v2_pets.config
 

###Generate inference graph

python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-{{last-epoch-number}}--output_directory inference_graph

### For Good Accuracy

Create A dataset with 1000+ images and observe the loss over time if loss is minimum stop training.

# Testing 

mask-det.py file and change file-folder name 

