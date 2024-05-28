# Motion Detection with OpenCV

This project demonstrates a simple motion detection system using OpenCV and Python. The code captures video from a webcam, processes the video frames to detect motion, and highlights the areas where motion is detected.

## Features

- Capture video from the webcam.
- Convert frames to grayscale and apply Gaussian blur.
- Compute the difference between the current frame and the first frame to detect changes.
- Threshold and dilate the difference image to get the foreground mask.
- Find contours in the thresholded image and draw bounding boxes around moving objects.
- Display the video feed with detected motion highlighted.

## Requirements

- Python 3.6 or higher
- OpenCV
- imutils

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/balapavitra/motion-detection-opencv.git
    cd motion-detection-opencv
    ```

2. Create a virtual environment (optional but recommended):

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3. Install the required packages:

    ```bash
    pip install opencv-python imutils
    ```

## Usage

1. Run the motion detection script:

    ```bash
    python motion_detection.py
    ```

2. The webcam feed will open in a new window. The script will display "Normal" if no motion is detected and "Moving object detected" when motion is detected. Bounding boxes will be drawn around moving objects.

3. Press the `q` key to quit the program.

## Code Explanation

- `cv2.VideoCapture(0)`: Initialize the webcam.
- `imutils.resize(img, width=1000)`: Resize the frame to a width of 1000 pixels for consistent processing.
- `cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)`: Convert the frame to grayscale.
- `cv2.GaussianBlur(grayimg, (21, 21), 0)`: Apply Gaussian blur to the grayscale image to reduce noise and detail.
- `cv2.absdiff(firstFrame, gaussianimg)`: Compute the absolute difference between the current frame and the first frame.
- `cv2.threshold(imgDiff, 25, 255, cv2.THRESH_BINARY)[1]`: Apply a binary threshold to the difference image.
- `cv2.dilate(threshimg, None, iterations=2)`: Dilate the thresholded image to fill in holes.
- `cv2.findContours(threshimg.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)`: Find contours in the thresholded image.
- `cv2.boundingRect(c)`: Get the bounding box for each contour.
- `cv2.rectangle(img, (x, y), (x + w, y + h), (0, 255, 0), 2)`: Draw a rectangle around the detected motion.
- `cv2.putText(img, text, (10, 20), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255), 2)`: Display the status text on the frame.
- `cv2.imshow("camerafeed", img)`: Show the processed video feed.
- `cv2.waitKey(10)`: Wait for 10 milliseconds for a key press. If the `q` key is pressed, break the loop.

## Acknowledgments

- This project uses the OpenCV library for computer vision tasks.
- The `imutils` library is used for additional image processing functions.

