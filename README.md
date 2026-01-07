# WIDS 5.0 Midterm Report


## How the Algorithm Works (Theoretical Understanding)

During this project, I studied the "DeepFace" pipeline and how modern Face Recognition algorithms process images. The system follows these four key steps:

1. Face Detection (HOG & CNN)
The system first locates the face in the image. It uses Histogram of Oriented Gradients (HOG) to identify patterns of light and dark that look like a face.

2. Face Alignment
To ensure accuracy, the algorithm figures out the pose of the face (finding specific landmarks like the chin and nose) and centers the image.

3. Face Encoding (The "Deep Learning" Part)
This is the core of the project. The image is passed through a deep neural network trained to convert facial features into a set of 128 unique measurements (embeddings). No matter the lighting or angle, the network generates a similar list of numbers for the same person.

4. Matching (Euclidean Distance)
The system compares the 128 measurements of the live face with the known faces in the database. It calculates the mathematical distance between them. If the numbers are close enough, it confirms the identity.

## How the Code Works

The code is divided into four main parts:

### 1. Training and Encoding
The script looks into the "train" directory. It loads every image found there and converts them into "encodings." An encoding is a list of 128 measurements that represent the unique features of a face. This acts as the database for the system.

### 2. Video Capture
The code initiates the webcam using OpenCV. To ensure the video runs smoothly and maintains a high frame rate, the input frames are resized to 1/4th of their original size before processing.

### 3. Face Matching
For every frame in the video:
- The system detects face locations and generates encodings for the current frame.
- It compares these new encodings against the known list created in step 1.
- It calculates the mathematical distance between the faces. The lower the distance, the better the match.

### 4. Visual Output
If the distance is low enough to be a match:
- The code retrieves the filename of the matching image.
- It draws a rectangle around the face on the video feed.
- It writes the name of the person on the screen.

## Prerequisites

To run this code, the following Python libraries are required:
- numpy
- opencv-python
- face-recognition

## How to Run

1. Create a folder named "train" in the same directory as the script.
2. Place images of the people you want to recognize inside the "train" folder. Name the files with the person's name (e.g., "San.jpg").
3. Run the python script.
