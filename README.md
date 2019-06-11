# bone_analysis
    This project is used to analize whether there is an Atypical Femur Fracture in the uploaded X-ray.
## configuration environment
    Graphics card: Nvidia MX150
    OS: Windows 10
    Driver: 
      CUDNN 7.6.0
      CUDA 10.0
    Anaconda 3.7
    Tensorflow 1.14
    FLASK 1.0.2
## training processing
   1. use xml_to_csv.py to transfer the labelled img to csv
   2. use generate_tfrecord.py for training set and testing set to generate train.record and test.record
   3. Execute the command line   
      python model_main.py \
      --pipeline_config_path=training/ssd_mobilenet_v1_coco.config \
      --model_dir=training \
      --num_train_steps=80000 \
      --num_eval_steps=2000 \
      --alsologtostderr
   4. use export_inference_graph.py to export the model
       python export_inference_graph.py \ 
       --input_type image_tensor \ 
       --pipeline_config_path training/ssd_mobilenet_v1_coco.config \  
       --trained_checkpoint_prefix training/model.ckpt-80000 \  
       --output_directory bone_model
  ## use web application
      execute the command line:
      set FLASK_APP=app.py
      set FLASK_DEBUG=1
      flask run --host=0.0.0.0
     
