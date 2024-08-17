---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
Time series classification is a rapidly evolving research field. Traditionally, quantitative methods such as Dynamic Time Warping have been the primary approach for tackling these tasks. However, with the recent advancements in deep learning, deep convolutional neural networks (CNNs) have gained prominence for their ability to handle time series data effectively. The introduction of transformer models has further revolutionized the field, enabling the transfer of learning capabilities from Vision-Language Models (VLMs) to time series classification. In this project, we pioneer the application of a multi-modal architecture like LLaVA for Time Series Classification (TSC), marking the first known exploration of this approach.

## Introduction
Llava is a powerful model for various machine learning tasks. Fine-tuning it for time series classification can significantly improve performance in your specific use case.

## GitHub Repository

You can find the complete codebase for this project on our [GitHub repository](https://github.com/vinayp17/VLM-TSC).

## Setting Up and Fine-Tuning VLM-TSC with LLaVA

Follow these steps to set up the environment and kick off the fine-tuning process:

### Step 1: Clone the VLM-TSC Repository
Begin by checking out the VLM-TSC repository:
```bash
git clone git@github.com:vinayp17/VLM-TSC.git
```
### Step 2: Run the Setup Script 
Navigate to the VLM-TSC directory and execute the setup script. This script will clone the Llava repository and install the necessary dependencies:
```
. setup.sh /code/LLaVA
```

### Step 3: Log in to Weights & Biases (wandb)
LLaVA uses wandb for experiment tracking. Log in to wandb before starting the training process:
```
wandb login
```

### Step 4: Initiate Fine-Tuning
Choose your dataset and hyperparameters, then start the fine-tuning process. Here’s an example command:
```
python train.py --downsample 2 --round_to 2 --dataset TwoLeadECG \
--vlm-root /code/VLM-TSC --llava-root /code/LLaVA --num-epochs 2 \
--context-length 2048 --data-repr WITH_STATS
```

## Datasets Considered

We have considered a diverse set of datasets for our time series classification tasks. These include:

### Univariate Time Series Datasets
- **TwoLeadECG**: A dataset of ECG signals with two leads.
- **CinCECGTorso**: ECG signals recorded from the torso.
- **FreezerSmallTrain**: Temperature readings from a small freezer.
- **PhalangesOutlinesCorrect**: Outlines of phalanges from X-ray images.
- **ItalyPowerDemand**: Power demand readings from Italy.

### Multivariate Time Series Datasets
- **PenDigits**: Handwritten digit data with multiple features.
- **HandOutlines**: Outlines of hand shapes.

## Data Generation

To generate data for a specific datasource, follow these steps:

1. Edit the `configs/llava_config.yaml` file to specify the appropriate dataset, downsampling, and rounding parameters.
2. Run the following command:
   ```sh
   python dataset.py configs/llava_config.yaml```

## Steps to Fine-tune Llava

1. **Data Preparation:**
   - Gather and preprocess your time series data.
2. **Model Configuration:**
   - Configure Llava for your specific task.
3. **Training:**
   - Train the model with your data.
4. **Evaluation:**
   - Evaluate the model's performance.

## Resources

- [Llava Documentation](https://llava-docs.example.com)
- [Time Series Classification Tutorial](https://time-series-tutorial.example.com)

## Conclusion

Fine-tuning Llava for time series classification tasks can be highly beneficial for improving model accuracy and performance. Follow the steps outlined in this guide to achieve the best results.

