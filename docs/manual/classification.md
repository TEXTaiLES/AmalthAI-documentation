# Classification Mode
In classification mode, the model assigns a single label to an entire image, indicating the primary object or scene depicted. This allows the user to train the model to recognize and categorize images based on their content.

### Dataset Creation
To start creating a dataset for classification, you need to organize your images into folders, where each folder represents a different class. For example, if you are classifying images with type of materials, you need to have separate folders for "wool", "cotton" and "silk". Once your images are organized, you can upload them to the platform and create a new classification task.
The structure should look like this:

```
DatasetName/
│
├── Class1/
│   ├── obj1.jpg
│   ├── obj2.jpg
├── Class2/
│   ├── obj3.jpg
│   ├── obj4.jpg
├── Class3/
│   ├── obj5.jpg
│   ├── obj6.jpg
```

### Annotation Process
Once the dataset is created based on the previous mentioned structure, you can compress it as .zip file and upload it to the platform. The platform will automatically recognize the folder structure and register the dataset accordingly.

When you complete the upload, the platform will display the dataset existance in the Collections page, showing the number of images it contains.

### Training Initiation
After completing the Dataset upload, you can initiate the training of your classification model. Follow these steps:

1. Navigate to the Train an ML model page.
2. Select the Classification mode.

There are two main fields that need to be filled:

- **Select Model**: Choose the model architecture you want to use for training.
- **Select Collection**: Provide a name for your model.

For the available models, you can find information about them by clicking on the Currently Available models arrow and click on the preferred model to see more details about its architecture.

### Inference Process
Once the model is trained, you can use it for inference on new images. To perform inference, follow these steps:

1. Navigate to the Inference page.
2. Select the trained semantic segmentation model from the list.
3. Upload the image you want to perform inference on.
4. Click the Run Inference button to see the segmentation results.

Once the Inference process is complete, the result will be displayed directly into the same page, showing the origin image along with the corresponding class and confidence score.

<p align="center">
  <img src="/assets/platform_ui/class_inference.png" alt="CVAT" width="800">
</p>