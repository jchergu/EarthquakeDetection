# Earthquake Detection with ESP32 and Detectron2

## Project Overview
This project focuses on developing an automated system for detecting earthquake damage in structures using computer vision. Leveraging Facebook AI's Detectron2 library, a state-of-the-art object detection framework, the system is trained to identify various types of damage from aerial imagery or ground-level photos. The trained model is then deployed as a cloud-hosted API endpoint, enabling real-time damage assessment by external devices like ESP32 microcontrollers.

## Key Features
- **Custom Dataset Preparation**: Utilizes a COCO-formatted dataset of earthquake damage images, split into training, validation, and test sets.
- **Detectron2 Integration**: Implements a Faster R-CNN (Region-based Convolutional Neural Network) model with a ResNet-50-FPN backbone for robust object detection.
- **Advanced Data Augmentation**: Incorporates geometric (flips, rotations, crops) and photometric (brightness, contrast, saturation) augmentations during training to improve model generalization and robustness to varying real-world conditions.
- **Model Training & Evaluation**: Trains the Detectron2 model on a GPU-accelerated environment, saving the best performing model weights.
- **Cloud Deployment**: Deploys the trained model as a FastAPI application, accessible via a secure Cloudflared tunnel.
- **Real-time Inference**: Provides an API endpoint `/upload` for receiving images and performing immediate damage detection, returning the most prominent damage type found.
- **ESP32 Integration**: Designed to be integrated with ESP32 cameras for capturing images and sending them to the deployed cloud inference service.

## Technical Stack
- **Python**: Primary programming language.
- **Detectron2**: Object detection framework.
- **PyTorch**: Deep learning backend.
- **OpenCV (cv2)**: Image processing.
- **FastAPI**: Web framework for building the API.
- **Cloudflared**: Secure tunnel for exposing local server to the internet.
- **Google Colab**: Development and training environment.
- **Google Drive**: Dataset and model storage.

## Dataset
The project uses a custom dataset of earthquake damage images (e.g., `patches_20percent`) annotated in COCO format, categorized into 7 distinct damage classes:
- Crack
- Corrosion/Rebar
- Spalling
- Leaching
- Other Damage
- Debris
- Non-structural

## Setup and Installation
To run this project, you will need:
1.  **Google Colab Environment**: Most of the setup is handled within the Colab notebook.
2.  **Google Drive Access**: Mount your Google Drive to access datasets and store models.
3.  **Detectron2 Installation**: The notebook includes commands to clone and install Detectron2 and its dependencies.
4.  **Cloudflared**: Installed for creating a secure public tunnel to the FastAPI server.

### Running the Notebook
1.  **Mount Google Drive**: Execute the cell to mount Google Drive.
2.  **Install Dependencies**: Run the `pip install` and `git clone detectron2` commands.
3.  **Register Datasets**: Execute cells to register your COCO datasets with Detectron2.
4.  **Configure and Train Model**: Set up the Detectron2 configuration and initiate training. 
5.  **Run Inference**: Test the trained model on sample images.
6.  **Deploy API**: Start the FastAPI server and Cloudflared tunnel to expose your inference endpoint.

## Usage (API Endpoint)
Once deployed, the FastAPI server provides the following endpoints:
- `POST /upload`: Send an image file to this endpoint for damage detection. The server will process the image and update its `latest_ai_result`.
- `GET /result`: Retrieve the most recently detected damage type from the server.

## Example ESP32 Integration (Conceptual)
An ESP32 camera module can capture images and send them to the `/upload` endpoint. The ESP32 can then query the `/result` endpoint to get the damage assessment, allowing for autonomous damage monitoring in remote locations.

## Future Enhancements
- **Improved Model Architectures**: Experiment with more advanced Detectron2 models (e.g., Cascade R-CNN, Mask R-CNN) or other object detection frameworks.
- **Quantization and Edge Deployment**: Optimize the model for deployment on resource-constrained edge devices, potentially running inference directly on the ESP32.
- **Real-time Video Processing**: Extend the system to process video streams for continuous monitoring.
- **More Robust API**: Add authentication, error handling, and more detailed response structures to the FastAPI application.
- **Custom Loss Functions/Metrics**: Implement domain-specific loss functions or evaluation metrics to fine-tune performance for earthquake damage detection.
