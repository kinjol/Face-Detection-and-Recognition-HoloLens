# Face-Detection-and-Recognition-HoloLens
Facial detection and recognition application for the Microsoft HoloLens with anti spoofing capabilities.

Interface

By default, it looks for faces and tries to recognize them. If it does, he person’s name is displayed alongside. If it doesn’t, “unknown” is displayed.


The UI consists of 4 buttons:

⦁	Add Person: 
  
  -	On clicking, the application asks you to enter the name of the person being collected.
  
  -	On clicking OK, the application starts collecting the faces for the respective person. The collected face is displayed at the top right corner.

⦁	Train:
  
  -	When enough faces have been collected, the application prompts you to click the Train button.
  
  -	On clicking, the application trains the model using the collected faces and it starts recognizing faces again.

⦁	Save:
  
  -	On clicking, the application saves the trained model and a list in which the names have been stored.
  
  -	Click this every time you add a new person.

⦁	Delete All:
  
  -	Deletes all saved data


How it works

Detection

The facial detection in this application uses the Haar Cascade classifier. This classifier is used for the detection of haar- like features.
It is a common observation that among all faces the region of the eyes is darker than the region of the cheeks. Therefore, a common Haar feature for face detection is a set of two adjacent rectangles that lie above the eye and the cheek region. The position of these rectangles is defined relative to a detection window that acts like a bounding box to the target object (the face in this case).

Recognition

The recognition part works using the Local Binary Pattern Histograms (LBPH) algorithm.
After extracting, resizing and converting the faces to grayscale the model is trained with these faces. 
Local Binary Pattern is a simple yet very efficient texture operator which labels the pixels of an image by thresholding the neighbourhood of each pixel and considers the result as a binary number. Then the threshold pixel is replaced by this decimal value and this process is repeated for all pixels. This algorithm eliminates the variations caused by lighting conditions.

Spoof Detection

I tried using 2 approaches: 

1.	Recording changes with respect to time:
  
2 consecutive collected faces are taken and their similarity is computed. A real face is found to have a higher value while a fake image is found to have a lower value. The optimal threshold turned out to be 0.41. A mean of 5 such cases gives more stable results. Results were accurate enough to be implemented into the final application.


2.	Detecting eye blinks in a given amount of time:
  
It has been found that a person blinks 1 – 2 times within 5 seconds. Hence real faces can be distinguished from fakes within 5 seconds. Here I used 2 different Haar cascades for eye detection. The default cascade can detect open eyes but not closed eyes. A separate cascade called 2Splits can detect open as well as closed eyes. Hence if the default cascade doesn’t detect an eye but the second one does, it is registered as a bink.

