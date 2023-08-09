# Sky_Detection

This ai can detect whither or not it's seeing a plane, a drone, or a bird using the imagenet. Runs on a Jetson Nano Developer Kit 4GB.  

![add image descrition here](direct image link here)

## The Algorithm

The AI trains on a data set that has multiable images of bird, drones, and planes. The dataset follows the 10 80 10 rule where 10% goes to testing, 10% goes to val, and 80% goes to training. 
-2563 images in total
-563 bird images
-1000 drone images
-1000 plane images

## Running this project
## Setting Up Jetson Nano
 1.Click on the green icon at the bottom left of your screen to go to the SSH menu. 
 2.Click on + Add New SSH Host.
 3.To add a new host Enter ssh nvidia@x.x.x.x, replacing x.x.x.x.x with yourIP address (You can find this on the mobile hotspot on your computer).
 4.Pick the first configuration file.
 5.Click Connect.
 6.Choose Linux as the operating system.
 7.Click Continue.
 8.Enter your Jetson Nano login, by defualt the username and password should be nvidia 
 9.Select Open Folder and navigate to jetson-inference.
10.Click Yes, I trust the authors to access and start working on your projects in this directory.

## Setting Up the Data Set
1.Go to jetson-inference/python/training/classification/data.
2.Extract the dataset ZIP file.
3.In the data directory create a new folder named Sky_Detection. 
4.Add three folders within the Sky_Detection directory: test, train, val, and a file named labels.txt.
5.In the train directory create 3 folders named recyclable, organic, and trash. Repeat this for test and val.
6.Distribute the images from your ZIP file among these folders, with 80% in the train folder, 10% in the val folder, and 10% in the test folder.
## Running the Docker Container
1.Go to the jetson-inference and run this command ./docker/run.sh.
2.Once inside the Docker container, go to jetson-inference/python/training/classification.
## Training the Ai
1.Run the training script with the following command: python3 train.py --model-dir=models/Name of your model --batch-size=4 --workers=4 --epoch=1 data/waste_detect Replace ANY_NAME_YOU_WANT with your desired output file name. This process may take quite some time.
2.You can change the batch size, workers, and epochs to improve the Ai
3.You can stop the process at any time using Ctl+C.
## Test the Ai
1.Press Ctrl + D in the terminal to exit Docker.
2.Go back to jetson-inference/python/training/classification.
3.Check if the model exists by executing ls models/The name of your model/. You should see a file named resnet18.onnx.
4.Set the NET and DATASET variables: NET=models/The name of your model DATASET=data/waste_detect
5.To test the AI with an image run this command imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/Direction_To_The_Image_You_Want_To_Test Result_Name
Example:imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/bird/01.jpg birdtest.jpg

## Congrats on following the directions!!!!
[View a video explanation here](video link)
