# Building a Facial Recognition System at the Edge

In this project, my team performed transfer learning on FaceNet at the edge using Nvidia Jetson TX2 for better user privacy and data security. This repo is forked from the [project main repo](https://github.com/adamxjohns/w251project) hosted by one of the teammate's GitHub.

The [project white papar](https://github.com/adamxjohns/w251project/blob/master/w251%20final%20project%20report%20final.pdf)

## Requirement

* Nvidia Jetson TX2
* Jetpack 4.3 (Docker is pre-installed)
* Pre-trained Keras FaceNet model provided by [Hiroki Taniai](https://github.com/nyoki-mtl/keras-facenet)
## Steps

Note:
* All steps if not specify should be performed on Jetson TX2 
* Refer to the directory structure for the locations to store the preprocessing results

-- repo root dir  
   |-- data  
   |   |-- videos (the directory for videos of the identities used for training)   
   |   |   |-- train (videos for training)   
   |   |   |-- val (videos for validation)   
   |   |   |-- test (videos for testing)   
   |   |   ...    
   |   |-- images (the directory storing the frames extracted from videos)   
   |   |   |-- train (images for training)   
   ... |   |   |-- identity_1 (the directory containing the frames of the identity_1)   
       |   |   |-- identity_2 (similar to above)   
       |   |   ...   
       |   |-- val (images for validation)   
       |   ...   
       |-- faces (the directory storing the aligned face images)  
       |   |-- train (images for training)  
           |   |-- identity_1 (the directory containing the aligned images of the identity_1)   
           |   |-- identity_2 (similar to above)   
       |   ...  
       |-- embeddings (directory to store the embeddings by FaceNet)  
           |-- process_1 (the directroy containing the embeddings generated by certain combination of process)   
           |-- process_2 (similar to above)  
           ...  

### Preprocess Data
1. Use any device capable of recording videos to record short videos (1-2 minutes) of the people to train the classifier and save it to the data/video folder under the repo root folder and name the video by the person's name as the label. 
2. On TX2, cd into the root directory of this repo which is also where the data pre-processing notebook ([data_preprocessing.ipynb](https://github.com/adamxjohns/w251project/blob/master/data_preprocessing.ipynb))
3. Run the container with `docker run -v $PWD:/notebooks -p 8888:8888 -d --rm erikhou/final_project_keras:2.0`
4. Run the command `docker logs <your contain id>` to access the link with token for the juypter notebook server
5. Follow the steps in [data_preprocessing.ipynb](https://github.com/adamxjohns/w251project/blob/master/data_preprocessing.ipynb) to extract and align the face images for fine-tuning FaceNet. To skip fine-tuning FaceNet and train the SVM classifier directly, follow the steps in the last section to code the aligned face images and save the embeddings.

### Transfer Learning on validation
1. Use the same container in Preprocessing Data
2. Open notebook, [facenet_fine_tuning.ipynb](https://github.com/adamxjohns/w251project/blob/master/facenet_fine_tuning.ipynb)
3. Follow the steps to fine-tune the top two layers of FaceNet with the preprocessed face images

### Train Face Classifier
1. Use the same container in Preprocessing Data
2. Open notebook, [classifier_training.ipynb](https://github.com/adamxjohns/w251project/blob/master/classifier_training.ipynb)
3. Follow the steps to train the SVM classifier with the face embeddings

### Code for Demo
1. On TX2, cd into the root directory of this repo.
2. Run the container with `docker run --net=host -e DISPLAY=$DISPLAY --privileged -v $PWD:/notebooks -p 8888:8888 -d --rm --env QT_X11_NO_MITSHM=1 -it erikhou/final_project_tx2:2.0 bash`
3. Run the command `docker logs <your contain id>` to access the link with token for the juypter notebook server
4. Run the code blocks in [model_integration.ipynb](https://github.com/adamxjohns/w251project/blob/master/model_integration.ipynb)
to intiate demo.

