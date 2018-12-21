# KicksHunter
KicksHunter is an iOS application, which implements the CoreML library and a Keras script, designed to identify the model of a shoe in the camera. 
The current script and application for KicksHunter has been trained on five different shoe models: The Adidas Yeezy 350 Boost Cream, The Adidas NMD R1 OG, The Balenciaga Speed Trainer Triple Black, The Nike Air Jordan 1 Retro High OG Chicago and the Vans Old Skool Black and White.


# Demonstration
Images of the working application can be seen below:
![Yeezy](utilities/Demo1.PNG)
![AirJordan](utilities/Demo2.PNG)


# Files
The description of each main file is as follows:
* search_bing_api.py: This file utilizes the Bing API to download and store images of the five Pokemon that will be used in training. The search was repeated five times, with each Pokemon being passed as a query on five separate occasions. All the resultant images are stored in the 'dataset' directory. 
* train.py: This file utilizes the files in the dataset directory to construct a Keras model, utilizing the VGGNet, that can detect which Pokemon is in each image.
* coremlconverter.py: This file converts the Keras model into a CoreML one for use on iOS applications.
* mymodel.mlmodel: This file contains the converted CoreML model.
* KicksHunter: This directory holds the Swift project that implements the model as a real-time iOS application.


# Deconstructing the Process
To replicate the process of creating this application, if one wishes to add modifications or additional shoes, the following commands were run in terminal.

To create the dataset skeleton directory:
```
mkdir dataset
```

To download and create a sub-database for each shoe:
```
python search_bing_api.py --query <"shoe model name"> --output dataset/<shoe-model-name>
```
To acheive this, one must also change the API Key listed in 'search_bing_api.py' to a valid one.


Next, to train the network:
```
python train.py -d dataset -m mymodel.model -l lb.pickle
```

Next, to convert the trained network into a CoreML model:
```
python coremlconverter.py -m mymodel.model -l lb.pickle
```

After this, simply swap this with the existing CoreML model in the XCode Project file, update the labels in the View Controller, and the application is good to go!
