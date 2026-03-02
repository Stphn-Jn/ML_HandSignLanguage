
# Hand Sign Language Recognition (A-Z)

A custom-trained Machine Learning pipeline that detects and translates American Sign Language (ASL) alphabets in real-time using your webcam! 

This project uses **MediaPipe** to extract 3D hand landmarks and a **Scikit-Learn Random Forest Classifier** to recognize the unique skeletal structure of each hand sign. 

## Features
* **Custom Dataset Creation:** Easily collect your own images via webcam to train the model exactly how you sign.
* **Fast Training:** Uses a lightweight Random Forest model instead of a heavy deep-learning image classifier, meaning it trains in seconds.
* **Real-Time Inference:** Smooth, instant letter recognition drawn directly onto your live video feed.
* **UI-Optimized Confidence:** The on-screen UI is built for fast-snapping, confident predictions to make demonstrations look incredibly polished and responsive.

---

## Prerequisites & Installation

To run this project, you will need **Python** installed on your computer. 

1. Clone or download this repository to your local machine.
2. Open your terminal (Command Prompt, PowerShell, or VS Code Terminal) and navigate to the project folder.
3. Install the required Python extensions/libraries by running this exact command:

```bash
pip install opencv-python mediapipe==0.10.14 scikit-learn numpy

```

*(Note: We specifically use MediaPipe `0.10.14` as newer versions occasionally have protobuf conflicts on Windows).*

---

## How to Use (Step-by-Step)

The project is broken down into four simple scripts. Run them in this exact order:

### Step 1: Collect Data

```bash
python 1_collect_img.py

```

This script opens your webcam. It will prompt you to prepare for class `0` (Letter A).

* Make the sign for "A" in front of the camera.
* Press the **'Q'** key on your keyboard to rapidly snap 100 images.
* **Pro-tip:** While it is taking the 100 pictures, slightly move and tilt your hand around the frame to give the AI better, more diverse data.
* Repeat this for all 26 classes (A through Z).

### Step 2: Create the Dataset

```bash
python 2_create_dataset.py

```

This script reads your newly collected images, uses MediaPipe to map out the 21 joints of your hand, normalizes the math, and packages it all neatly into a `data.pickle` file.

### Step 3: Train the Model

```bash
python 3_train_classifier.py

```

This feeds your mapped hand coordinates into a Random Forest Classifier. It will print out your training accuracy (hopefully 99%+) and save the trained brain as `model.p`.

### Step 4: Real-Time Inference

```bash
python 4_inference.py

```

The grand finale! This opens your webcam and draws a live skeleton over your hand. Make a sign, and it will instantly draw a bounding box, guess the letter, and display the confidence percentage. Press **'Q'** to exit.

---

## Project Structure

* `1_collect_img.py` - Script to capture training images.
* `2_create_dataset.py` - Script to extract hand landmarks and create `data.pickle`.
* `3_train_classifier.py` - Script to train the AI and generate `model.p`.
* `4_inference.py` - Script to run the live webcam tester.
* `/data` - (Auto-generated) Folder where your webcam images are saved.
* `data.pickle` - (Auto-generated) The processed landmark data.
* `model.p` - (Auto-generated) The trained Machine Learning model.

---

## Known Limitations (ASL 'J' and 'Z')

Because this model relies on static, single-frame images rather than analyzing video motion over time, dynamic signs might be tricky. In ASL, the letters **J** and **Z** require motion (drawing the shape in the air). The model may occasionally confuse 'J' with 'I', or 'Z' with 'D' or '1', as their static hand positions look very similar!
