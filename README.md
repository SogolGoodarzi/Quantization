# Quantization
Assume the following signal:

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/9123dc4a-5954-4da6-93c3-ac3c92f51e3e)

<p align="justify"> The purpose of the question is to convert the above signal into a digital signal through uniform quantization and then, upon receiving it at the receiver, convert it again into an analog signal. For this purpose, we go through the following steps. </p>

### Sampling
<p align="justify"> 1) First, plot the above signal in MATLAB. The number of considered points should be between 15000 and 20000. (Given that there are many points, we consider this signal as the main analog signal implemented in MATLAB). </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/d0ecaa75-c882-41cc-bfe6-7257e89dd644)

2) Sample the considered analog signal with a frequency of 300Hz and plot the resulting discrete-time signal.

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/5d547012-67bf-4a62-a09f-0c5686322202)

### Applying quantization levels
<p align="justify"> As mentioned earlier, uniform quantization is used to pack signal data. In this step, we define the number of N levels and depict each point of the signal that is placed between the two levels on the cluster center of those two levels. The following figure represents this function. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/aba6c0db-e013-4b4c-a054-f71008b9e0fe)

<p align="justify"> 3) For this purpose, according to the uniformity of quantization, we define 32 levels with the same distance from each other in the range of the signal range and depict each of the points on the center of the two-level group. Bring the shape of the quantized signal in your report after implementing this approach. </p>

<p align="justify"> To quantize the sampled signal, we must first place levels with the same distance in the signal domain. For this purpose, we enter the maximum and minimum values ​​of the signal amplitude along with the desired number of levels (32 levels) into the linspace() command in MATLAB to form these quantization levels. Now, to quantize the samples, we first store the distance between two levels in a variable called delta. Using two loops, one of which scrolls over the discrete signal points and the other over individual levels, we first check which two levels the desired point is between according to the first condition written. In the next condition, we checked that if the distance of the desired point was less than half of the distance of both surfaces, that point would be imagined on its lower surface, and otherwise it would be imaged on the upper surface. By implementing this algorithm for the discrete signal of the previous section, we have the output of the quantized signal as follows: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/99c1aa94-6b43-4288-bb6b-01ce71c1a7db)

### Digitalizing the quantized signal
<p align="justify"> In this section, for each quantized point, according to the digital modulations, a pulse is supposed to be sent in the transmitter. The selection of the basic pulse is arbitrary and in this section we use the pulse of the following figure. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/7f956a91-d948-47b8-b4a7-971300fbbb2c)

<p align="justify"> For each point (which after a coding step, is interpreted as digit or symbol), the basic pulse in the above figure is multiplied in a certain range and sent from the transmitter to the receiver. (The digital modulation used in this exercise is PAM type). </p>

4) It is desirable to calculate the energy of the time-discrete signal obtained by sampling the signal with a frequency of 1000 Hz.

<p align="justify"> For this section, we first created a continuous rectangular pulse of 20000 points and then sampled it with a frequency of 1000Hz. The shape of the sampled pulse is as follows: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/d18df149-40d2-4608-888c-53f9cba6115d)

<p align="justify"> Now, to get the energy of the pulse, we import the p.mat file into the MATLAB environment and for this purpose, we calculate the sum of the squares of its points to obtain its energy. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/611553f1-6c9d-46d9-9b59-14667cbfe447)

<p align="justify"> 5) For each of the 32 quantization levels, assign a number from 0 to 31, which, as mentioned earlier, is known as a digit, and finally, store the signal value of each level with the corresponding digit in two-dimensional arrays (from this array for we will use signal recovery). One of the most common coding methods in digital telecommunications can be referred to as Graycode labeling; Code each of the symbols in this way and find the pulse corresponding to it from the existing folder. Finally, by placing these pulses next to each other in order, bring the form of the digital signal resulting from this modulation in your report. (Each of the pulses must be sent within 1 second). </p>

<p align="justify"> To implement this section, it is necessary to form the desired array first. As it is clear from the written program, we put decimal values ​​from -31 to 31 in the first column of the mentioned array with steps of 2. The second column has gray codes from 0 to 31. (Note that in this coding, both consecutive numbers differ by one bit, and this is the reason for using this method to code the levels.) In the third column of this array, the values ​​of each of the levels in the section " Applying the quantization levels" we have formed. </p>

<p align="justify"> Now, with appropriate commands, by scrolling over the quantized signal points in the previous parts, by obtaining the level where each point is located, we can also find the decimal equivalent of that level through the array we formed. Now, we multiply the value of this level (that is, the decimal code related to the level, which is between -31 and 31) in the pulse signal and store a string of these pulses with amplitudes corresponding to the amplitudes of the quantized signal in a matrix. We will have the form of the digital signal resulting from this modulation by plotting the previous matrix as follows: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/564b77fb-96bd-4290-925b-1232f46ffb4e)

### Receiving digital signal in reciever
<p align="justify"> At the receiver, the received signal will be accompanied by noise. Channel noise is considered Gaussian noise type and according to definition, it is a normal random process and SNR in the receiver is assumed equal to 2dB. </p>

6) Obtain the variables related to noise modeling and write a brief explanation for each variable.

<p align="justify"> For this part, we are supposed to add noise to the signal to simulate the real mode of sending and receiving a signal. For this purpose, it is necessary to have Gaussian noise along with the message signal in the receiver. The two parameters we need to form Gaussian noise are the mean value and the variance (because we have considered the noise as a random variable with Gaussian distribution). Now we find these two parameters. </p>

**Mean:**

<p align="justify"> The mean of this Gaussian distribution is zero. As explained in the lesson, therefore, the mean of a distribution we use to simulate noise is zero because the generated random values ​​are such that their weighted sum will eventually equal zero. </p>

**Variance:**

<p align="justify"> To calculate the variance of this distribution, we need to find the value of this parameter using the given SNR. According to the information we have from the previous section and using the appropriate relationships we will have: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/cb828e98-b846-45a0-8b65-94f4e634824b)

<p align="justify"> Now, having the value of SNR, we must first find the value of the signal power of the sent message to find the variance. For this purpose, according to the code we have written, we must calculate the average of the sum of the squares of the coded points with triangular pulses that we obtained in the previous section in order to obtain the power of the message signal ( $S_x$ ). According to the MATLAB instructions and the above relations, the amount of variance will be as follows: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/a64cff3f-15bf-4742-b00f-2ba4fa3dd3fd)

7) By adding noise with the mentioned characteristics to the transmitted signal, display the received signal in the receiver.

The output graph of adding noise will be as follows:

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/4878207f-0172-43b4-b78d-66a60df89bf4)

### Decoding the digital signal
<p align="justify"> From this point on, we go through the process of recovering the analog signal from the digital one. With the knowledge that each of the symbols is sent in 1 second, we implement a policy to convert the pulses into its corresponding symbols based on it. For this purpose, we must know that each of the pulses assigned to each digit is a multiple of the base pulse. </p>

<p align="justify"> 8) Multiply the base pulse by the pulse string received in the receiver, per second, and by calculating their mutual energy and considering the base pulse energy, find the amplitude of each of these pulses, and in this way, using the bit string. Specify the quantization level digit for each symbol sent. </p>
 
<p align="justify"> According to the requirement of the problem, first, every 1000 points, we advance 1000 points in the received signal in the receiver and multiply the basic pulse by it. (Please note that for this reason, we have considered 1000 points as 1 second because our basic pulse has 1000 points in one second, or in other words, as we saw from the first question of this section, we had sampled the pulse signal with a frequency of 1000.) In the figure below, the resulting signal By multiplying these pulses in the signal, you can see the received message. According to this operation and comparing the diagram below with the diagram of the previous section, we can see that a good amount of noise has been reduced by this work. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/8cb01135-df74-450a-8161-843500d45203)

<p align="justify"> Now, in order to get the reciprocal energy, i.e. the energy of the same signal multiplied by the base pulses, we act similarly to the previous cases and get the sum of the squares of each second of the signal (one second means 1000 samples, which can also be seen in the code that by writing a circle, we have scrolled on the signal and obtained the energy of each second). Now by comparing the energy of each second of this signal with the energy of the base pulse, we can find the amplitude of each of the sent pulses. This comparison is done by obtaining the ratio of the energy of each second of the signal to the energy of the base pulse. In the next step, to calculate the digit of the sent pulse string, we implement the algorithm to find the smallest distance from the quantization levels. That is, we get the difference between the values ​​calculated for the amplitude of each pulse with the values ​​of each quantization level in order to determine which of the sent pulses corresponded to which sample in which quantization level. We implement the algorithm and the resulting digits are as follows. (Please note that the resulting numbers are the digits that we put in the requested array in the form of decimal coding. That is, the same numerical string from -31 to 31 with a step of 2. The point is that we could have added the gray code digits at this stage. but for convenience, we have obtained the string of decimal codes). </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/8b2e71d9-4d72-4639-87cd-df20b1b36fd5)

<p align="justify"> 9) Using the two-dimensional array obtained in the "Digitization of the quantized signal" section, convert each digit to the actual value of the signal at the quantization level and plot the shape of the resulting signal. </p>

<p align="justify"> Using the digits obtained in the previous part, we get the level value corresponding to each digit through the appropriate commands with the array we made of the codes and values ​​of the levels, and new samples are retrieved in this way. Using these samples, we plot the recovered signal. In the figure below, in order to make a comparison between the original quantized signal and the recovered quantized signal, we have shown the graph recovered in this section and the graph formed in the previous sections at the same time. As it is clear, the two graphs are perfectly matched and the signal is correctly recovered. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/754fa9ef-feb9-480a-b2a5-2f075f06502d)

### Transforming the quantized signal to analog
<p align="justify"> 10) Design an algorithm based on which it is possible to detect key points that have common signal and quantization levels (intersection points). Explain your algorithm with a diagram. </p>

<p align="justify"> According to the mentioned guide, it is better to set the quantization to a low level for this section. For this purpose, we act according to the algorithm that we implemented for the quantization part of the previous parts, with the difference that when we find the two surfaces where the desired point is located, then we image this point on the lower surface. The shape of the quantized signal with this method is as follows: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/aac8fa54-6925-4567-9196-0c06b9e3915a)

<p align="justify"> First, we give a brief explanation about the process to be followed. By scrolling on the quantized signal to any point we reach, we must measure it based on its position relative to the points before and after it, whether to store it in the desired points or whether it will be deleted. So, the implemented algorithm is divided into four parts, which you can see in the overview of the program written in the code file. </p>

**Ascending zone of the signal:**

<p align="justify"> For the case where the current point is located in a place of the signal that is at a higher level than the previous point and is lower than the next point or is at the same level as it (that is, the signal is ascending), select that point we do. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/4737f67c-7d5b-43c3-8840-6bfc07c502d0)

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/73f1f604-e3ed-47ba-812d-f927d828af63)

**Falling area of ​​the signal:**

<p align="justify"> For this section, according to the previous section, it can be said that when the current point is greater than the next point and is smaller than or equal to the previous point, then this point will be selected. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/b53f297c-df0a-4441-af28-48552851df4b)

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/fc34e711-f688-4563-a41b-1ebb691f42e8)

**Maximum signal area:** 

<p align="justify"> We have only one condition for the maximum signal area, and that is when the current point is greater than its previous and next point and is not equal to them. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/3bc18879-5dc1-4d22-a6e9-fece11f250b5)

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/8e4f1c13-3a7a-4859-a463-46129ff1bae9)

**Minimum signal area:** 

We will have two modes for this section. One on the left and one on the right of the minimum signal point. 

* Left Side of Min Point:

<p align="justify"> Before reaching the minimum (that is, the left side of the signal minimum), if the current point is smaller than its previous point and is smaller than all the points before it (temp2) and all the points after it (temp1) (which is the condition of being a minimum) then this point should be saved. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/548b1f62-1269-4410-9155-f5501d3c93b6)

* Right Side of Min Point:

<p align="justify"> In this case, after crossing the minimum point, that is, where the current point is equal to the previous point and is smaller than the next point and is smaller than all the points before and after it (i.e. temp2 and temp1), then this point must also be saved. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/55cd3d91-b3df-482e-8595-f384f9b1137b)

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/b03a2851-99a3-428d-9689-76e6240b4345)

Finally, the general form of the output for which we have implemented the algorithm is as follows:

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/84c21cdb-29c7-40eb-aee5-cb70301cf9b9)

<p align="justify"> 11) Using the obtained points and using the MATLAB function, interpolate the spline points and reach a signal with the same number of points as the analog signal stored in MATLAB and plot both in one graph. </p>

<p align="justify"> Using the spline() function and the appropriate arguments we put for it, we can recover the analog signal. The first argument of this function should be the index of the points that we saved in the previous part, of course, a suitable scale based on the sampling frequency and continuous signal frequency should also be performed on it. The second argument is the points stored according to the algorithm of the previous part, and the third argument is the time of the continuous domain, which is needed to recover the analog signal in this domain. By implementing this function, the analog signal is recovered and the initial analog signal has been plotted together in the figure below. As it is clear, we see that there is a little difference between the original signal and the recovered signal, and we see most of this difference in the critical parts of the signal, i.e., its maximum and minimum points, which is expected because at these points, the quantization of the signal is such that a number of adjacent points are usually placed on the same level, and choosing the beginning and end points of these intervals for interpolation causes the middle points that were in other values ​​but are all placed on the same level (due to quantization) are not located in the array of stored points and therefore do not play a role in the interpolation process and we see an error in the recovered signal compared to the original signal. </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/3b4f3aef-768a-4a18-87b5-50e4a64d6662)

<p align="justify"> 12) We calculate the error value between the original analog signal and the recovered signal in the previous section with the immse() function, and the result is as follows: </p>

![image](https://github.com/SogolGoodarzi/Quantization/assets/125180530/40474038-9496-48d7-9df5-5aa966885bf3)

<p align="justify"> As it is clear from the figure and the calculated error, it can be said that with a relatively good approximation, the algorithm implemented in this section can be used to recover analog signals. </p>
