
# Image Captioning with BLIP

This project implements an image captioning system using the BLIP (Bootstrapping Language-Image Pretraining) model. 
The pipeline fine-tunes the pretrained BLIP model to generate natural language descriptions of input images using a dataset of image-caption pairs.

## Project Structure

```
Image_Captioning/
├── Image_Captioning.ipynb        # Main notebook for end-to-end execution
├── data/                         # Folder for images and annotations (train.csv)
├── outputs/                      # Generated captions and results
└── README.md                     # Project documentation (this file)
```

## Dataset

The dataset contains image-caption pairs and is stored externally due to size limitations.  
Please download and extract it into the `/content/data` directory.

Download the dataset:  
https://drive.google.com/drive/folders/12MrQf0s39WKGB-81ftvZ6x6KgucODXGU?usp=drive_link

The dataset structure should look like this after extraction:

```
data/
├── train/
│   ├── image1.jpg
│   ├── image2.jpg
│   └── ...
└── train.csv      # CSV file with 'image_id' and 'caption' columns
```

## Setup & Requirements

Install the required dependencies:

```bash
pip install -q transformers sentence-transformers torchvision
```

## Training

1. Unzip the dataset into `/content/data`.
2. Launch and run `Image_Captioning.ipynb` in Google Colab or Jupyter Notebook.
3. The notebook handles preprocessing, dataset creation, and model training.

### Key Components

- `BlipProcessor` and `BlipForConditionalGeneration` are used for processing and model loading.
- Custom `ImageCaptionDataset` loads images and applies tokenization and image transformations.
- Fine-tuning is done using Hugging Face `Trainer` with a custom data collator.

### TrainingArguments

```
batch_size = 4 (with gradient accumulation = 4)
num_train_epochs = 6
logging_steps = 100
save_steps = 500
```

Model and processor are saved after training at `/content/6-epoch`.
