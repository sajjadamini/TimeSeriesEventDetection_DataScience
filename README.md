# TimeSeriesEventDetection_DataScience
This script analyzes a timestamped power consumption signal for an electrical device to detect active usage start/stop times.


Here are the steps taken to detect the start/stop time of active usages:

1- Denoising the raw signal: A butterworth lowpass filter is designed and the raw signal is filtered out to eliminate the high-frequency noises.

Challenges: cutoff frequency has to be selected carefully in order to keep important information of the signal specially signal edges which also consists of high-frequency components.

2- Finding trend of the signal: This step is done for detecting the edges.

Challenges: 1- Size of first derivative of the signal is decreased by 1 that    must be correctly compensated for finding the corresponding timestamp. 
2- To completely denoise the signal remained from the first step due to limitation on cutoff frequency, signal smoothness must be done by specifying a proper threshold value.

3- To indicate the potential usage periods, non-zero values of the first derivative of the signal get 1 and zero values get 0 as an on/off signal.

   Challenges: There are many false detections that must be still eliminated.

4- Matched filter method is used in detecting the true usuage periods and removing false detections. A typical usage pattern is defind and convolved with the potential usage period signal to detect the true usage periods. Sign function is applied to show the result as an on/off signal.

   Challenges: 1- Defining the kernel for matched filter, i.e., typical usage pattern, is always tricky and has to be done carefully by studying the typical duration of true active usage periods. 

5- Finally, derivative of the usage on/off signal is taken to indicate start/stop time as a separate signal.

Challenges: 1- Size of first derivative of the signal is decreased by 1 that    must be correctly compensated for finding the corresponding timestamp.
2-Please note that always the first couple of samples due to filtering and taking derivatives are not reliable that must be eliminated from the final results.
