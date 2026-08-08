# Dataset Preparation

## Dataset Size

The amount of data required depends on the task, the number of classes, and the complexity of the problem. The following values are practical guidelines rather than strict requirements.

### 1. Image Classification

* **Recommended minimum:** At least 100 images per class.
* **Recommended value:** 500-1,000 images per class.
* **Important:** Try to maintain a relatively balanced number of images across classes.
* **Data diversity:** Images should contain different viewpoints, backgrounds, lighting conditions, scales, and appearances.

### 2. Object Detection

* **Recommended minimum:** At least 100 images containing each object class.
* **Recommended value:** 500-1,000 images containing each class.
* **Important:** The number of annotated object instances is also important because one image can contain multiple objects.
* **Data diversity:** Include different object sizes, positions, viewpoints, backgrounds, lighting conditions, and levels of occlusion.

### 3. Semantic Segmentation

* **Recommended minimum:** At least 100 annotated images.
* **Recommended value:** 300-500+ annotated images.
* **Complex datasets:** 1,000+ annotated images may be required for complex problems with many classes or high visual variability.
* **Important:** Each class should have sufficient pixel-level representation.
* **Annotation quality:** Segmentation masks should accurately represent the target regions.

## Dataset Split

The dataset is divided into three subsets:

* **Training Set:** Used to train the model and update its parameters.
* **Validation Set:** Used during training to evaluate the model and select the best configuration.
* **Test Set:** Used after training to evaluate the final model.

### Recommended Split

A general-purpose split is:

```text
Training:    80%
Validation:  10%
Test:        10%
```

For example, for a dataset containing 1,000 images:

```text
Training:    800 images
Validation:  100 images
Test:        100 images
```

If a separate test set is not required, a **70/30 split** can be used:

```text
Training:    70%
Validation:  30%
```

For example, for a dataset containing 1,000 images:

```text
Training:    700 images
Validation:  300 images
```

This is a suitable option when the main goal is model training and configuration selection and a separate final test evaluation is not required.

## Class Balance

The classes should be reasonably balanced across the dataset splits.

For example, if the original classification dataset contains:

```text
Class A: 60%
Class B: 30%
Class C: 10%
```

the same approximate distribution should be maintained in the training, validation, and test sets.

For object detection and segmentation, class balance should also be considered at the object and pixel levels respectively.

## Data Diversity

The dataset should contain enough variation to represent the conditions in which the model will be used.

Consider including:

* Different viewpoints and orientations.
* Different object sizes and positions.
* Different backgrounds.
* Different lighting conditions.
* Different levels of occlusion.
* Different image qualities.
* Different appearances within the same class.

Having many nearly identical images does not provide the same benefit as having diverse images.

## Data Leakage

Data leakage occurs when information from the validation or test set is indirectly available during training. This can lead to overly optimistic evaluation results.

To reduce the risk of data leakage:

* Do not include duplicate images in different subsets.
* Avoid placing near-duplicate images in different subsets.
* Images from the same video sequence should preferably remain in the same subset.
* Images of the same physical object or scene should preferably remain in the same subset.
* Preprocessing parameters learned from the data should be calculated using the training set only.

For example, if multiple images are extracted from the same video sequence:

**Recommended:**

```text
video_01 → Training
video_02 → Training
video_03 → Validation
video_04 → Test
```

**Incorrect:**

```text
video_01_frame_001 → Training
video_01_frame_002 → Test
video_01_frame_003 → Training
```

The incorrect approach can cause the test set to contain images that are very similar to images seen during training.

**Note on Dataset Size:** These values are provided as practical guidelines rather than fixed requirements. The required dataset size depends on the number of classes, task complexity, image diversity, annotation quality, and model architecture.

**Note on Dataset Splitting:** The test set should only be used for final evaluation. It should not be used for model selection or hyperparameter tuning.
