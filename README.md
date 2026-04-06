```markdown
# Handwritten Character Recognition (CRNN)

## Project Overview
This project implements a Convolutional Recurrent Neural Network (CRNN) to classify handwritten characters from image data. The model combines the power of Convolutional Neural Networks (CNNs) for feature extraction and Bidirectional Long Short-Term Memory (BiLSTM) networks for sequence processing, making it suitable for tasks involving variable-length sequences or character-level predictions.

## Dataset
The model is trained on a custom dataset of handwritten images, located in `/content/drive/MyDrive/FEATURE-BASED-IMAGES/`. The dataset is expected to be organized into subfolders, where each subfolder represents a distinct class (e.g., `CLASS_0`, `CLASS_1`, etc.).

## Model Architecture
The CRNN model consists of the following components:
-   **CNN Layers**: Multiple `Conv2D` and `MaxPooling2D` layers are used for feature extraction from the input images, followed by `BatchNormalization` and `Dropout` for regularization.
-   **Reshape Layer**: The output from the CNN layers is reshaped into a sequence format suitable for the recurrent layers.
-   **BiLSTM Layers**: A `Bidirectional LSTM` layer processes the sequence features, capturing dependencies in both forward and backward directions.
-   **Dense Layers**: Fully connected `Dense` layers with `BatchNormalization` and `Dropout` form the classifier head, outputting probabilities for each class using a `softmax` activation.

## Preprocessing Steps
The following preprocessing steps are applied to the images:
1.  **Grayscale Conversion**: Images are loaded in grayscale.
2.  **Resizing**: Images are resized to `256x256` pixels.
3.  **Adaptive Thresholding**: `cv2.adaptiveThreshold` is used to binarize the images, robustly handling varying lighting conditions.
4.  **Morphological Operations**: Dilation and inversion are applied to enhance character strokes.
5.  **Normalization**: Pixel values are normalized to `[0, 1]`.

## Training
-   **Batch Size**: `32`
-   **Epochs**: `50`
-   **Optimizer**: Adam with a learning rate of `0.0003`
-   **Loss Function**: `categorical_crossentropy`
-   **Metrics**: `accuracy`
-   **Callbacks**: `EarlyStopping` (patience=10) and `ReduceLROnPlateau` (patience=5) are used to prevent overfitting and adjust the learning rate.

## Prediction and Evaluation
After training, the model's performance is evaluated using:
-   **Test Accuracy**: Reported on the validation set.
-   **Confusion Matrix**: Visualizes the performance of the classification model on a set of test data for which the true values are known.
-   **Classification Report**: Provides precision, recall, and F1-score for each class.

### Personality Mapping
The prediction script includes a custom `print_results` function that maps the predicted classes (e.g., `CLASS_0`, `CLASS_1`) to descriptive personality traits based on the user's specific interpretation of handwritten features.

## Files
-   `training_script.ipynb`: The main notebook containing model definition, training, and evaluation.
-   `prediction_script.ipynb`: Notebook for making predictions on new images.
-   `variables.py`: Python file containing configurable parameters like image dimensions, batch size, and file paths.
-   `model.json`: Model architecture saved in JSON format.
-   `model.weights.h5`: Trained model weights.
-   `label_encoder.pkl`: Pickled `LabelEncoder` object for mapping numerical labels back to class names.

## Usage
1.  **Setup Google Drive**: Mount your Google Drive to access the dataset and save model outputs.
2.  **Install Dependencies**: Ensure all required Python packages (TensorFlow, Keras, OpenCV, scikit-learn, etc.) are installed.
3.  **Configure `variables.py`**: Update paths and parameters in `variables.py` to match your environment and dataset specifics.
4.  **Run Training**: Execute the training script to train the CRNN model.
5.  **Run Prediction**: Use the prediction script to classify new images and interpret the personality traits.

```
