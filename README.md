# Learning to Amend Facial Expression Representation via De-albino and Affinity
                                                          Jiawei Shi and Songhao Zhu
                                        Nanjing University of Posts and Telecommunications
                                                                    Nanjing, China
                                                   {1319055608, zhush}@njupt.edu.cn


## Abstract
  Facial Expression Recognition (FER) is a classification task that points to face variants. Hence, there are certain affinity features between facial expressions, receiving little attention in the FER literature. Convolution padding, despite helping capture the edge information, causes erosion of the feature map simultaneously. After multi-layer filling convolution, the output feature map named albino feature definitely weakens the representation of the expression. To tackle these challenges, we propose a novel architecture named Amending Representation Module (ARM). ARM is a substitute for the pooling layer. Theoretically, it can be embedded in the back end of any network to deal with the Padding Erosion. ARM efficiently enhances facial expression representation from two different directions: 1) reducing the weight of eroded features to offset the side effect of padding, and 2) decomposing facial features to simplify representation learning. In terms of data imbalance, we designed a minimal random resampling (MRR) scheme to suppress network overfitting. Experiments on public benchmarks prove that our ARM boosts the performance of FER remarkably. The validation accuracies are respectively **90.42%** on RAF-DB, **65.2%** on Affect-Net, and **58.71%** on SFEW, exceeding current state-of-theart methods. The paper has been submitted in [arXiv.org](https://arxiv.org/abs/2103.10189).

## Amend-Representation-Module

![image](https://github.com/sunmusik/Amend-Representation-Module/blob/master/imgs/Net.png)

Overview of Amend Representation Module (ARM). The ARM composed of three blocks replaces the pooling layer
of CNN. The solid arrows indicate the processing flow of one feature map, and the dotted arrows refer to the auxiliary flow of
a batch. It should be noted that the relationship between the two channels requires the de-albino kernel to be single-channel
and unique.

## Train
- Requirements

  Torch 1.7.1, APEX 0.1, and torchvision 0.8.2.
  
  For APEX 0.1 (Linux):
  
	  git clone https://github.com/NVIDIA/apex
	  cd apex
	  pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./
	  
- Data Preparation

  Download [RAF-DB](http://www.whdeng.cn/RAF/model1.html#dataset) dataset, and make sure it have a structure like following:
 
	```
	- datasets/raf-basic/
		 EmoLabel/
		     list_patition_label.txt
		 Image/aligned/
		     train_00001_aligned.jpg
		     test_0001_aligned.jpg
		     ...
	```
- Training
	```
	python src/train_raf-db.py
	```


- Testing
	
	```
	python src/test_raf-db.py --checkpoint *.pth
	```
   	
- Testing and Confusion Matrix
	
	```
	python src/test_raf-db.py --checkpoint *.pth --plot_cm
	```



## Result
- Confusion Matrix on RAF-DB

<div align=center><img src="https://github.com/JiaweiShiCV/Amend-Representation-Module/blob/master/imgs/acc_rafdb.png" width="600" height="450" /></div>



# Citation
If you use the sample code or part of it in your research, please cite the following:

```
@ARTICLE{2021arXiv210310189S,
       author = {{Shi}, Jiawei and {Zhu}, Songhao},
        title = "{Learning to Amend Facial Expression Representation via De-albino and Affinity}",
      journal = {arXiv e-prints},
     keywords = {Computer Science - Computer Vision and Pattern Recognition},
         year = 2021,
        month = mar,
          eid = {arXiv:2103.10189},
        pages = {arXiv:2103.10189},
archivePrefix = {arXiv},
       eprint = {2103.10189},
 primaryClass = {cs.CV},
       adsurl = {https://ui.adsabs.harvard.edu/abs/2021arXiv210310189S},
      adsnote = {Provided by the SAO/NASA Astrophysics Data System}
}
```

## License
ARM is available under the MIT license. See the LICENSE file for more info.
