---
linkTitle: new2
title: new2
categories: ["jetson nano"]
---
The error `ModuleNotFoundError: No module named 'cv2'` indicates that the OpenCV library (cv2) is not installed on your system. To resolve this issue, you need to install OpenCV. Below are the steps you can follow to install OpenCV:

### Install OpenCV on Nvidia Jetson Nano

#### Step 1: Update Package Lists and Install Dependencies
Open a terminal and run the following commands to update the package lists and install necessary dependencies:

```bash
sudo apt update
sudo apt install -y libopencv-dev python3-opencv
```

#### Step 2: Check OpenCV Version
You can check the installed OpenCV version using the following Python command:

```bash
python3 -c "import cv2; print(cv2.__version__)"
```

This command should print the installed OpenCV version. If it doesn't print any errors, then OpenCV is successfully installed.

#### Step 3: Test OpenCV Installation
Create a simple Python script (e.g., `test_opencv.py`) and add the following code to test if OpenCV is working:

```python
import cv2

# Read an image from file
image = cv2.imread('path_to_your_image.jpg')

# Display the image
cv2.imshow('Image', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

Replace `'path_to_your_image.jpg'` with the path to an image file on your system.

Save the file and run it:

```bash
python3 test_opencv.py
```

If OpenCV is installed correctly, it should display the image using OpenCV functions.

#### Additional Note:
If you are using virtual environments, make sure your virtual environment is activated when installing OpenCV and running your Python script.

If you encounter any issues or have specific requirements, feel free to provide more details, and I'll assist you further.