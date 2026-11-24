# Rotten and Fresh Fruit Detection

A binary image classifier that tells whether a fruit is **fresh** or **rotten**.

## Dataset

- Shipped as `dataset.rar`. After extracting you get `dataset/train` and `dataset/test`.
- Six folders: `freshapples`, `freshbanana`, `freshoranges`, `rottenapples`, `rottenbanana`, `rottenoranges`. The three fruit types are merged into two labels: fresh (0) and rotten (1).
- Sizes printed by the notebook:
  - Train: 10,901 images (6,161 rotten, 4,740 fresh)
  - Test (used as validation): 2,698 images (1,534 rotten, 1,164 fresh)
- Images are resized to 100 x 100 RGB and divided by 255.
- The original source of the images is not stated in the code.

## Model

A CNN built from scratch with Keras / TensorFlow:

- Blocks of `Conv2D` / `SeparableConv2D` with 32, 64 and 128 filters, each with BatchNormalization, MaxPooling and Dropout (0.3 to 0.5)
- `Flatten` -> `Dense(128, relu)` -> `Dropout(0.3)` -> `Dense(1, sigmoid)`
- 2,591,393 parameters in total
- Loss: binary cross-entropy, optimizer: Adam (learning rate 0.001), batch size 20, 50 epochs
- A checkpoint callback saves the model with the best validation loss as `rotten.h5`

## Results (from the notebook output)

- Final epoch (50/50): training accuracy 0.9870, validation accuracy 0.9878
- Final `model.evaluate` on the test set: loss 0.0361, accuracy **0.9878**
- Validation accuracy moved between epochs (for example 0.9611 at one epoch near the end), so results vary from epoch to epoch.

The test set is also used as the validation set during training, so the final number is not from a fully separate hold-out set.

## How to run

1. Extract `dataset.rar` so `dataset/` is next to the notebook.
2. Install: `pip install tensorflow keras numpy pandas matplotlib opencv-python tqdm`
3. Open `Rotten Vs Fresh Fruit.ipynb` and run the cells in order. A GPU is recommended (the notebook ran on one).

## Files

- `Rotten Vs Fresh Fruit.ipynb`: the full code and outputs
- `dataset.rar`: the dataset
