# Supplementary materials for RSS-183
## Supplementary materials：
>
We have added the following experiments and results based on the reviewers' comments:<br/>
>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; * Search for appropriate β values to eliminate background texture in Fourier transform-based domain augmentation. This experiment will be added to part E of Section Ⅳ. Experiments.<br/>
>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; * Comparison to the DISP (GAN-based local feature learning method). This experiment will be added to part D of section Ⅳ. Experiments.<br/>
>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Comparisons of keypoints matching results with baseline method using Aachen Day-Night actual image datasets. 

***A. Experiment on selecting β values***
>
As demonstrated by Equation 9, β=0 will produce the same result as the original source image. In contrast, when β equals 1, the result's amplitude is replaced by that of the target image. Experiments were conducted in order to determine a suitable β value. First, we tested images with varying β values and observed that when β was greater than or equal to 0.03, image artefacts became obvious, as shown in Fig. 1. Subsequently, we sampled numerous β values (0.01, 0.015, 0.02, and 0.025) less than 0.03 to train the network (baseline with Fourier transform-based domain augmentation). We use the open-source code of ASLFeat (CVPR) as the baseline. The performance of models trained with β values 0.01, 0.015, and 0.02 are comparable, the performance of the model trained with β value 0.025 was lower. The test results on Image Matching task with HPatches are shown in Table Ⅰ. For each iteration in the training process, one of the three β values (0.01, 0.015, or 0.02) was chosen at random. This β selection strategy is employed for all subsequent experiments.<br/>




![输入图片描述](https://github.com/Research000/RSS-183/blob/main/cut_2.JPG)<br/>

Figure 1. Examples of images after Fourier transform-based domain augmentation with different β values. When β value is greater than or equal to 0.03 the image artefacts became obvious.<br/>

TABLE I. Evaluation results of local featurs learned with various β value on HPatches
<table>
	<tr>
	    <th >$\beta$ value</th>
	    <th >Precision</th>
	    <th >Recall</th>  
	    <th >MMA</th> 
	    <th >Homo.</th> 
	</tr >
  <tr>
      <td><p align="center">baseline</p></td>
      <td><p align="center">72.27</p></td>
      <td><p align="center">63.63</p></td>
      <td><p align="center">70.83</p></td>
      <td><p align="center">73.51</p></td>
	</tr >
 <tr>
      <td><p align="center">0.01</p></td>
      <td><p align="center">73.20</p></td>
      <td><p align="center">71.87</p></td>
      <td><p align="center">71.22</p></td>
      <td><p align="center">74.22</p></td>
	</tr >
   <tr>
      <td><p align="center">0.015</p></td>
      <td><p align="center">73.16</p></td>
      <td><p align="center">71.73</p></td>
      <td><p align="center">71.19</p></td>
      <td><p align="center">74.34</p></td>
	</tr >
<tr>
      <td><p align="center">0.02</p></td>
      <td><p align="center">73.26</p></td>
      <td><p align="center">71.70</p></td>
      <td><p align="center">71.24</p></td>
      <td><p align="center">74.28</p></td>
	</tr >
<tr>
      <td><p align="center">0.025</p></td>
      <td><p align="center">73.08</p></td>
      <td><p align="center">71.66</p></td>
      <td><p align="center">71.15</p></td>
      <td><p align="center">73.94</p></td>
	</tr >

</table><br/>


***B. Comparison with GAN based learning method***
>
Since the GAN-based local feature learning method DISP [30] mentioned in our paper is not open-source, we conducted experiments using the same experimental pipeline as DISP and compared the results on the Aachen Day Night dataset to those of DISP [30]. We employ the same efficient hierarchical localization concept proposed in [62]. Using NetVLAD (Abbreviated NV) [63] as a global image descriptor, we first locate candidate images by matching the query against images in the database. The 6-DoF camera pose is then calculated by matching the query image's local features to those of the retrieved candidates. We compare it to two versions of our proposed features, one of which employs only Fourier transform-based data augmentation during representational learning and the other of which employs domain augmentation and feature distribution alignment strategies. The results of the comparison are shown in Table Ⅱ.<br/>

TABLE II. Results on visual localization for different distance and orientation thresholds
<table>
	<tr>
	    <th rowspan="2">Method</th>
	    <th colspan="3">day</th>
	    <th colspan="3">night</th>  
	</tr >
  <tr>
	    <th >(0.25m, 2°)</th>
	    <th>(0.5m, 5°)</th>
	    <th>(5m, 10°)</th>  
      <th >(0.25m, 2°)</th>
	    <th>(0.5m, 5°)</th>
	    <th>(5m, 10°)</th> 
	</tr >
  <tr>
	    <td><p align="center">NV+DISP</p></td>
      <td><p align="center">79.2</p></td>
      <td><p align="center">87.4</p></td>
      <td><p align="center">93.9</p></td>
      <td><p align="center">62.2</p></td>
      <td><p align="center">72.4</p></td>
      <td><p align="center">81.6</p></td>
	</tr >
 <tr>
	    <td><p align="center">NV+SADGFeat (data)</p></td>
      <td><p align="center">80.4</p></td>
      <td><p align="center">86.8</p></td>
      <td><p align="center">94.2</p></td>
      <td><p align="center">63.8</p></td>
      <td><p align="center">71.8</p></td>
      <td><p align="center">83.0</p></td>
	</tr >
   <tr>
	    <td><p align="center">NV+SADGFeat(data&align)</p></td>
      <td><p align="center">82.7</p></td>
      <td><p align="center">88.4</p></td>
      <td><p align="center">97.5</p></td>
      <td><p align="center">68.6</p></td>
      <td><p align="center">73.4</p></td>
      <td><p align="center">85.8</p></td>
	</tr >
</table>

As observed, the proposed local feature only with Fourier transform-based domain augmentation for representational learning is comparable to that of DISP, indicating that Fourier transform-based domain augmentation can also increase domain diversity without requiring additional time-consuming GAN network training. The addition of a domain feature alignment strategy results in further improvement, proving the validity of the proposed strategy.<br/>  

 
***C. Comparison of Keypoints Matching on real images***<br/>

In the visual localization task with the Aachen Day-Night datasets, we illustrate local feature matching for image pairs in Fig. 2. It can be seen that our proposed local feature gets more matching keypoints pairs than that of the baseline under environment changing conditions. It is extremely advantageous for the long-term localization of robots in the actual world.


![输入图片描述](https://github.com/Research000/RSS-183/blob/main/cut_1.JPG)<br/>

Figure 2. Examples for local feature matching for image pairs taken from Aachen Day-Night datasets. The left column displays the baseline's matching results, while the right column displays that of ours <br/>
