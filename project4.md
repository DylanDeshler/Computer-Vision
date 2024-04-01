
# Introduction
For this project I wanted to pick a kaggle competition that used images and seemed interesting to me. This ended up being the Harmful Brain Activity Classification competition. The goal is to predict the distribution of expert annotations for a given EEG. Submissions are scored by the KL Divergence between the predicted and true annotation distributions. 

Link to the competition: https://www.kaggle.com/competitions/hms-harmful-brain-activity-classification

# Method
This competition is nearing completition, so there have already been many interesting ideas presented and scored. As is the case for all kaggle competitions, the best results are from ensemble methods, but in the interest of learning I wanted to avoid ensembles and instead focus on an interesting training procedure that still achieved compeitive results. For this I found a notebook which used a unique data augmentation along with self-training. The author of this notebook noted the correlation between high concensus annotations high quality data. To leverage this he initially splits the dataset into to subsets: high quality, having >= 10 votes for any  class label; low quality, having < 10 votes for all class labels. He came to this split via testing, but given that most samples have around 16 experts annotate them, 10/16 constitutes a 60% majority. Then he follows a typical self-training pipeline: train on the high quality data, predict psuedo-labels for the low quality data, update the datasets according to some aggregating function (here simple averaging).

The network used is an EfficientNetB0 and achieves 0.37 LB which is competitive with the best public notebook results (~0.3). For reference the current leaders score around 0.22, but likely use large ensembles and more complex methods.


The author uses an interesting data augmentation approach which concatentates multiple EEG spectrograms of the same signal but with different views. The result is a training image which has the entire spectrogram, along with two zoom-ins over the inference window (extracted from meta data). An example of the final spectrogram is shown below.
![image](https://github.com/DylanDeshler/Computer-Vision/assets/12647385/0208530b-6002-40f5-bdfa-e66b52e4be74)


# Results
You can check my leaderboard submission here:
https://www.kaggle.com/code/dylandesh/no-ensemble-new-spectrograms-label-refine?scriptVersionId=169678558

# Analysis of Results
Because the video I used is a timelapse of a single bar it is unreasonable to make any generalizations, and further there is no designation about when the bar opens or closes. But the bar maintains a reasonably steady average of people until close to closing time, when it dies out. The plot shows a consistant average for the majority of the time, but there is a large variance between frames. After examining the video I think this is primarily a symptom of downsampling the timelapse, rather than the true fluctuation of customers. I found nothing surprising about these results.


# Analysis of Vision Algorithms
Like most computer vision deep learning algorithms, they very rarely work 'in the wild' without any finetuning. I ran a handful of images through DETR and got reasonably accurate results, but the number of detections and correct classifications was rarely perfect. I've noticed the large gap between benchmark accuracy and real world performance frequently with my work, and I think it primarily stems from the type of data these networks are typically trained and evaluated on. The images are typically prestine quality, with a clear distinction between target, foreground, and background, which makes the learning simple and leads to non-robust representations. When doing a breif prior analysis, I found that DETR seemed to perform substantially worse on people of color (not surprising), the bar video I found is primarily of white people, so this shouldn't have much of an impact on the results I was able to gather.
