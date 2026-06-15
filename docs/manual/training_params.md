# Training Parameters

## Hyperparameters

### 1. Learning Rate
* **Definition:** How fast the AI tries to learn from its mistakes. Think of it like adjusting your aim in darts: a big learning rate means making huge corrections, while a small one means making tiny, careful adjustments.
* **How it is tuned:** We start small. If the AI learns too slowly, we increase it. If it gets confused and makes erratic mistakes, we decrease it.
* **Recommended value space:** 0.0001-0.01

### 2. Batch Size
* **Definition:** The number of examples the model processes at the same time before updating its knowledge.
* **How it is tuned:** It depends on the available computer memory (VRAM).
* **Recommended value space:** 8-32.

### 3. Epochs
* **Definition:** How many times the AI reads through the entire set of examples. One epoch means the AI has seen every single training image exactly once.
* **How it is tuned:** We set a number based on how long the model needs to adequately learn the patterns in the data, ensuring it learns general patterns without simply memorizing the training set.
* **Recommended value space:** 10-100.

**Note on Parameter Selection:** These values are provided as ranges rather than fixed inputs because the platform employs a Random Search optimization algorithm. During execution, the system evaluates various random combinations within these boundaries to efficiently identify the best-performing configuration for your data.

## Augmentations

These techniques slightly change the original images to artificially create new data, helping the model generalize better.

<p align="center">
  <img src="../../assets/others/Augmentations.png" alt="Augmentations" width="800">
</p>

* **Blur:** Makes the image less sharp.
* **Scale:** Zooms in or out.
* **Rotate:** Turns the image by random degrees.
* **Flip:** Mirrors the image horizontally or vertically.
* **Hue:** Slightly changes the color spectrum.
* **Saturation:** Makes the colors more vibrant or more washed out.
* **Value:** Changes the brightness or darkness of the image.