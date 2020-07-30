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
 

### Generate inference graph

python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-{{last-epoch-number}}--output_directory inference_graph

I have taken only 1500 steps , steps can be increased!

### For Good Accuracy

Create A dataset with 1000+ images and observe the loss over time if loss is minimum stop training.

# Testing 

mask-det.py file and change file-folder name 

![Screenshot (17)](https://user-images.githubusercontent.com/59947941/88922986-9b3ee200-d28e-11ea-9a5b-b96138160ff6.png)
![Screenshot (18)](https://user-images.githubusercontent.com/59947941/88923005-a0039600-d28e-11ea-9b33-dd2b7266e782.png)
## Lets Try!!
### Result Can be Improve by taking training for more ephocs 
![Screenshot (15)](https://user-images.githubusercontent.com/59947941/88923011-a2fe8680-d28e-11ea-81b1-84e32c5bf744.png)

