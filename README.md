# DWT-SVD
The code is developed using MATLAB R2013a. save these filesa as m files in matlab and then simulate and record sound used as input.

# Abstract
This code investigates the development of digital audio watermarking in addressing issues such as copyright protection. Over the past two decades, many digital watermarking algorithms have been developed, each with its own advantages and disadvantages. The main aim of this thesis was to develop a new watermarking algorithm within an existing discrete wavelet Transform (DWT) and singular value decomposition (SVD) framework. This resulted in the development of a combination of DWT-SVD-BFO (bacterial foraging optimisation) watermarking algorithm. In this new implementation, the embedding depth was generated dynamically thereby rendering it more difficult for an attacker to remove, and watermark information was embedded by manipulation of the spectral components in the spatial domain thereby reducing any audible distortion. Further improvements were attained when the embedding criteria was based on bin location comparison instead of magnitude, thereby rendering it more robust against those attacks that interfere with the spectral magnitudes. The further aim of this thesis is to analyze the algorithm from a different perspective. 

Improvements were investigated using DWT-SVD and DWT-SVD-BFO algorithms. A comparison of these two algorithms for different watermark images on two types of audio input signal is presented here. The whole thesis work is divided into five main chapters with 4th 5th chapter describing proposed algorithm and results with discussions.

# Results

![watermarked audio signal](https://user-images.githubusercontent.com/11607018/39228564-6457e942-487c-11e8-96d6-a0804214e408.png)

![embedding message in audio signal](https://user-images.githubusercontent.com/11607018/39228565-648f60f2-487c-11e8-8fe5-14bf324cf1ce.png)

![evaluation of audio watermarking](https://user-images.githubusercontent.com/11607018/39228566-64c56d46-487c-11e8-99c6-d7dfdc4a876f.png)
