---
layout: page
title: "Configuration"
permalink: /configuration/
---

Following table describes a snapshot of the config space used, this is easily extensible by adding your scenario inside scenario_generator.py

| Scenario                            | round_to | num_epochs | context_length | data_repr | use_adaptive_downsampling | plot_downsampled_graph |
|-------------------------------------|----------|------------|----------------|-----------|--------------------------|------------------------|
| BASELINE_2048                       | 2        | 2          | 2048           | BASELINE  | false                    | false                  |
| BASELINE_4096                       | 2        | 2          | 4096           | BASELINE  | false                    | false                  |
| WITH_STATS_2048                     | 2        | 2          | 2048           | WITH_STATS | false                   | false                  |
| WITH_STATS_4096                     | 2        | 2          | 4096           | WITH_STATS | false                   | false                  |
| BASELINE_2048_adaptive_ds_plot_ds   | 2        | 2          | 2048           | BASELINE  | true                     | true                   |
| BASELINE_2048_adaptive_ds           | 2        | 2          | 2048           | BASELINE  | true                     | false                  |

