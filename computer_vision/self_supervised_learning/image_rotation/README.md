# Paper Understanding
- [Unsupervised Representation Learning by Predicting Image Rotations](https://arxiv.org/pdf/1803.07728.pdf)
## Related Works
- In order to learn features, [1] and [2] train ConvNets to colorize gray scale images, [3] and [4] predict the relative position of image patches, and [5] predict the egomotion (i.e., self-motion) of a moving vehicle between two consecutive frames.
- The core intuition of our self-supervised feature learning approach is that if someone is not aware of the concepts of the objects depicted in the images, he cannot recognize the rotation that was applied to them.
- Other successful cases of unsupervised feature learning are clustering based methods ([6], [7] and [8]), reconstruction based methods (Bengio et al., 2007; Huang et al., 2007; Masci et al., 2011), and methods that involve learning generative probabilistic models Goodfellow et al. (2014); Donahue et al. (2016); Radford et al. (2015).
## Introduction
- Self-supervised learning defines an annotation free pretext task, using only the visual information present on the images or videos, in order to provide a surrogate supervision signal for feature learning.
## Methodolgy
- We propose to train a ConvNet model $F$ to estimate the geometric transformation applied to an image that is given to it as input. Specifically, we define a set of $K$ discrete geometric transformations $G = \{g(; k)\}^{K}_{k = 1}$, where $g(; k)$ is the operator that applies the geometric transformation $k$ to image $X$ that yields the transformed image $X^{k} = g(X ; k)$. The ConvNet model $F$ gets an image $X^{k^*}$ (where $k^{∗}$ is unknown to model $F$) as input and yields as output a probability distribution over all possible geometric transformations:
$$p(X^{k^{∗}}; \theta) = \{p^{k}(X^{k^{*}}; \theta)\}^{K}_{k = 1}$$
- where $p^{y}(X^{k^{∗}}; \theta)$ is the predicted probability for the geometric transformation $k$ and $\theta$ are the learnable parameters of model $F$. Therefore, given a set of $N$ training images $D = \{X_{i}\}^{N}_{i = 1}$, the self-supervised training objective that the ConvNet model must learn to solve is:
$$\argmin_{\theta}\frac{1}{N}\sum^{N}_{i = 1}loss(X_{i}, \theta)$$
- where the loss function $loss$ is defined as:
$$loss(X_{i}, \theta) = −\frac{1}{K}\sum^{K}_{k = 1}\log\bigg(p^{k}\big(g(X_{i}; k); \theta\big)\bigg)$$
- Figure 2
    - <img src="https://user-images.githubusercontent.com/67457712/227820083-dea02047-3d9d-43d0-8936-e4172c94aeec.png" width="800">
    - In the above formulation, the geometric transformations G must define a classification task that should force the ConvNet model to learn semantic features useful for visual perception tasks (e.g., object detection or image classification). In our work we propose to define the set of geometric transformations G as all the image rotations by multiples of 90 degrees, i.e., 2d image rotations by 0, 90, 180, and 270 degrees (see Figure 2). More formally, if Rot(X, φ) is an operator that rotates image X by φ degrees, then our set of geometric transformations consists of the K = 4 image rotations G = {g(X|y)} 4 y=1, where g(X|y) = Rot(X,(y − 1)90).
- The core intuition behind using these image rotations as the set of geometric transformations relates to the simple fact that **it is essentially impossible for a ConvNet model to effectively perform the above rotation recognition task unless it has first learned to recognize and detect classes of objects as well as their semantic parts in images. More specifically to successfully predict the rotation of an image the ConvNet model must necessarily learn to localize salient objects in the image, recognize their orientation and object type, and then relate the object orientation with the dominant orientation that each type of object tends to be depicted within the available images.***
## Experiments
- Figure 3
    - <img src="https://user-images.githubusercontent.com/105417680/228284692-dde6840d-8b27-4f2a-acee-27d90688d22b.png" width="900">
    - '(b)': We visualize some attention maps generated by a model trained on the rotation recognition task.
    - These attention maps are computed based on the magnitude of activations at each spatial cell of a convolutional layer and essentially reflect where the network puts most of its focus in order to classify an input image. ***We observe that in order for the model to accomplish the rotation prediction task it learns to focus on high level object parts in the image, such as eyes, nose, tails, and heads.***
    - '(a)': By comparing them with the attention maps generated by a model trained on the object recognition task in a supervised way we observe that both models seem to focus on roughly the same image regions.
## References
- [1] [Colorful Image Colorization](https://arxiv.org/pdf/1603.08511.pdf)
- [2] [Learning Representations for Automatic Colorization](https://arxiv.org/pdf/1603.06668.pdf)
- [3] [Unsupervised Visual Representation Learning by Context Prediction](https://arxiv.org/pdf/1505.05192.pdf)
- [4] [Unsupervised Learning of Visual Representations by Solving Jigsaw Puzzles](https://arxiv.org/pdf/1603.09246.pdf)
- [5] [Learning to See by Moving](https://arxiv.org/pdf/1505.01596.pdf)
- [6] [Discriminative Unsupervised Feature Learning with Exemplar Convolutional Neural Networks](https://arxiv.org/pdf/1406.6909.pdf)
- [7] [Learning deep parsimonious representations]
- [8] [Joint unsupervised learning of deep representations and image clusters]


- Figure 4
    - <img src="https://user-images.githubusercontent.com/67457712/227821123-ea732b32-49ca-4783-a849-9ec18da55a78.png" width="500">
- Table 1
    - <img src="https://user-images.githubusercontent.com/67457712/227821225-f98e1b5d-b626-4d7f-a209-9d2213079a89.png" width="400">
- Table 2
    - <img src="https://user-images.githubusercontent.com/67457712/227821317-0973c388-b632-47b6-80a6-cb531009e778.png" width="400">
    - Exploring the quality of the self-supervised learned features w.r.t. the number of recognized rotations. For all the entries we trained a non-linear classifier with 3 fully connected layers (similar to Table 1) on top of the feature maps generated by the 2nd conv. block of a RotNet model with 4 conv. blocks in total. The reported results are from CIFAR-10.
- Table 3
    - <img src="https://user-images.githubusercontent.com/67457712/227821425-cd89da20-88b6-4eb5-8538-8d3187895bce.png" width="500">
    - Evaluation of unsupervised feature learning methods on CIFAR-10. The Supervised NIN and the (Ours) RotNet + conv entries have exactly the same architecture but the first was trained fully supervised while on the second the first 2 conv. blocks were trained unsupervised with our rotation prediction task and the 3rd block only was trained in a supervised manner. In the Random Init. + conv entry a conv. classifier (similar to that of (Ours) RotNet + conv) is trained on top of two NIN conv. blocks that are randomly initialized and stay frozen. Note that each of the prior approaches has a different ConvNet architecture and thus the comparison with them is just indicative.
- Figure 5
    - <img src="https://user-images.githubusercontent.com/67457712/227821533-bd5118a8-bb46-41ba-b37f-275d0bf6e391.png" width="700">
    - (a) Plot with the rotation prediction accuracy and object recognition accuracy as a function of the training epochs used for solving the rotation prediction task. The red curve is the object recognition accuracy of a fully supervised model (a NIN model), which is independent from the training epochs on the rotation prediction task. The yellow curve is the object recognition accuracy of an object classifier trained on top of feature maps learned by a RotNet model at different snapshots of the training procedure. (b) Accuracy as a function of the number of training examples per category in CIFAR-10. Ours semi-supervised is a NIN model that the first 2 conv. blocks are RotNet model that was trained in a self-supervised way on the entire training set of CIFAR-10 and the 3rd conv. block along with a prediction linear layer that was trained with the object recognition task only on the available set of labeled images.
- Table 4
    - <img src="https://user-images.githubusercontent.com/67457712/227821622-1da08ecd-3d06-463e-bd57-3724eb0d0412.png" width="500">
    - Task Generalization: ImageNet top-1 classification with non-linear layers. We compare our unsupervised feature learning approach with other unsupervised approaches by training non-linear classifiers on top of the feature maps of each layer to perform the 1000-way ImageNet classification task, as proposed by Noroozi & Favaro (2016). For instance, for the conv5 feature map we train the layers that follow the conv5 layer in the AlexNet architecture (i.e., fc6, fc7, and fc8). Similarly for the conv4 feature maps. We implemented those non-linear classifiers with batch normalization units after each linear layer (fully connected or convolutional) and without employing drop out units. All approaches use AlexNet variants and were pre-trained on ImageNet without labels except the ImageNet labels and Random entries. During testing we use a single crop and do not perform flipping augmentation. We report top-1 classification accuracy.
- Table 5
    - <img src="https://user-images.githubusercontent.com/67457712/227821722-02b98536-58d2-412b-8725-9c7efa96e90e.png" width="500">
    - Task Generalization: ImageNet top-1 classification with linear layers. We compare our unsupervised feature learning approach with other unsupervised approaches by training logistic regression classifiers on top of the feature maps of each layer to perform the 1000-way ImageNet classification task, as proposed by Zhang et al. (2016a). All weights are frozen and feature maps are spatially resized (with adaptive max pooling) so as to have around 9000 elements. All approaches use AlexNet variants and were pre-trained on ImageNet without labels except the ImageNet labels and Random entries.
- Table 6
    - <img src="https://user-images.githubusercontent.com/67457712/227821818-66866861-cdf6-47a9-8575-a1ebcdcb8a9d.png" width="500">
    - Task & Dataset Generalization: Places top-1 classification with linear layers. We compare our unsupervised feature learning approach with other unsupervised approaches by training logistic regression classifiers on top of the feature maps of each layer to perform the 205-way Places classification task (Zhou et al., 2014). All unsupervised methods are pre-trained (in an unsupervised way) on ImageNet. All weights are frozen and feature maps are spatially resized (with adaptive max pooling) so as to have around 9000 elements. All approaches use AlexNet variants and were pretrained on ImageNet without labels except the Place labels, ImageNet labels, and Random entries.
- Table 7
    - <img src="https://user-images.githubusercontent.com/67457712/227821916-3fbfa1df-7878-4f54-8b4d-ee3bfda663c6.png" width="500">
    - Task & Dataset Generalization: PASCAL VOC 2007 classification and detection results, and PASCAL VOC 2012 segmentation results. We used the publicly available testing frameworks of Krahenb ¨ uhl et al. (2015) for classification, of Girshick (2015) for detection, and ¨ of Long et al. (2015) for segmentation. For classification, we either fix the features before conv5 (column fc6-8) or we fine-tune the whole model (column all). For detection we use multi-scale training and single scale testing. All approaches use AlexNet variants and were pre-trained on ImageNet without labels except the ImageNet labels and Random entries. After unsupervised training, we absorb the batch normalization units on the linear layers and we use the weight rescaling technique proposed by Krahenb ¨ uhl et al. (2015) (which is common among the unsupervised methods). ¨ As customary, we report the mean average precision (mAP) on the classification and detection tasks, and the mean intersection over union (mIoU) on the segmentation task.