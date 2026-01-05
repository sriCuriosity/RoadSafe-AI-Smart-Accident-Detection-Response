# Accident Detection System

## Project Report

### 1. Introduction
This project aims to detect accidents in real-time using computer vision and deep learning techniques. It utilizes a Convolutional Neural Network (CNN) to classify video frames as either "Accident" or "No Accident". When an accident is detected with high probability, the system triggers an alarm, captures a photo, and can initiate an emergency call via Twilio.

### 2. Features
- **Real-time Detection**: Processes video feed (from camera or file) to detect accidents.
- **Deep Learning Model**: Uses a trained CNN model for accurate classification.
- **Visual & Audio Alerts**:
    - Draws a bounding box around the detected region.
    - Displays the prediction and probability on the screen.
    - Plays a beep sound when an accident is detected (Windows only).
    - Pops up a GUI alert window requiring user interaction.
- **Emergency Response**:
    - **Photo Capture**: Automatically saves a snapshot of the accident scene.
    - **Twilio Integration**: Capable of making automated calls to emergency contacts/ambulance.
- **GUI Interface**: A Tkinter-based alert window allows the user to confirm the accident or cancel the alarm.

### 3. Functionalities

- **`camera.py`**: The main application logic. It handles video capture, frame processing, model inference, alerting, and Twilio integration.
- **`detection.py`**: Contains the `AccidentDetectionModel` class responsible for loading the trained model (from JSON and weights) and performing predictions.
- **`accident-classification.ipynb`**: A Jupyter Notebook used for training the CNN model on an accident dataset. It generates `model.json` and `model_weights.keras`.
- **`main.py`**: A simple entry point to start the application.

### 4. Prerequisites

- Python 3.x
- Required Python packages:
    - `opencv-python`
    - `numpy`
    - `tensorflow` (or `keras`)
    - `twilio`
    - `Pillow`
    - `pandas` (for the notebook)
    - `matplotlib` (for the notebook)

**Note:** The audio alert uses `winsound`, which is specific to Windows. For other operating systems, this part of the code needs modification.

### 5. Usage Steps

#### Step 1: Installation
1.  Clone the repository.
2.  Install the required dependencies:
    ```bash
    pip install opencv-python numpy tensorflow twilio Pillow pandas matplotlib
    ```

#### Step 2: Configuration
Open `camera.py` and update the following configurations:

1.  **Video Source**: Change `"test_video_path"` to the path of your video file (e.g., `"test_video.mp4"`) or `0` for the webcam.
    ```python
    video = cv2.VideoCapture("test_video.mp4")
    ```
2.  **Twilio Credentials** (Optional but recommended for emergency calling):
    Replace the placeholders with your actual Twilio credentials.
    ```python
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_account_auth_token"
    # Update to and from numbers in client.calls.create(...)
    ```
3.  **GIF Path**: Update `gif_path` in `show_alert_message` function to point to a valid image/gif for the alert window.

#### Step 3: Model Weights
Ensure `model.json` and `model_weights.keras` are present in the directory. If `model_weights.keras` is missing, you need to train the model:
1.  Open `accident-classification.ipynb`.
2.  Download the dataset (as referenced in the notebook) and place it in the `data/` folder.
3.  Run all cells to train the model and generate `model_weights.keras`.

#### Step 4: Running the Application
Run the main script:
```bash
python main.py
```

- The application will open a video window showing the detection results.
- If an accident is detected (>99% probability):
    - A photo will be saved to the `accident_photos` directory.
    - An alarm will sound.
    - An alert window will pop up.
- Click "Call Ambulance" to trigger the Twilio call or "Cancel" to dismiss.
- Press 'q' to quit the application.
