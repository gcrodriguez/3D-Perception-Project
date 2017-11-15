## Project: Perception Pick & Place
### This writeup contains the analyses made for the 3D perception project in order to identify objects in three different scenarions as requested.

---

## [Rubric](https://review.udacity.com/#!/rubrics/1067/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Exercise 1, 2 and 3 pipeline implemented 

Completing the three mentioned exercises gave the base to implement the code and identify the object as project requisition. Without training and learning with these exercises make the object identification was practically an impossible task. After implementing all filtering steps, RANSAC algorithm, cluster segmentation and a lot of try and error, the parameters presneted in the table below were achieved and considered reasonable for object recognition. The objects segmented and clustered are shown in the images of the final of this section with their identification, showing the success of the algorithm.

Leaf Size | z axis min | z axis max | Cluest Tol. | Min. Cluster Size | Max. Cluster Size 
--- | --- | --- | --- | --- | ---
0.01 | 0.77 | 1.1 | 0.01 | 0.05 | 50 | 1500 

The first step was to capture the objects and then train them to verify the accuracy and appropriate classifier that should be implemented to achieve a reasonable object identification. For the first attempts, 5 different positions were stipulated for each object. Considering the linear classifier and rgb method, the first results showed bad results (as image below) indicating the necessity of more different positions. 

![image-1](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/exercicio3_confusematrix_com_histogram_5capturas_rgb_linear.png)

After defining 10 positions for each object (and then it can be concluded that this quantity was satisfactory) and changing to hsv method, the next task was to identify which of the classifiers would result in better accuracy of the results. By verifying the linear, rbf, poly and sigmoid classifiers through the results presented in the images below, it was possible to conclude that the linear classifier gave the most accurate results, allowing the greater distinction between the objects.

Linear

![image-2](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/exercicio3_confusematrix_com_histogram_10capturas_hsv_linear.png)

![image-3](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/results_com_histogram_10capturas_hsv_linear.png)

Poly

![image-4](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/exercicio3_confusematrix_com_histogram_10capturas_hsv_poly.png)

![image-5](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/results_com_histogram_10capturas_hsv_poly.png)

RBF

![image-6](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/exercicio3_confusematrix_com_histogram_10capturas_hsv_rbf.png)

![image-7](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/results_com_histogram_10capturas_hsv_rbf.png)

Sigmoid

![image-8](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/exercicio3_confusematrix_com_histogram_10capturas_hsv_sigmoid.png)

![image-9](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/results_com_histogram_10capturas_hsv_sigmoid.png)

With the mentioned parameters and linear classifier, the objects could be correctly segmented, clustered and identified as can be observed in the images below.

Object Segmentation

![image-10](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/object_recon.png)

Object clustering

![image-11](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/object_recon_cluster.png)

Point cloud

![image-12](https://github.com/gcrodriguez/3D-Perception-Project/blob/master/point_cloud.png)

 ####Note: After a while, the create object moves from its position and then vanish (this identificantion was not possible anymore). But, in the cluesterd objects image, this was object was identified. Probably this is an error and it was not taken into account.

### Pick and Place Setup

For the project code, initially it was used the same method, parameters and classifier. When running it the results obtained were terrible. Then it was clear that the parameters had to change and more of try and error was necessary. Adding also the outlier filter in order to eliminate the thrash points, the parameters of the table below ere obtained.

Leaf Size | z axis min | z axis max | Cluest Tol. | Min. Cluster Size | Max. Cluster Size 
--- | --- | --- | --- | --- | ---
0.005 | 0.06 | 2.0 | 0.05 | 0.05 | 50 | 1500 








#### 1. For all three tabletop setups (`test*.world`), perform object recognition, then read in respective pick list (`pick_list_*.yaml`). Next construct the messages that would comprise a valid `PickPlace` request output them to `.yaml` format.

And here's another image! 
![demo-2](https://user-images.githubusercontent.com/20687560/28748286-9f65680e-7468-11e7-83dc-f1a32380b89c.png)

Spend some time at the end to discuss your code, what techniques you used, what worked and why, where the implementation might fail and how you might improve it if you were going to pursue this project further.  



