# Introduction

This repository provides the models and the source code for the master's thesis "Extraction and Classification of Time in Unstructured Data" (2023).
Furthermore, it describes the steps required to reproduce the thesis results.
The transformer-based models are finetuned to find and classify temporal expressions in unstructured text.

The models produced by the thesis utilize the two frameworks, UIE and MaChAmp.
Both repositories were forked in August 2023 and modified to suit the problem of temporal extraction and classification.
Most changes were applied to the evaluation and dataset preprocessing scripts.
The scripts for finetuning and inference remain very close to the original versions:

* Unified Structure Generation for Universal Information Extraction (UIE) [[Lu et al., 2022]](#References) - [GitHub Link](https://github.com/universal-ie/UIE)
    * UIE is a sequence-to-sequence framework that extracts various information extraction targets into a graph structure called "Structured Extraction Language".
    It is based on the T5 library [[Raffel et al., 2020]](#References).
* Massive Choice, Ample Tasks (MACHAMP) [[van der Goot et al., 2020]](#References) - [GitHub Link](https://github.com/machamp-nlp/machamp)
    * MaChAmp is a multitask learning framework.
    In this thesis, it is used to train BERT-based models in a single-task fashion. [Lu et al., 2022]

The finetuned models are produced using a 10-fold-crossvalidation appraoch, which might be time consuming to reproduce.
Nevertheless, this documentation provides two different instructions:

* Quickstart: download the finetuned models and use them immediatly
* Full reproduction of all steps required to convert the datasets, finetune the models and do inference on the datasets

Since two different frameworks are used in this theis, the general steps are the same (converting the data, finetuning the models, inference). But the two frameworks have differnt scripts to achieve this.
Furthermore, both frameworks require different Python packages.
Creating an Anaconda environment for both UIE and MaChAmp is recommended.
The exact installation packages are described in README.md files in the [UIE](uie/README.md) and [MaChAmp](machamp/README.md) folders.



# Project Overview

The overall projectstructure looks like this:

```text
temporal-extraction
├── uie                 # Contains all the scripts and documentation related to UIE
├── machamp             # Contains all the scripts and documentation related to MaChAmp
├── results             # Contains the result tables and logfiles of the finetuned models used in the theis 
├── temporal-data       # Contains the datasets, as well as the scripts required for conversion
```

This is the main directory (temporal-extraction).
Its purpose is to offer the general introduction and overview for the project.
Both [uie](uie/README.md) and [machamp](machamp/README.md) contain the framework-specific documentation required to both use the models and fully reproduce the steps in the thesis.

The [results](results/README.md) folder shows the result tables and logfiles produced during the thesis.
In particular, it shows the results for every dataset and every fold in the crossvalidation.
Furthermore, it contains the files that display the exact error cases i.e. where the model mispredicted the sentence.

The [temporal-data](temporal-data/README.md) folder contains all the converted datasets, as well as the publicly available original versions.
It also contains the scripts required to convert the original datasets into the required format.
UIE uses a json format structure, while MaChAmp uses a mutliclass BIO format.



# Finetuned Models
Only the best performing models are shared in this section, due to the large amount of different models produced in the thesis.
Furthermore, only the models which detect multiple classes (date, time, duration, set) are uploaded, because the single class models do not show any performance increase as was found in the "Results" section of the thesis.
The following table shows the mutliclass results on the different datasets:

[![This table compares the most important metrics “Strict-F1” and “RelaxedType-F1” for the temporal extraction and classification tasks across all datasets and all models. The best three values per column are highlighted with bold font. Table 11 in the appendix C displays the standard deviation values for the MaChAmp (M) and UIE model rows.](docs/images/temporal-extraction-and-classification-performance.png)]()
> Table shows the temporal extraction and classification performance for the models produced in the thesis. M stands for MaChAmp models. The bottom part of the table shows the performance of related work. "Strict" means an exact match and "Type" means a match where at least one token (also known as "relaxed" match) and the temporal class is correct.

## UIE Models

### UIE Base Models 
| Dataset                        | URL                     |
|-------------------------------:|-------------------------|
| TempEval-3      | [Download Link](https://www.fdr.uni-hamburg.de/record/13599)                      |
| WikiWars        | [Download Link](https://www.fdr.uni-hamburg.de/record/13595)                      |
| Tweets          | [Download Link](https://www.fdr.uni-hamburg.de/record/13597)                      |
| Fullpate        | [Download Link](https://www.fdr.uni-hamburg.de/record/13601)                      |

### UIE Large Models 
| Dataset                        | URL                                                                |
|-------------------------------:|--------------------------------------------------------------------|
| TempEval-3      | [Download Link](https://www.fdr.uni-hamburg.de/record/13615)                      |
| WikiWars        | [Download Link](https://www.fdr.uni-hamburg.de/record/13617)                      |
| Tweets          | [Download Link](https://www.fdr.uni-hamburg.de/record/13619)                      |
| Fullpate        | [Download Link](https://www.fdr.uni-hamburg.de/record/13621)                      |

## MaChAmp Models

### MaChAmp-RoBERTa Large Models 
| Dataset                        | URL                                                                |
|-------------------------------:|--------------------------------------------------------------------|
| TempEval-3      | [Download Link](https://www.fdr.uni-hamburg.de/record/13623)                      |
| WikiWars        | [Download Link](https://www.fdr.uni-hamburg.de/record/13627)                      |
| Tweets          | [Download Link](https://www.fdr.uni-hamburg.de/record/13629)                      |
| Fullpate        | [Download Link](https://www.fdr.uni-hamburg.de/record/13625)                      |

### MaChAmp-XLM-RoBERTa Base Models 
| Dataset                        | URL                                                                |
|-------------------------------:|--------------------------------------------------------------------|
| TempEval-3      | [Download Link](https://www.fdr.uni-hamburg.de/record/13631)                      |
| WikiWars        | [Download Link](https://www.fdr.uni-hamburg.de/record/13635)                      |
| Tweets          | [Download Link](https://www.fdr.uni-hamburg.de/record/13637)                      |
| Fullpate        | [Download Link](https://www.fdr.uni-hamburg.de/record/13633)                      |

### MaChAmp-XLM-RoBERTa Large Models 
| Dataset                        | URL                                                                |
|-------------------------------:|--------------------------------------------------------------------|
| TempEval-3      | [Download Link](https://www.fdr.uni-hamburg.de/record/13589)                      |
| WikiWars        | [Download Link](https://www.fdr.uni-hamburg.de/record/13591)                      |
| Tweets          | [Download Link](https://www.fdr.uni-hamburg.de/record/13587)                      |
| Fullpate        | [Download Link](https://www.fdr.uni-hamburg.de/record/13593)                      |



# References
* [Lu et al., 2022] [Lu, Y., Liu, Q., Dai, D., Xiao, X., Lin, H., Han, X., Sun, L., and Wu, H. (2022). Unified structure generation for universal information extraction. arXiv preprint arXiv:2203.12277.](https://aclanthology.org/2022.acl-long.395/)

* [van der Goot et al., 2020] [van der Goot, R., Üstün, A., Ramponi, A., Sharaf, I., and Plank, B. (2020). Massive choice, ample tasks (machamp): A toolkit for multi-task learning in nlp. arXiv preprint arXiv:2005.14672.](https://arxiv.org/abs/2005.14672)

* [Raffel et al., 2020] [Raffel, C., Shazeer, N., Roberts, A., Lee, K., Narang, S., Matena, M., Zhou, Y., Li, W., and Liu, P. J. (2020). Exploring the limits of transfer learning with a unified text-to-text transformer. The Journal of Machine Learning Research, 21(1):5485– 5551](https://arxiv.org/abs/1910.10683)

[comment]: <> (Test comment)