# Deep-Oversampling-Technique-for-4-level-Acne-Classification-in-Imbalanced-Data
This is a Python implementation of Deep Oversampling Technique for Acne Images Classification in Imbalanced Data.
## Methodology
We assume imbalanced dataset **_S_** with m objects |**_S_**| = **_m_**, as a pair **_S_** = {(**_x_**_i_, **_y_**_i_)}, **_i_** = **1**, ..., **_m_**, where **_x_**_i_ **ϵ _X_** denotes the instance in the **_n_**-dimensional feature space **_X_**={***f***1, ***f***2, ..., ***f***_n_}, and ***y***_i_  ϵ ***Y*** = {**1**, …, ***C***} denotes the class identifier label associated with ***x***_i_. in particular, when ***C*** = 2 we deal with binary classification task. In addition, we define subsets ***S***min ⊂ ***S*** and ***S***maj ⊂ ***S***, where ***S***min is the set of minority objects of classes in ***S***, and ***S***maj is the set of objects of prevailing classes in ***S***, so that ***S***min ∩ ***S***maj = {Φ} and ***S***min ᴜ ***S***maj = {***S***}. Based on these assumptions the problem of acne recognition can be formulated as a 4-type classification task. 
Thereafter, the multiclass classification problem is transformed into a regression task. This transformation helps to reduce possible subjectivity in the assessment of the acne severity at the stage of data annotation. Since the acne levels class have a meaningful ordering, we assign the numeric values from **0** to ***C*** to each of the corresponding ***C*** classes labels. Formally, it presented as follow ***y***  ⊆ ***S*** = {**1**, …, ***C***}→transformation→***y*** ϵ **ℝ**_n_. The values of the class variable are transformed into numbers. A numeric target is corresponding to a level of acne severity.
Thresholding is also used to transform back a regression prediction into a classification prediction ***y'*** ϵ ℝ*n*→transformation→***y'*** ⊆ ***S***, where ***y'*** is a prediction.
The proposed methodology includes dealing with imbalanced images dataset at the data level and feature level. At the data level, the following methods have been used: patch extraction and data augmentation. At the feature level, an oversampling technique has been used to deal with imbalanced data.
Firstly, we extract patches from original images of human faces using one of the two pre-trained models. Then data augmentation, feature extraction, and data oversampling are conducted. Finally, results obtained after oversampling are fed to CNN for model training and evaluation.

![Proposed methodology](https://user-images.githubusercontent.com/53811556/163562251-623506a6-0099-413b-a76c-8f74de256a4a.png) 
Proposed methodology pipeline

### Step 1: Patches extraction 
At the first stage, preliminary processing of images is carried out for capturing skin areas from the face image. The severity of acne does not depend on the location; it depends on the volume and severity of the lesion on the patient's face. From this prospective, the separate patches of the face image should give results that are more informative relatively to the entire face. The result of this step is a dataset ***S*** consisting of m patches extracted from facial images. Each patch inherits the image class label. 
### Step 2: Data augmentation
CNNs are spatially sensitive, which leads to insufficient recognition quality when using a limited number of images for network training. To overcome this issue, we use translation of an image section. The result of this step is a dataset ***S*** consisting of an increased number of patches. Each translated patch inherits the class label of the original patch that was used for augmentation.
### Step 3: Feature extraction
We utilised the transferring learning paradigm and a pretrained ResNet-152 to extract features from training set of acne images. The result of this step is a dataset ***S*** = {(***x***_i_, ***y***_i_)} consisting of the features extracted using the trained model, where ***x***_i_ is the vector of extracted features of the patch ***m***_i_, and ***y***_i_ is the class label which denotes the severity of acne associated with ***x***_i_.
### Step 4: Oversampling
We use oversampling to balance the number of dataset objects for each class. Formally, oversampling can be represented as follows. Any objects generated from the dataset S are denoted as ***E***, with disjoint subsets of ***E***min and ***E***maj representing the minority and majority of the ***E*** objects, respectively, whenever they are applied. The random oversampling pro-cess is implemented by adding a set ***E*** selected from the minority class: for a set of randomly selected minority examples in ***S***min, increase the original set ***S*** by replicating the selected examples and adding them to ***S***. Thus, the number of typical examples in ***S***min increases by |***E***|, and the balance of the class distribution of ***S*** is adjusted accordingly. This provides a mechanism for changing the degree of balance in the distribution of classes to any desired level. The result of this step is a dataset ***S*** = {(***x***_i_, ***y***_i_) consisting of extracted and generated features, where ***x***_i_ is a vector of extracted and generated features of patches ***m***_i_, and ***y***_i_ is the class label associated with ***x***_i_.
### Step 5: Model training 
The extracted and generated features are passed to train a CNN model to classify acne severity. Model evaluation is implemented on validation data.  

## Experiment
For this study the [ACNE04](https://github.com/xpwu95/ldl) the open dataset was used. The [ACNE04](https://github.com/xpwu95/ldl) includes 1457 face images and expert annotations according to the Japanese rating scale. The dataset has the following acne severity annotations: level 0 – Mild, level 1 – Moderate, level 2 – Severe, level 3 – Very severe. All images were taken at an angle of approximately 70 degrees from the front of the patient and manually annotated by experts.
A study by [Microsoft](https://github.com/microsoft/nestle-acne-assessment) was used as a benchmark for the experiment. Steps 1, 2, 3 have been implemented using the [source code that has been developed for the collaborative project between Microsoft and Nestle Skin Health](https://github.com/microsoft/nestle-acne-assessment). Our modification of Steps 4, 5 is presented in [Steps4,5.ipynb](https://github.com/beloborodova-t/Deep-Oversampling-Technique-for-4-level-Acne-Classification-in-Imbalanced-Data/blob/main/Step4%2C5.ipynb) code.
Step 1 utilizes two pre-trained models: [shape_predictor_68_face_landmarks model](https://github.com/davisking/dlib-models) or the [One Eye model](https://github.com/opencv/opencv/blob/master/data/haarcascades/haarcascade_eye.xml).
Sliding translation as augmentation technique has been used at the Step 2.
At the Step 3 the feature extraction from each patch is carried out using the [ResNet-152](https://www.cntk.ai/Models/Caffe_Converted/ResNet152_ImageNet_Caffe.model) model. 
Data oversampling has been conducted with Synthetic Minority Oversampling Technique (SMOTE). 
Data generated at the oversampling stage are used to train a CNN model.

### How to Cite
If you find this work helpful, please cite it as
Biloborodova Т., Koverha M., Skarga-Bandurova I., Yevsieieva Ye., Skarha-Bandurov I. Deep Oversampling Technique for 4-level Acne Classification in Imbalanced Data. Proceedings of International Conference on Information Technology and Applications - ICITA 2021. Lecture Notes in Networks and Systems. P.
