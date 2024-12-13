---
layout: page
title: Automatic Modulation Classifer
description: Major Project - Identifying the Modulation Type of a Signal
img: assets/img/amc/displaypicture.png
importance: 1
category: College Projects
---
<header>
    <h1>
        <a href="{{ '/assets/pdf/automatic_modulation_classification.pdf' | relative_url }}" target="_blank" rel="noopener noreferrer" class="float-right" style="color: grey; text-decoration: none;">
        <i class="fa-solid fa-file-pdf"></i>
        </a>
    </h1>
</header>


**Please refer to the entire thesis by clicking on the grey PDF button on the right.**

## Abstract
***
<div style="text-align: justify;">
Automatic Modulation Classification (AMC) is the classification of signals automatically based on the type of modulation used to generate that signal. Many different approaches
for AMC have been proposed which are categorized as ‘Decision Theoretic Approach’, ‘Feature Based Approach’ and ‘Deep Learning Based Approach’. Here, we have implemented
various types of classifiers for AMC which include likelihood based approach, deep learning
based approaches (LSTM and BiLSTM networks), CNN-LSTM model and also using a Quantum Neural Network
(QNN). The likelihood based classifier and the QNN are restricted to classify only two types
of modulations, namely BPSK and QPSK due to various limitation of those approaches.
The deep learning based classifiers can classify 11 different modualtion types from their IQ
samples in RadioML2016.10A dataset.
</div>
<div style="text-align: justify;">
Very poor classification accuracy is seen at lower SNR levels for all the implemented
models. The unrealistic requirement of perfect Channel State Information (CSI) in likelihood
based classifiers and the lack of computational power at present in QNN architectures make
them infeasible for real life use cases. The overall accuracy of 37.33%, 46.68%, 51.31%,
54.84% ,56.88%, 60.25% for LSTM, LSTM with attention, RadioML, Modified CNN, Bi-
LSTM, CNN-LSTM models respectively were observed. Among all these DL based models, CNN-LSTM with
attention layer achieved the highest accuracy of 90.01% (snr > 12 dB) while retaining a comparable
average prediction time of 0.041 ms for a signal.
</div>

<div style="border: 10px solid transparent;"></div>

## Methodology
***

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/systemblockdiagram.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    AMC System Block Diagram
</div>

We used multiple methodologies:


### CNN-LSTM based techinique
 CNN-LSTM model was found to be best.

##### Key Features of the Model

- **Multi-Scale Convolutional Layers**: Utilizes convolutional layers with different kernel sizes to capture features at various scales, crucial for understanding diverse characteristics of radio signals.

- **Regularization Techniques (L1/L2)**: Implements L1 and L2 regularization to prevent overfitting, encouraging model simplicity and parameter smoothness.

- **Batch Normalization**: Normalizes the activations of each layer, aiding in faster training convergence and providing regularization.

- **Max Pooling Layers**: Reduces the spatial dimensions of the input, cutting down on the number of parameters and computational load, which is essential for controlling overfitting.

- **Bidirectional LSTM with Attention Mechanism**: Processes data in both directions with a Bidirectional LSTM, capturing dependencies throughout the sequence. The Attention mechanism enables the model to focus on the most relevant parts of the input sequence for accurate predictions.

- **Dropout Layer**: Introduces a dropout layer to randomly deactivate input units during training, further preventing overfitting.

- **Dense and Output Layers**: Incorporates Dense layers, especially with a high neuron count, to learn complex patterns, and uses a softmax activation in the final layer for effective multi-class classification.

- **Optimization and Metrics**: Employs the Adam optimizer for adaptive learning rate adjustments, with categorical crossentropy as the loss function and accuracy as the performance metric.

This model represents a comprehensive approach to tackle the challenges in radio signal modulation recognition, offering a robust solution for accurately classifying different types of radio signal modulations, a task of immense significance in wireless communications.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/cnnlstm/MODEL.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/cnnlstm/SNR-ACCURACY.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/cnnlstm/OVERALLSNR.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/cnnlstm/ALL-SNR.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
***
## OTHER METHODS
- **Likelihood-Based Classifiers**: Traditional approach focusing on probabilistic models.
- **Other Deep Learning Techniques**: Different neural network architectures were used. This includes a modified Convolutional Neural Network (ConvNet), and Long Short-Term Memory (LSTM) units enhanced by an attention layer. Additionally, Bidirectional Long Short-Term Memory (Bi-LSTM) for efficient and comprehensive feature extraction.
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/namc.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/namla.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/nambil.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
- **Quantum Neural Network (QNN)**: Basic use of QNN
<div style="border: 10px solid transparent;"></div>

## Results
***

<div style="text-align: justify;">
    The graph below shows the accuracy of all the deep learning based models for different SNR levels.
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/overallsnr.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div style="text-align: justify;">
    We also computed the average time taken to perform prediction by each model. The tests were all run on Tensor Processing Unit (TPU)provided by Google Colab. Here, we see that the prediction time for a single sample is similar across all the models with little variations. The time taken for the single sample
    prediction is longest for the Bi-LSTM model and the fastest among all is the LSTM with attention layer model
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/time.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div style="border: 10px solid transparent;"></div>

#### Confusion matrix
***

<div style="text-align: justify;">
    Overall confusion matric for all methods
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/3_sa.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/4_sa.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/2_c.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/5_c.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/ca.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div style="border: 10px solid transparent;"></div>

#### Accuracy
***

<div style="text-align: justify;">
   Accuracy for different SNR level for all methods
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/2_slmc.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/3_c.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/4_c.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/amc/5_sa.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
