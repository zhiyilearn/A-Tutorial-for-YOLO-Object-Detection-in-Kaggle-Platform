# This tutorial is developed by Zhiyi Li, Kshitiz Dhakal, and Dr. Song Li, from Department of Plant and Environmental Science, Virginia Tech, Blacksburg, VA. It is free to download to teach students to write Jupter Notebook scripts.

We use Open Source keras-yolo3 code from:
         https://github.com/qqwweee/keras-yolo3

1. Preprocessing:
1.1 Merge RGB images with MiCaSense scripts.
      Install Micasense library in micasense directory.
      Install exiftool.exe in PC or Mac by following instructions at:
https://exiftool.org/


      Dataset is located in: preprocsssing/merge_align/dataset
      Input data directory: RGBInput
      Your output data directory: RGBOutput


       Merge process: 
       python  mergealignmentRGB.py


1.2 Draw bounding boxes for images to generate XML file
      Install image label tool for PC based on instructions:
           https://github.com/tzutalin/labelImg
      Label image in PC:
      Input data directory: RGBOutput
      Output data directory: annotation_voc


2. Kaggle Jupyter Notebook
2.1 Create your own kaggle account.

2.2 Upload dataset: 
         click Data in left menu, 
                         select YOUR DATASETS
                         click new Dataset button
                       Give dataset title: tutorialforyolodataset
                       Click Select Files for Upload button to upload zipped file: 
                       tutorialforyolodataset.zip
2.3 Upload Jupyter Notebook scripts
         
        Click Notebooks in left menu, or upload  tutorialforyolo.ipynb file
Select YOUR WORK
Give script name: TutorialForYOLO
            Write scripts in two sections
                    Section 1: Data Preprocessing (This part mainly did off-line)
                        Section 2: Prepare YOLO format, train, evaluation. 
            On right, click Add data button, 
input: select the dataset you select tutorialforyolodataset
Output: /kaggle/working
 (Reason is that this directory you can read/write files)

Section 2 script summary:
    Copy data from input directory to /kaggle/working directory. 
    Prepare YOLO format XML file
    Create anchors. 
    Train process,
    Evaluation process. 
    Prediction 
                                                       
3. Step to run in ARC machine huckleberry1.arc.vt.edu
1. Upload tutorialforyolodataset.zip file to ARC machine and unzip it (unzip tutorialforyolodatasetForArc.zip). (from this directory: /groups/songli_lab/CornImageAnalysis)
   For example /home/Kshitiz/tutorialForYOLO
2. Request resource to use your account. 
                salloc -N 2 --gres=gpu:4  --partition=normal_q --account=Introtogds --exclusive 
               --time=72:00:00
3. Set up environment: 
    module load gcc cuda Anaconda3 jdk
    source activate powerai16_ibm

4. python xml_to_yolo_for_train.py
python xml_to_yolo_for_test.py

5. # Get anchor information
python kmeans.py, #update the results in model_data/yolo_anchors.txt
6. # Train the model
python train.py
7. # Evaluate  the model
python yolo_evaluation.py
8. # Calculate mAP
python yolo_mAP_Calculation.py
