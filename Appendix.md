# Appendix A - Detector Analysis: Additional Thresholds
To further demonstrate that no detector is dominated by another, we repeated the experiments presented in Table II, but with a fixed false positives rate 5\%. 
We argue that this scenario is typical of actual use cases where organizations determine a fixed false positives rate, setting its value at a level that would enable human experts to analyze all alerts.
The results of our additional experiments are presented in the below table. 
The results show that for both datasets -- PE and APK -- no detector is dominated by another. 
Moreover, the large variance in the detection rates for the originally misclassified files -- larger than those presented in Table II in some cases -- further supports our claim that an intelligent selection of detector subsets can maintain high performance at a fraction of the resources-use.
![](https://user-images.githubusercontent.com/45119337/95994553-1e58e880-0e39-11eb-8716-8693b1d0a954.jpg)

#Appendix B - Influence of Changes in the Classification Threshold on Baseline Performance
In order to show that SPIREL outperforms all baselines regardless of their confidence threshold settings, we conducted an additional set of experiments. Figure 5 presents our additional experiments. We ran each baseline in four additional configurations, with the confidence score threshold set to different values. The chosen threshold values were set to 0.3, 0.4, 0.6, and 0.7 (0.5 is the original value presented in Figure 4). Our results clearly show that SPIREL outperforms all baselines, regardless of their chosen configurations.
