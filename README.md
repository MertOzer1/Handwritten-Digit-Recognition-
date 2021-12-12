# HANDWRITTEN-DIGIT-RECOGNITION
Handwritten Digit Recognition of the Printed ‘Particle Board Cutting and Edge Banding Information Form’ Using OCR (Optical Character Recognition)
# ABSTRACT
I noticed that in a furniture cutting and edge banding company, which transfers the data received from the customer to the computer by having the form filled in handwriting, it takes a long time to transform and control the form into the digital environment by a human. To solve this problem, a system has been developed by the usage of machine learning. As a result, although the average accuracy rate of the examined samples is not completely reliable with a result of 72.1977 percent, the research findings suggest that this tech-enabled system can save time for furniture materials processing.
# 1	INTRODUCTION
In our constantly changing, transforming, and developing world, we have seen that many manual and labor-intensive tasks can now be performed in seconds by machines and smart technologies. This development has been accelerated by machine learning, which has been the key driver behind our increasingly automated world.

In this research, I investigated how machine learning and optical character recognition systems can make our lives easier in the field of furniture materials processing. In other words, in this paper, I will explain how the cutting and banding form, which is traditionally filled in manually is instead transferred to an excel file with the text detection method. In this process, I paid attention to the way the machine accepts data in terms of usability and to carry out the process with the minimum effort.
	
## 1.1	UNDERSTANDING THE PROBLEM
Every summer throughout high school, I did an internship at a local furniture business. Their business divided furniture materials such as chipboard or medium density fiberboard into small pieces used for the construction of home furniture (i.e., cabinets, tables). Piece chipboard dimensions are requested by retail furniture manufacturers, and the dimensions can vary widely. These desired dimensions are handwritten by the customer on a printed form and delivered to the company for processing. 

For the machine to detect these forms, someone must meticulously transfer them to the computer one by one, line by line, measure by measure. In addition to taking a lot of time, there is a significant risk of mistakes due to potential human error. Fortunately, machine learning can be used to expedite this process and make it more efficient.

There are two important factors for this algorithm to be effective: high accuracy and ease of use. I aim to achieve a result close to the human error rate, or even exceed it. Otherwise, if it makes more mistakes than a human, such an algorithm cannot be used, and further improvements needs to be developed. Furthermore, ease of use is an important consideration because a technical algorithm may require high-end programming knowledge that the everyday user may not know.
## 1.2	UNDERSTANDING THE FORM
<img src="Images/Figure 1 Empty Form.png" height="750">
<img src="Images/Figure 2&3 Filled Form.png" height="750">
Figure 1 shows the blank form of the data processing form taken into consideration. The second figure shows the completed form as an example. The form is divided into two parts, cutting and banding. The first 4 columns are used for the features of the parts to be cut, while the last 4 columns are used to express the sides of the part to be edge banded.
	
To begin with the cutting side, 1st column represents the ordinal number. So, each piece has its own serial number. The second column represents the length, and the third column represents the width of the piece to be cut. The last column in the cutting section is there to indicate how many numbers of that piece are requested. 

If we move on to the banding part, the options for which section is requested to be banded are listed as follows:

| Length 1 | Length 2 | Width 1 | Width 2 | No Marking | All |
| --- | --- | --- | --- | --- | --- |
| One length	| Both lengths	| One width	| Both widths	| No banding	| Every side |

In the edge banding part, there is no specific marking style. This is completely up to the customer's preference, and crosses (x), checkmarks (√), dashes (-) can be given as examples, but the options are not limited to these. 
	
The form does not have to be filled in completely, so if only 10 different parts are required to fill out the customer's needs, it will be sufficient to fill in just the 10 lines.
## 1.3	POSSIBLE SOLUTIONS 
As one can imagine, it takes a long time to manually transfer handwritten forms to the computer environment. Therefore, there is a clear demand for an automated system that has the capabilities to expedite the processing of furniture materials. For this, other applications that meet similar needs can be examined. The most popular of these softwares are Amazon Textract and Google Vision API.
	
“Amazon Textract is a machine learning service that automatically extracts text, handwriting, and data from scanned documents that goes beyond simple optical character recognition (OCR) to identify, understand, and extract data from forms and tables.” 

“Cloud Vision allows developers to easily integrate vision detection features within applications, including image labeling, face and landmark detection, optical character recognition (OCR), and tagging of explicit content.” 

These two programs perform similar functions in terms of working strategies, but they have one downside: they are not free. They do, however, grant free entitlements up to a certain use. In this research paper, I will investigate alternative solutions to these systems.

# 2	COMPONENTS OF THE METHOD USED
Many different algorithms and collaborations have been used to solve the problem mentioned in the introduction. Python was used as the programming language.
## 2.1	GOOGLE COLABORATORY
“Google Colaboratory allows anybody to write and execute arbitrary python code through the browser, and is especially well suited to machine learning, data analysis and education.” 
	
Google Collaboratory was used in this study because I was able to run code in Google’s cloud servers. So, I leveraged the power of Google's hardware without needing any GPU or CPU in my own computer.
## 2.2	OPTICAL CHARACTER RECOGNITION (OCR)
“Optical character recognition is the electronic or mechanical conversion of images of typed, handwritten or printed text into machine-encoded text, whether from a scanned document, a photo of a document, a scene-photo or from subtitle text superimposed on an image.”
	
This process can be divided into text detection and text recognition. 
## 2.3	DOCTR
The Github page named "mindee/doctr" was used to parse the textual information from the documents. Doctr stands for “Document Text Recognition.”
## 2.4	CONVOLUTION NEURAL NETWORKS
“A Convolutional Neural Network is a Deep Learning algorithm which can take in an input image, assign importance (learnable weights and biases) to various aspects/objects in the image and be able to differentiate one from the other.” In this study, different pictures of forms containing numbers were examined and classified according to which value they were closer to. In addition, a confidence ratio has emerged that reflects how much the algorithm thinks the output is closest to.
## 2.5	RESNET-50 AND VGG 16
“ResNet-50 is a convolutional neural network that is 50 layers deep. You can load a pretrained version of the network trained on more than a million images from the ImageNet database.” “VGG-16 is a convolutional neural network that is 16 layers deep. You can load a pretrained version of the network trained on more than a million images from the ImageNet database.” “ImageNet is a dataset of over 15 million labeled high-resolution images belonging to roughly 22,000 categories.”
	
In this study, instead of teaching the machine to recognize text from scratch, I used a pre-trained model because otherwise it would be a very time-consuming process requiring many samples to train the model. Moreover, I have neither enough people nor enough examples to label the picture to make such a study possible. 
## 2.6	ORDERING THE OUTPUT
Each tile detected has many values. One of them is the geometry value. And it contains a list of four separate numbers. These can be shown as ((xmin, ymin), (xmax, ymax)) respectively. By using these values that emerge from the entire form, it emerges in JSON format, which is a complex state. These values were then aligned according to their rows and columns for each form and converted into a human-understandable format.
## 2.7	REPLACING SOME VALUES
When the results were evaluated, it was seen that some typical numbers could be confused with certain letters or symbols. Since the purpose of the developed application is to detect purely numbers, I replaced some values confused by the algorithm with the numbers that should be in the dataset. Their list is as follows:

| Displaced Value |	g	| i	| L	| I	| ı |	s | S | O	| o |	-	| J	| / |	( |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| New Value	| 9	| 1	| 1 |	1	| 1	| 5	| 5	| 0	| 0	| . |	1 |	1 | 	1 |
# 3	 RESULTS 
To examine the result of the tested model, 4 sample cutting banding forms were selected. While making this selection, I chose 2 samples in good condition and 2 samples in bad condition. At the same time, I considered that they have different characteristics for comparison. Each example will be examined in detail.
## 3.1	GETTING TO KNOW THE EXAMPLES 
<img src="Images/Figure 2&3 Filled Form.png" height="750">
<img src="Images/Figure 4.png" height="750">
<img src="Images/Figure 5.png" height="750">
<img src="Images/Figure 6.png" height="750">

The first two examples are relatively cleaner and neater compared to the last two examples. 
	
In the first example, there is no other roughness except the scribble on line 13 and the long line on line 20. In the second, extra text was written on the banding part in just two lines.

In the 5th figure, everything seems to be a mess. To begin with, the paper was scanned skewed on the scanner. The decimal digits were written in a different format without the use of dots. Number 7 is interesting. The part data is split, so rows 5 and 6 are empty. There are also inscriptions in orange around the form and between important data. In addition to the skipped row in the last example, line 15 has a scribble. Furthermore, the picture was taken with a camera instead of being taken from the scanner, and some areas were shaded.
## 3.2	CALCULATING THE REPORT ACCURACY
To calculate the report accuracies, the following formula is used:

Report Accuracy=(Number of correct predictions)/(Total number of numbers)*100

Report Accuracy=(Total number of predictions-Number of wrong predictions)/(Total number of numbers)*100
	
Sequence numbers were not considered when making this calculation because they are already computer-printed numbers. I also excluded the banding part was also not taken into account while making the calculations, because when I examined the results, different markings did not bring the desired result. Since the order of the markings in the banding is also important, and the required ordering cannot be made, it will not be evaluated to measure the efficiency of the model. Another reason for this is that some of the markings made in this section were different such as crosses and dashes, and the algorithm detects them accordingly. Detailed information on this subject is mentioned in the suggestions section.

### 3.2.1	Decent Examples
#### 3.2.1.1	First example
The numbers of lines and columns equal to 27 and 3, respectively. So, the total number of values is 27 x 3= 81. The incorrect values are listed below:

| The value read by the algorithm	| The actual value	| The number of repetitions |
| --- | --- | --- |
| 17	| 12 |	1 |
| 272	| 27.2 | 1 |
| 1675	| 167.5 | 1 |
| 27	| 22	| 1 |
| 345	| 34.5	| 1 |
| 348	| 34.8	| 1 |
| “Didn’t read” | 4 |	1 |
| 652	| 65.2	| 1 |

Report Accuracy=(81-8)/81*100=90.1235

It can be seen from here that the 6 values, which were written in a dominant manner by scribbling, were detected without any problems.
#### 3.2.1.2	Second example
The numbers of lines and columns equal to 26 and 3, respectively. So, the total number of values is 27 x 3= 78. The incorrect values are listed below:

| The value read by the algorithm	| The actual value	| The number of repetitions |
| --- | --- | --- |
| X	| 1	|4 |
| “Didn’t read” |	1 | 4 |
| J15	| 115	| 1 |
| 564	| 56.4	| 1 |
| 4L14	| 41.4	| 1 |
| M14	| 111.4	| 1 |
| M1r4	| 111.4	| 1 |
| 53	| 58	| 2 |
| 115	| 11.5	| 1 |
| 594	| 59.4	| 1 |
| 53.2	| 58.2	| 1 |
| 30	| 80	| 1 |

Report Accuracy=(78-19)/78*100=75.6410

There are two major problems with this example. The algorithm mostly did not detect the number 1 written as a straight bar. Some 8's read like 3's, depending on the handwriting of the person writing it. This means that different types of handwriting may cause problems for the algorithm. Therefore, it is necessary to be careful when using this algorithm in real life.
### 3.2.2	Poor Quality Examples
#### 3.2.2.1	Third Example
The number of lines and columns equals to 8 and 3 respectively. So, the total number of values is 8 x 3= 24. The incorrect values are listed below:
- Didn’t read both two 1s. 
- All 9 decimal numbers written in a different were read without dots.
- The algorithm defined three 7's written in different styles, one as 8, one as 2, and the last as 7. So only one is correct. (Since 8 read values also contain another error, these are considered as only one error when calculating the value of accuracy.)
- The last line shifted due to skew.
- Some values written in small are wrongly classified. <br>
Report Accuracy=(24-13)/24*100=45.8333

#### 3.2.2.2	Forth Example
The number of lines and columns equals to 19 and 3 respectively. So, the total number of numbers is 19 x 3= 57. The incorrect values are listed below:
| The value read by the algorithm	| The actual value	| The number of repetitions |
| --- | --- | --- |
| 98	| 38 |	1 |
| )	| 5	| 1 |
| 464	| 46.4 |	1|
| “Didn’t read” |	1 |	2 |
| 12414	| 124.4 |	1 |
| 648	| 64(also a scribble) |	1 |
| dJ	| 4	| 1 |
| 6416	| 64.6	| 1 |
| 443 |	49.3	| 1 |
| “Didn’t read” | 4 |	2 |
| 3416 | 34.6 |	1 |

Report Accuracy=(57-13)/57*100=77.1930
# 4	DISCUSSION
Overall, although the accuracies are not high enough (90.1235, 75.6410, 45.8333,77.1930), these rates can be increased by improving some of the limitations highlighted in this research paper.
## 4.1	LIMITATIONS, SUGGESTIONS, AND INFERENCES
- This algorithm was not successful as the algorithm cannot detect empty cells in the banding section. In other words, the algorithm cannot identify areas that should not be taped. To solve this problem, cells can be taught to the algorithm with the labelling method. Since the form is always the same form, it will work because there is no change.
- Many different shapes are used for marking in the banding section. To solve this problem, the pre-filled forms can be examined one by one, and a list of possible different methods can be drawn up, and they can all be linked to a single symbol.
- The algorithm did not recognize some points and produced very large numbers. However, since this is a furniture material cutting form and there is a certain maximum size of the raw material, entries exceeding this limit value can be marked by the program for human eye control.
- One of the samples examined was taken with a camera, and as a result, some value left in the dark could not be identified or were misidentified. To get the best results from this software, it is necessary to use a scanner or a professional scanner mobile application.
- Scanning the paper crookedly, as in the 3rd example, causes the lines to be detected as shifted. Although this can easily be fixed manually, it makes sense to take care to scan the form straight.
- Although the code works properly in Google Colaboratory since this system will be used all the time, it takes time to run every code and makes it difficult to use. Different alternatives should be tried to use the system more effectively.
- Sometimes, the customer can write incorrectly, make doodles, as in the 1st example, and this can lower the accuracy rate of the algorithm. Therefore, it is necessary to raise awareness of this issue to potential users and recommend to them they should use correction fluid when they encounter a situation like this.
- The form also contains the customer's information and any notes they want to add. While the algorithm works more effectively when exposed to numbers only, cropping scanned files is an extra workload. For this, a system that automatically scans the place where the necessary information is can be developed and integrated into the software.
- In places where the task is edge banding, some customers do not deduct the PVC cuts that need to be adjusted. Since the banding also has a thickness, the desired size of the output can be different. If it is an area that needs to be worked on, even millimeters can be important. For this reason, a code can be written that determines the deduction of PVC cuts according to which edges are taped, which can be activated selectively when necessary.

## 4.2	CONCLUSION
Although, the performance of the algorithm seems to be low given the data, the results of this paper suggest that a machine learning algorithm is still preferable to doing everything by hand. It is essential that the entire process be carried out by a supervisor, and that there is still someone to check for possible incorrect values. At the same time, this person must manually enter the entire banding part. The most promising aspect of the study is that the machine learning algorithm has room for growth via improvements to the limitations observed in this study. In other words, if the applications given in the LIMITATIONS, SUGGESTIONS, AND INFERENCES sections are implemented, the developed algorithm will greatly facilitate the work of many businesses using a similar information form.
# 5	REFERENCES
Deep Network designer. ResNet-50 convolutional neural network - MATLAB. (n.d.). Retrieved from https://www.mathworks.com/help/deeplearning/ref/resnet50.html;jsessionid=514a4e37c08728c23002e7a01979. 

Deep Network designer. VGG-16 convolutional neural network - MATLAB. (n.d.). Retrieved from https://www.mathworks.com/help/deeplearning/ref/vgg16.html;jsessionid=39c7e563045899e404f9fcdb8d2d. 

Doctr.io¶. doctr.io - docTR 0.4.1a0-git documentation. (n.d.). Retrieved from https://mindee.github.io/doctr/io.html#document-structure. 

Google. (n.d.). Cloud vision documentation &nbsp;|&nbsp; cloud vision API &nbsp;|&nbsp; google cloud. Google. Retrieved from https://cloud.google.com/vision/docs/. 

Mindee. (n.d.). Mindee/doctr: Doctr (document text recognition) - a seamless, high-performing &amp; accessible library for OCR-related tasks powered by deep learning. GitHub. Retrieved from https://github.com/mindee/doctr. 

Molter, C. (2002). Amazon Textract. Amazon. Retrieved from https://aws.amazon.com/tr/textract/. 

Saha, S. (2018, December 17). A comprehensive guide to Convolutional Neural Networks - the eli5 way. Medium. Retrieved from https://towardsdatascience.com/a-comprehensive-guide-to-convolutional-neural-networks-the-eli5-way-3bd2b1164a53. 

VGG16 - convolutional network for classification and detection. VGG16 - Convolutional Network for Classification and Detection. (2021, February 24). Retrieved from https://neurohive.io/en/popular-networks/vgg16/.





















