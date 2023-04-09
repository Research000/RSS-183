# Supplementary materials for RSS-183
## Supplementary materials：
>
We have added the following experiments and results displays based on the reviewers' comments:<br />
>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.Comparison with DISP (GAN-based local feature learning method). This experiment will add to the part D of section Ⅳ. Experiments.<br />
>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.Real image comparisons between the baseline and our proposed local feature on Aachen Day-Night datasets. The display will be insert in visual localization task (Ⅳ.Experiments. D).<br />
>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3.Experiment for searching appropriate beta value to avoid background texture in Fourier transform-based domain augmentation. This experiment will add to the part E of Experiments section. 

**1.Comparison with DISP**
>
Due to the fact that the GAN-based local feature learning method DISP mentioned in our paper is not open-source, we conducted experiments using the same experimental pipeline as DISP and compared the results on the Aachen Day Night dataset to those of DISP. We employ the same computation-efficient hierarchical localization concept as proposed in [62]. First, we find candidate images by matching the query against images in the database using NetVLAD (Abbreviated as NV) [63] as a global image descriptor. The 6-DoF camera pose is then calculated by matching local features between the query image and the retrieved candidates. We will compare it to two versions of our proposed features, one if which only conducts Fourier transform-based data augmentation during representational learning, the other uses domain augmentation and feature distribution alignment strategies. The comparison results are shown in Table.1. 

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

As seen, the proposed local feature only with Fourier transform-based domain augmentation for representational learning is comparable to that of DISP, indicating that Fourier transform-based domain augmentation method can also increase domain diversity without requiring additional time-consuming training of GAN networks. The result is considerably enhanced by the addition of a domain feature alignment strategy, further demonstrating the validity of the proposed strategy.

**2.Real image comparisons**
>
As shown in Equation 9, $\beta$ = 0 will render the result the same as the original source image. In contrast, when $\beta$ = 1.0, the amplitude of the result will be replaced by the target image. To determine an appropriate beta value, we conducted some experiments. First, we performed image testing with varying beta values and noticed that when beta was more than or equal to 0.03, the artifacts in transformed images became obvious. Subsequently, we sampled numerous beta values (0.01, 0.015, 0.02, 0.025) less than 0.03 to train the network (baseline with Fourier transform-based domain augmentation), and the performance of models trained with beta values 0.01, 0.015, 0.02 are comparable, model trained with beta value 0.025 was a litter worse. Thus, in the experiments that follows we chose one of the three beta values (0.01, 0.015, 0.02) at random for each training iteration. 

![输入图片描述](README1_md_files/3b43f800-d555-11ed-ad9c-736d76abbe05.jpeg?v=1&type=image)

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
      <td><p align="center">**71.87**</p></td>
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
      <td><p align="center"> </p></td>
	</tr >

</table>
