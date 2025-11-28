# Platform Expansions

This page is dedicated to documenting the various extensions and plugins available for the TEXTaiLES platform. These extensions enhance the core functionality of TEXTaiLES, allowing developers to customize their experience and add new features as needed.

### Integrate more Machine Learning models for each task

Developers can integrate additional machine learning models for the pre existing tasks following the guidelines provided in the following sections.

#### Adding a new model for Semantic Segmentation

1. To register a new model for Semantic Segmentation, create a new Python file inside the `/Backend/Segmentation/models` and update the `__init__.py` file to include your new model.
2. Update the `models_available_segmentation.csv` on the `/AmalthAI_WebApp/data/` folder.
3. Create a new json following the existing structure in `/Backend/Segmentation/configfiles` and name it using the model name.
4. Update the training options inside the `training_button_segmentation.py` by adding your model to the list of the available models.

Its important to note that the first column of the `models_available_segmentation.csv` file should match the name of the created json file in step 3. In the second column, you can write the display name of the model that will appear in the platform UI.

#### Adding a new model for Object Detection

Currently, AmalthAI is designed to use only YOLO family models using the [Ultralytics](https://github.com/ultralytics/ultralytics) package. Furthermore, the annotation settings are properly configured to work with YOLO models.

If you want to add a new model from the YOLO family, you can do so by following these steps:

1. Create a new Python file for your model inside the `/Backend/ObjectDetection/ultralytics` directory named `yolovX.py` where X is the version. This will be used to train the model. Follow the other pre-existing files as examples.
2. Update the `models_available_object_detection.csv` on the `/AmalthAI_WebApp/data/` folder to include your new model.
3. Update the training options inside the `training_button_object_detection.py` by adding your model to the list of the available models.

#### Adding a new model for Image Classification

1. To register a new model for Image Classification, create a new Python file inside the `/Backend/Classification/models` and update the `model_factory.py` file to include your new model. Follow the other pre-existing registrations as examples.
2. Update the `models_available_classification.csv` on the `/AmalthAI_WebApp/data/` folder to include your new model.
3. Update the training options inside the `training_button_classification.py` by adding your model to the list of the available models.

To ensure proper integration of your new model, make sure it arrives from the Torchvision models. You can refer to the [Torchvision Models Documentation](https://docs.pytorch.org/vision/main/models.html) for more details on available models and their usage.