# Appendix A - Detector Analysis: Additional Thresholds
To further demonstrate that no detector is dominated by another, we repeated the experiments presented in Table II, but with a fixed false positives rate 5\%. 
We argue that this scenario is typical of actual use cases where organizations determine a fixed false positives rate, setting its value at a level that would enable human experts to analyze all alerts.
The results of our additional experiments are presented in the below table. 
The results show that for both datasets -- PE and APK -- no detector is dominated by another. 
Moreover, the large variance in the detection rates for the originally misclassified files -- larger than those presented in Table II in some cases -- further supports our claim that an intelligent selection of detector subsets can maintain high performance at a fraction of the resources-use.
![](https://user-images.githubusercontent.com/45119337/95994553-1e58e880-0e39-11eb-8716-8693b1d0a954.jpg)

# Appendix B - Influence of Changes in the Classification Threshold on Baseline Performance
In order to show that SPIREL outperforms all baselines regardless of their confidence threshold settings, we conducted an additional set of experiments. The below figure presents our additional experiments. We ran each baseline in four additional configurations, with the confidence score threshold set to different values. The chosen threshold values were set to 0.3, 0.4, 0.6, and 0.7 (0.5 is the original value presented in Figure 4). Our results clearly show that SPIREL outperforms all baselines, regardless of their chosen configurations.
![](https://user-images.githubusercontent.com/45119337/95996170-0c784500-0e3b-11eb-85b7-01bb88f8ccc5.png)

# Appendix C -  DRL Agent Action Distribution
In continuation to the analysis presented in subsection V-C, we now present in full detail the detector combinations chosen by each SPIREL experiment. The results are presented in 
the below table and include the description of the detector subset, its average runtime and the percentage of files (out of all those analyzed) on which this particular detectors subset was applied.
![istribution of detector combination choices madeby the agent for each of our experimental policies](https://user-images.githubusercontent.com/45119337/95997405-6cbbb680-0e3c-11eb-95f7-2e71e6f92f6d.jpg)

# Appendix D - Training Times
The training time required for our DRL agent to convergence change according to experimental settings. The experiments conducted in this study had the same action space and state representation, and a varying reward function (i.e., confusion matrix) that indicates the relation between correct and incorrect classification. The below table specifies for every dataset the amount of epochs and the average total time required for it to convergence. 
![he  training  duration  and  number  of  epochsrequired to converge for both datasets](https://user-images.githubusercontent.com/45119337/95997919-f9667480-0e3c-11eb-81de-63d53cf8e381.jpg)

# Appendix E - Training Times
As mentioned in the introduction Section, there is no existing ML approach for the dynamic selection of detector subsets while a file is being analyzed. 
For this reason, any baseline we compare our approach to must consist of a preselected detector subset (i.e., defined prior to running). 
We therefore compare our method to all possible detector subset combinations and their aggregation methods. 

Given that we have four detectors and three aggregation methods (or, majority, and stacking), we evaluated 48 baselines for each of our datasets.
The below two tables (PE and APK accordingly related) present the F1 score and average runtime for all runs. 
An analysis of the results shows that \MethodName consistently outperforms all of the baselines. 
More specifically, for every desired level of performance (with the exception of the poorest performing baselines which consist of a single detector), there is a version of our proposed method that can result in the equivalent or better performance at a reduced runtime. 
\MethodName’s superior performance is particularly evident when compared to the top performing baselines. 
For both datasets, our approach outperformed the top performing baselines while being more computationally efficient.
![erformance and mean time values of all possible detector combinations for PE files](https://user-images.githubusercontent.com/45119337/95998576-accf6900-0e3d-11eb-89d0-12fc88739771.jpg)
