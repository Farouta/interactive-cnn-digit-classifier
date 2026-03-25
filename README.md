# Interactive PyTorch CNN Digit Classifier & Visualizer

## Overview
This project demonstrates the iterative development of a machine learning model for classifying handwritten digits. It includes an interactive user interface that visualizes real-time probability distributions and internal layer activations (convolutions and pooling) as the user draws.

## Live Demonstration
![Interactive Demo](assets/cnn_visualization.gif)

## Architecture Evolution
The project was built in three phases:

### 1. Baseline Model (Linear Network)
Initially, I implemented a simple linear neural network to establish a baseline performance metric on the MNIST dataset. 

### 2. Architectural Upgrade (CNN)
To better capture the spatial hierarchies inherent in image data, I upgraded the architecture to a Convolutional Neural Network (CNN). This significantly improved validation accuracy over the baseline.

### 3. Engineering for Robustness (Data Augmentation)
Even with the CNN, the model trained strictly on the standard MNIST dataset failed to generalize to real-world inputs drawn via the UI, particularly when digits were drawn off-center or at varying scales.

To solve this, I used a simple PyTorch image transformation pipeline:
* **Resizing & Scaling:** Specifically because the initial model consistently misclassified smallly drawn "0"s as "9"s.
* **Random Translation:** This proved to also help when drawing numbers off center, since the MINST dataset numbers are always centered in the middle.
* **Random Rotation:** This transformation is used to accommodate for rotated numbers, it's worth noting that this rotation should be small (eg. -5;5 degrees) since a "9" is also a "6" upside down.

While these data augmentations only improved the cnn_model's validation tests by 0.2% it improved the it's robustness and accuracy on live UI inputs.
It has also made it prone

##Development Process :

Core Machine Learning: The neural network architectures, PyTorch training pipelines, and custom data augmentation transformations were developed independently.

Visualization Interface: The interactive frontend UI was generated using Claude' Sonnet 4.6 visualize the model's performance.

## Training Results
The CNN model was trained for 50 epochs. 
![Training and Validation Loss](assets/cnn_loss_graphs.png)

### Error Analysis
Below are the misclassified images.
![Misclassified Images](assets/cnn_misclassified_images_snippet.png)

## Tech Stack
* Python
* PyTorch
* CNN Architecture
* Data Augmentation (torchvision.transforms)

## How to Run
1. Clone the repository.
2. Install dependencies: `pip install -r requirements.txt`
3. Open `digit_classifier.ipynb` to view the training pipeline and launch the UI.
