
# Introduction
For this project I wanted to pick a kaggle competition that used images and seemed interesting to me. This ended up being the Harmful Brain Activity Classification competition. The goal is to predict the distribution of expert annotations for a given EEG. Submissions are scored by the KL Divergence between the predicted and true annotation distributions. 

Link to the competition: https://www.kaggle.com/competitions/hms-harmful-brain-activity-classification

# Method
This competition is nearing completition, so there have already been many interesting ideas presented and scored. As is the case for all kaggle competitions, the best results are from ensemble methods, but in the interest of learning I wanted to avoid ensembles and instead focus on an interesting training procedure that still achieved compeitive results. For this I found a notebook which used a unique data augmentation along with self-training. The author of this notebook noted the correlation between high concensus annotations high quality data. To leverage this he initially splits the dataset into to subsets: high quality, having >= 10 votes for any  class label; low quality, having < 10 votes for all class labels. He came to this split via testing, but given that most samples have around 16 experts annotate them, 10/16 constitutes a 60% majority. Then he follows a typical self-training pipeline: train on the high quality data, predict psuedo-labels for the low quality data, update the datasets according to some aggregating function (here simple averaging).

The network used is an EfficientNetB0 and achieves 0.37 LB which is competitive with the best public notebook results (~0.3). For reference the current leaders score around 0.22, but likely use large ensembles and more complex methods.

The author uses an interesting data augmentation approach which concatentates multiple EEG spectrograms of the same signal but with different views. The result is a training image which has the entire spectrogram, along with two zoom-ins over the inference window (extracted from meta data). 

An example of the final spectrogram is shown below.


![image](https://github.com/DylanDeshler/Computer-Vision/assets/12647385/0208530b-6002-40f5-bdfa-e66b52e4be74)

Finally the results are evaluated with 5-fold cross validation.

# Results
You can check my leaderboard submission (score and code) here:
https://www.kaggle.com/code/dylandesh/no-ensemble-new-spectrograms-label-refine?scriptVersionId=169678558

# Analysis of Results
I was able to improve the results by using a larger Efficient Net model: B1, B2, and B3 provide performance beenfits without requiring too much memory. Training for more epochs also helps improve performance, but greatly increases training time. 


# Analysis of Vision Algorithms
Like most computer vision deep learning algorithms, they very rarely work 'in the wild' without any finetuning. The pretrained EfficientNet B0 without any fine-tuning performs very poorly on this task, clearly EEGs are sufficiently out of the training distribution. However, fine-tuning from the pretrained checkpoints is more tractable than from random initialization.
