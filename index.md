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

### Results

| Dataset                   | Scenario                                | Accuracy |
|---------------------------|-----------------------------------------|----------|
| CinCECGTorso              | BASELINE_4096                           | 98.3     |
| CinCECGTorso              | BASELINE_2048_adaptive_ds_plot_ds       | 82.7     |
| CinCECGTorso              | BASELINE_2048                           | 76.4     |
| TwoLeadECG                | BASELINE_2048                           | 99.1     |
| ItalyPowerDemand          | BASELINE_2048                           | 90       |
| FreezerSmallTrain         | BASELINE_4096                           | 98.78    |
| FreezerSmallTrain         | BASELINE_2048                           | 97.39    |
| PenDigits                 | BASELINE_4096                           | 85.08    |
| PenDigits                 | BASELINE_2048                           | 72.89    |
| PhalangesOutlinesCorrect  | BASELINE_2048                           | 68.79    |
| HandOutlines              | BASELINE_4096                           | 66.7     |
| HandOutlines              | BASELINE_2048                           | 66.7     |


## Resources

- [Llava Documentation](https://llava-vl.github.io)
- [Time Series Classification Data](https://www.timeseriesclassification.com)

## Conclusion

Fine-tuning Llava for time series classification tasks can be highly beneficial for improving model accuracy and performance. Follow the steps outlined in this guide to achieve the best results.

