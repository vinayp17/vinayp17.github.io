---
layout: page
title: "Architecture"
permalink: /architecture/
---

# Pipeline Architecture
Our AI pipeline is designed to facilitate the end-to-end process of scenario generation, experiment execution for multiple data sets, data generation, training, and evaluation. Below is an overview of each component and its role in the pipeline.

## 1. Scenario Generator

The Scenario Generator is the first step in the pipeline, responsible for generating various experimental scenarios. Each scenario generates the input data for a given set of hyperparameters. For example, the BASELINE_2048 scenario uniformly downsamples time series signals to ensure they fit within a context length of 2048. More information related to different scenarios can be found on the [Configuration](/configuration) page.


```
python scenario_generator.py # Will generate a config json with all the scenarios
```

## 2. Experiment Launcher

The Experiment Launcher is used to execute experiments on the datasets defined within the metadata directory. It allows users to specify which scenario to run and supports running a subset of experiments by specifying start and end indices.

```
python experiments_launcher.py --vlm-root VLM_ROOT --llava-root LLAVA_ROOT --scenario SCENARIO --config CONFIG [--start-index START_INDEX] [--end-index END_INDEX]

```

### Options:
--vlm-root: Root directory for VLM-TSC git repository.

--llava-root: Root directory for LLaVA git repository.

--scenario: Scenario identifier for the experiment.

--config: Path to a JSON file describing all scenarios.

--start-index: Index to start the experiment from.

--end-index: Index to end the experiment at.

## 3. Training

Training is performed via the train.py script, which is invoked by the Experiment Launcher with the chosen scenario configuration. This step handles data generation, fine-tuning, and evaluation. Right before data generation, the appropriate YAML configuration file is generated for every given scenario, specifying settings such as context_length, rounding, and downsampling type.

```
python train.py --dataset DATASET --vlm-root VLM_ROOT --llava-root LLAVA_ROOT --scenario SCENARIO [other options...]
```

### Options

--round_to ROUND_TO

--dataset DATASET

--vlm-root VLM_ROOT   Root Dir for VLM-TSC git repo

--llava-root LLAVA_ROOT Root Dir for LLaVA git repo

--num-epochs NUM_EPOCHS

--context-length CONTEXT_LENGTH

--data-repr {BASELINE,WITH_RATIONALE,WITH_SIGNAL_ANALYSIS,WITH_STATS}

--use-adaptive-downsampling

--plot-downsampled-graph

--scenario SCENARIO   Experiment scenario to run for


## 4. Data Generation

Data generation is carried out by dataset.py, which processes data according to the YAML configuration file generated during the training phase. This script sets the hyperparameters needed for data generation based on the configuration file.

```
python dataset.py configs/llava_config.yaml
```



## 5. Fine-Tuning Methodology

Once the data is prepared, we proceed with fine-tuning using the methodology outlined in the [LLaVA Fine-Tuning Guide](https://wandb.ai/byyoung3/ml-news/reports/How-to-Fine-Tune-LLaVA-on-a-Custom-Dataset--Vmlldzo2NjUwNTc1). This step is crucial for adapting pre-trained models to the specific scenarios generated earlier.

## 6. Evaluation

After fine-tuning, the model's performance is evaluated using one-shot accuracy on the test data. The evaluation process includes performance calculation and one-shot testing on the generated scenarios.

### Performance Evaluation:

```
eval_performance(vlm_root, llava_root, scenario)
```

### One-Shot Testing:

```
one_shot(dataset, f"{llava_root}/playground/new_data/{scenario}/answer.json")
```

