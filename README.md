# Project Description: Transformer-Quantization
It is the final project repository for 2022 Spring COMS6998-E009 Practical Deep Learning System Performance in Columbia University. This repository is about conducting quantization and binarization on transformer models.

**Motivation**: Transformer is becoming SOTA base model for many NLP&CV tasks because of its ability to accomodate large-scale data. However, the main disadvantage of transformer is its large model size and even larger runtime memory usage. Therefore, it is important to explore diverse ways to compress model to lower hardware cost. Among diverse model compression techniques, quantization wins out because of its simplicity of implementation, preservation of original model structure and robustness to noise. 

Current quantization methods are mostly designed on CNN and tested on Image Classiﬁcation Task. However, there is huge difference between CNN and Transformer architecture. CNN has convolution as its base operation, while transformer relies mostly on Multi-head Attention module. They have totally different feature. So how to explore efficient and effective quantization method for transformer is main focus of our project.

**Goal**: We want to

1. Implement and modify diverse quantization and binarization methods from CNN to see if it still works well on transformer
2. Explore the internal feature of transformer structure and design special quantization pattern to improve quantization performance on transformer
3. Reach a trade-off between model size and bearable classiﬁcation error as an optimal compression strategy

**Approach**: We construct a transformer model with two encoder layers for text classification task as our baseline. We use AG_NEWS as target dataset. Basic quantization and binarization methods are implemented and tested on transformer, then two optimized algorithm from fully-quantization and IR Net are implemented to improve quantization performance. We also explored sensitivity of different parts of transformer and designed a speical pattern for transformer quantization that only quantizing Query and Key without Value, based on the observation that we only cares similarity between query and key instead of absolute values. At last, we proposed a new method called latent quantization, which train full precision model for a few epochs at beginning then switch to quantized model. This method is proved to be effective.
 

# Code Structure

**/quantization**: core codes including transformer definition, quantization, binarization. 

Inside this directory, `transformer.py` - definition of baseline transformer model; `quantize.py` - codes for basic quantization (weight only); `fully_quantize.py` - codes for fully quantization (quantize both weight and activation);  `binarize.py` - codes for basic and IR-Net binarization; `pytorch_api.py` - pytorch API for simple quantization, used for quickly go through essential ideas of quantization, not used in final experiment
 
**/utils**: util functions used in model training and other experiments

Inside this directory, `constants.py` - some pre-defined constants for model definition and training; `data_utils.py` - functions to construct dataset; `train_utils.py` - help functions used in training; `training.py` - core training codes; `check_activation.py` - functions used to compute runtime memory size; `pretrained.py` - functions to load pre-trained model weights; `utils.py` - other help functions


**/res**: save models, training logs, test results of different experiments

**/figures**: save figures for expeirments

`train_script.py`: main function to train model w or w/o quantization

`plot.ipynb`: used to plot figures

# Example commands to run

# Experiment and Results

## Experiment 1

```
