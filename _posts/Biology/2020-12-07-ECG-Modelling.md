---
layout: post
title: Basic ECG Modelling with Trigonometry
date:   2020-12-07
published: true
categories: biology
---

<iframe style='width:100%; height:500px;' src='https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9cc242a0-13a1-446d-b945-f83f74fd35a8/Final_IA_Report_Draft.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20201208%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20201208T013140Z&X-Amz-Expires=86400&X-Amz-Signature=04d1fdff6396997301aa5af171857876eb68a2d363c7263aa0813c1ec2453c19&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Final_IA_Report_Draft.pdf%22'></iframe>


Electricity is one of the most commonly used forms of energy. Not only generating power for daily appliances and technology, it is also an important element to maintaining life in the body. Notably, electricity is involved in the beating of the heart — an essential organ that pumps blood and delivers oxygen to other parts of the body. It contracts in response to the electrical depolarization of muscle cells and is stimulated by electrical nodes. An electrocardiogram (ECG) is an instrument that records the magnitude and time of electrical activity in the heart. The information is recorded on a graph that presents electrical signals at various locations of the heart, generated by electrodes placed on the surface of the body (Price, 2012). 

My grandpa has been undergoing chemotherapy which has had many harmful effects on his health. After seeing his ECG taken at the hospital, I was inspired to investigate how I can use mathematics to assess the health of his heart. Knowing that an ECG is a periodic signal, I am curious how I can apply math to model one and what algorithms are present in the real world that uses math for analysis. I want to use insight gathered from this exploration not only to learn about my grandfather’s health but to also see how realistic math models are in cardiology. 

## Research

To begin, understanding the anatomy of the heart in relation to ECG signals is essential for model development and pattern recognition. ECGs are recorded using 12 different lead directions, with limb leads (I, II, III, AVR, AVL and AVF) and chest leads (V1, V2, V3, V4, V5 and V6) (Price, 2012). For the sake of this investigation, V4 chest leads will be used across all models to allow for simplicity and consistency. This choice is because V4 leads typically exhibit a waveform similar to what is considered a “standard” ECG wave (Queens, n.d.), as in Figure 1. Also, comparing two different leads will be a major source of error as leads record signals from different directions and such comparison would cause incorrect interpretation.  

Figure 1 demonstrates the general waveform of an ECG signal. There are 5 deflections, called waves, that are either positive or negative and indicate a specific electrical event. (Healio, 2020) My approach was to first obtain an ECG of a normal healthy patient. After modelling the ECG, I could use the same method for my grandpa’s ECG. This choice is justified as the models can then be compared to identify similarities and differences.
Planning

When deciding on a general model that would be fitting for the waveform, I considered some properties that are important. The problem I faced was deciding on how to model the seemingly arbitrary curves as it does not fit with the form of any general function. 

Initially, I wanted to create a piecewise function composed of polynomials, however, I reflected on what limitations this might have. Primarily, it would be difficult to make a piecewise function periodic as they are generally non-periodic with a restricted domain. In contrast, an essential property of an ECG model is that it can present the patient’s heart rate by observing the periodicity of the waves.  

In the end, I decided that a sinusoidal function is appropriate for this model because not only is it periodic but also contains amplitudes similar to the 5 ECG waves. By using substitution, it can also reflect the electrical levels of the heart at each point in time, just like an ECG. The problem is that I need to figure out how a function can be created that reflects the different waves at the same time. Transformations for  will not obtain waves of varying amplitudes and slopes. I began by investigating the sum of a series of sinusoidal functions. 

I plotted  in red and  in blue, seen in Figure 2. The function of their sum  is in black. I realized that at any given point at X, the output is the sum of the y-values for  and . This would mean that in order to successfully model multiple waves, 5 different sine functions are required and then added. As seen in Figure 3, the individual functions also need a “peak” where the event occurs, and have a “baseline” where there is no event happening. In other words, it would be where  until it cycles again and another event occurs. This “baseline” is essential for another reason — to prevent multiple peaks from adding together, as in figure 2. This would cause disruptions due to altitude overlaps. This is problematic as if this was done through computing analysis, it would make it difficult to extract the end function into its constituent waves (reverse analysis) and decrease the accuracy greatly. 

A function of this form, with a “peak” and a flat “baseline” is not commonly seen. To start, I attempted to recreate the P peak of the ECG waveform. To do so, I compared the components of a standard sinusoidal function with the form I wanted. A standard trigonometric function has the form:


Where each variable represents a specific property of the function:

  is the amplitude
  is the period, or in other words, the span of each cycle
 is the horizontal translation
 is the vertical translation

However, these basic transformations still resulted in a repeating oscillation of a sine wave without a flat section in the function. I realized that adding exponents to the sine function introduced this property. I started with  and attempted to observe the set of sinusoidal functions which take the form  and what occurs when . This is incredibly interesting as it is not a function that is commonly investigated nor studied in class. Certainly, the application of this form of trigonometric functions is useful in ECG modelling but may be also helpful in other fields of signal processing.
I began this investigation by constructing a table of values and trying to identify a trend across the set of functions by substituting in values of x where . This segment shows how the first part of the original  will be altered with the addition of exponent .

Table 1. Output of functions with incrementing exponents derived from parent function f(x)=sin x.


There are some trends to note after analyzing Table 1. To start, across all the function variations, the output for where  always results in  respectively. However, there are changes between values of  and  which demonstrates a fascinating trend. For all the functions, as , all values within this range decrease exponentially and the shape of the curve becomes more exaggerated. It begins by growing at a small rate of change with a sharp increase towards the end. However, all points where  converge results in a value of . This behaviour is evident when graphed in figure 4. As a property, it can be seen that the “a” value is an indicator of how steep or exaggerated the curve should be.
I also realized a possible limitation to my table of values. A property that was not displayed was how the parity of the function affected how the curves for the function behaves across periods. This was not accounted for because this difference is only seen in values that extended beyond the range used for Table 1. Consider  and , for example. For function , the output of  whether it is positive or negative will always result in a positive output after being squared. This does not hold true for  as a negative number cubed will result in a negative number. To view this idea more clearly,  and  was graphed in figure 5.
This property creates restrictions for the “a” value when modelling each peak of the ECG. As an odd function will result in alternating positive and negative deflections seen in figure 5, it does not allow for a consistent peak and altitude. Because heartbeats have a similar altitude for each cycling peak, it would not be realistic to model it as an odd function. An even function will ensure consistency as the peaks are all positive deflections. Therefore, when selecting the “a” value, we would restrict “a” to be an even number.

ECGs of healthy individuals were obtained from a variety of sources and the V4 sections from two of the sources are displayed in figure 6 (D. Jenkins & S. Gerred, 2017). I decided to find multiple as I wanted to make sure my model is reliable and demonstrated similar properties throughout all ECGs of healthy individuals. Some notable observations about V4 leads are that the R wave has the highest altitude out of all the waves, the P and Q waves are small deflections that are barely visible, and that the T wave is the widest in shape out of the rest. 

Before going further, I realized it was essential to establish the scale to which time (x-axis) and electricity (y-axis) are measured in the ECG in relation to the coordinate grid. A standard ECG grid is distributed into small squares are large squares. A large square is composed of 5x5 small squares and each large square represents a time of 0.2 seconds. The height of one large square corresponds to 2 millivolts of electricity (Price, 2012). I decided for one unit of my graph to correspond to one large square in an ECG graph. This allows for more simple calculations, and the total time or electrical energy will be converted back from units to time or millivolts afterwards.

## Sinusoidal of a Single Curve

I first constructed the P wave through a series of transformations. The real ECG was overlaid on top of the function. First, it is crucial to calculate the period of the function, which is the b value. In the ECG, the period is around 5 large squares between peaks of the R wave. Therefore, the corresponding period for the function will be 5 units. The following formula gives us the period:

Substituting the desired value of 5 gives:


I was faced with a problem where this value yielded two times the number of P waves then intended. It was strange as when  was graphed it produced a period of 5. Upon reflection, I realized  was an odd function, where the negative deflection in the sine wave was unaccounted for in my desired model. This is seen clearly when graphed in figure 7. To solve this problem, I divided the b value by 2, which yields , and this b value will produce each wave of the ECG at a period of 5 units apart.  Next, I determined the horizontal shift. I know that the peak of the sinusoidal will be at the midpoint of 0 and , which is . Therefore, the placement of the vertex for the P wave will match this value. Shifting the  left 1.3 units results in a matched vertex with the P wave seen in figure 8. Currently, the sinusoidal function is:




It is important to note that there should be no vertical translation in any of the functions. This is to ensure that all “baselines” for each wave are at a value of 0. The next step is determining the amplitude of the wave. This is done by obtaining the vertex of the P wave and determining the y-value for that point. A value of 0.15 was obtained for the amplitude. Figure 9 displays the alignment of  with the amplitude of the P wave in the ECG.


Finally, the “slope” of the model will be aligned with the curve by changing the exponential variable. Through trial, the value of 76 was obtained and the result of the final model for the P wave is seen in figure 10.


After combining the different variables into one, the final function of the P curve is obtained:


The other 4 curves (Q, R, S, T) were obtained using the same method and their respective functions and graphs are displayed in figure 11.

When each segment is added together into one general function, the graph in figure 12 is obtained. Represented by . It can also be seen the benefit of using a sinusoidal rather than a polynomial — the sectors connect fluidly and the ECG wave flows naturally.




After obtaining a model of a normal ECG, I will use the same method to determine my grandfather’s ECG and perform analysis. Although the same process was used as before, there was an additional component in the final function as there was were abnormalities in the shape of the T wave.  More specifically, it is called the ST segment, the joint section where the S wave meets the T wave. Two bumps are present instead of one wave, therefore the addition of two different sinusoidal functions was needed to model the T wave. 


The general function of the combined T wave is shown in figure 14. The curve starts with a flat increase but is intercepted with a sharp increase. It is modelled with the function:



The final result of the function is graphed in figure 15 and the equation is:



Another benefit of this model is that I can break down the function into its different waves and then compare my grandpa’s ECG to the normal ECG graph. I first conducted a comparison of wave amplitude which is the coefficient (variable a) for each sinusoidal function. The comparisons are presented in table 2. This comparison is valid because the scale I used for both models is identical, where each square in the ECG representing 1 unit. In terms of time, one unit represents 0.2 seconds.

Table 2. Comparisons between wave amplitudes of normal ECG and my grandpa’s ECG.


From table 2, it can be deduced that there is a significant change in the R wave amplitude. Also seen in figure 15, the R wave does not spike past the T wave. The table shows that both the R wave and T wave have the same amplitude. This may suggest abnormalities in these corresponding areas of the heart. The R wave indicates the changing direction of an electrical stimulus as it passes through the main ventricular walls (University of Nottingham, n.d.). The structure is quite thick and requires a surplus of energy which suggests why the R wave is one of the biggest waves generated during conduction. However, a small wave in my grandpa’s ECG model may suggest that his ventricular walls are not as thick. Another abnormality mentioned earlier was the shape of the T wave in the ECG. Normal T waves have a single curve, but in this there are two which add to become a large deformed wave. In the table, it also shows how the T wave is greater in amplitude, but not drastically. 

Although this is a basic analysis, it may present indications about the nature of my grandpa’s heart. I may want to tell him to ask the doctor about these abnormalities in the ECG. I am actually quite proud of creating such a model and being able to analyze my grandpa’s ECG model to this degree of specificity. However, after analysis, I began to consider how realistic this model is and the assumptions made throughout my investigation. 

Considerations and Model Application

My model using sinusoidal functions is advantageous in two situations. The first being if a patient may want to see the general shape of their heartbeat and also its mathematical equation. Like the comparison in table 2, it may present some basic information about how the model deviates from a standard ECG. Second, the model is great for the approximation of an event and electrical level given any value of time. As it is a function, substituting any large time value would output an approximation for the patient's electrical activity at that point in time. This is useful in a variety of ways, especially in time constricted decision-making and predicting certain electrical levels. It would be incredibly difficult to predict electrical levels by directly looking at a patient’s ECG, and this function would provide this data in a timely, and relatively accurate manner. 

However, this model is indeed basic and only a mathematical approximation for a signal that may not be perfectly constant in real life. The major assumption made in my investigation was that the patient’s heart rate remained the same and that all waves were reproduced at the same altitudes each repeating cycle. This is largely incorrect for many reasons. A patient’s heart rate is never constant as there are always biological factors that affect heart rate in small amounts. Even if there is variation in a period by a millisecond, in rigorous data analysis, this must be accounted for. This is where a periodic model is only useful for making comparisons but not to use as instruments for health predictions and pathogen identification. Additionally, waves always fluctuate and amplitudes do not stay constant. It is impossible for the heart to generate the exact same amount of electricity to pump and contract each cycle.

Finally, as my model is an approximation, there are limitations that affect its accuracy. I believe it is essential to acknowledge these as they may affect data and the results in a variety of ways. The most prominent source of error for my model is the segments where different waves connect. Although adding different sinusoidal functions allow for the segments to flow better than a polynomial piecewise function, these joint segments are far less precise from the actual ECG in comparison to the precision of a specific wave and peak. 

After evaluating this model, I can conclude that it is good for basic analysis and learning about the characteristics of a patient’s ECG but is not accurate enough to use in real life and analytical applications. However, the concept behind the creation of my model and the use of sinusoidal functions are actually a fundamental part of real life algorithms used to analyze ECGs.

A major problem I had when analyzing my grandpa’s ECG was that there were many random bumps and waves that were not consistent with what was a typical waveform. After research, I learned these arbitrary waves and fluctuations were known as “noise”. Noise is caused by certain external and internal factors during the recording of the heart, and because electrodes are placed on the surface of the body, it is inevitable that hints of other signals are also picked up by the electrodes, which may interfere with the true ECG wave (Haque et al, 2009). 

Therefore, another problem with my mathematical model was the ambiguity of results surrounding my grandpa’s T wave. Was the wave abnormal due to some problem in the heart, or was that noise caused by an external factor? This ambiguity in real life analysis should not occur as in clinical applications it would have implications on the possible health and life of a patient. Therefore, I believe that further techniques or more complex algorithms are needed for in depth analysis about diagnosing certain coronary diseases. This model only fulfills the purpose in being able to direct use for heart rate estimations as well as give a general mathematical shape of the ECG waveform. 

A technique that I looked into when trying to find an appropriate model was the Fourier series. The idea behind the Fourier series is that it breaks down a complex function into its trigonometric constituents using an infinite sum series of sine and cosines. This is useful as the larger the number of terms in the series get, the more accurate the approximation of the function becomes. However, the reason why I didn’t use the series for this investigation was that I wasn’t able to find a way to connect the complex approximations (in segments of waves) together as a whole signal. However, after further research, this idea of using a finite domain with infinite terms to model an approximation for a function is actually used in analytical computing to create a complex algorithm called the Fast Fourier Transform (FFT). This is one of the most commonly used algorithms in the medical industry for creating ECG analysis software and a method of coronary disease recognition through ECG input (B. V. P Prasad & V. Parthasarathy, 2018). An extension and next step for my investigation would be to dive deeper into this area of using a Fourier series as a model, learn more about the FFT, and the mathematical concepts behind its design.

Through this exploration, I learned that although models for certain signals can be mathematically deduced, the extent to which these models are reliable and applicable in real life depends on the context as well as the possible limitations of the model. Each model has their benefits and it also depends on the circumstance. Also, some may be more accurate and useful than others. In general, I realized that functions and mathematical models always have possible sources of errors and that more accurate and efficient models can always be deduced. 

This investigation demonstrates not just the simple deduction of ECG analysis. It also suggests that repeated mathematical innovation is necessary to solve issues in the real world - especially in the field of biological signal analysis, where better models can be developed to help more people.





















Bibliography
Queens University. (n.d.). Analysis and Interpretation of the Electrocardiogram. Retrieved from
	https://elentra.healthsci.queensu.ca/assets/modules/ECG/index.html

Healio. (2020). Introduction to the ECG. ECG Basics. Retrieved from 
	https://www.healio.com/cardiology/learn-the-heart/ecg-review/ecg-interpretation-tutorial/	
	introduction-to-the-ecg

University of Nottingham. (n.d.). A Beginners Guide to Normal Heart Function, Sinus Rhythm & 	Common Cardiac Arrhythmias. Retrieved from
	https://www.nottingham.ac.uk/nursing/practice/resources/cardiology/function/r_wave.php

B. V. P Prasad & V. Parthasarathy. (2018). Detection and classification of cardiovascular 	
	abnormalities using FFT based multi-objective genetic algorithm, Biotechnology & 	
	Biotechnological Equipment, 32:1, 183-193, DOI: 10.1080/13102818.2017.1389303

Jenkins, D & Gerred, S. (2017). Normal adult 12 lead ECG. ECG Library. Retrieved from
	https://ecglibrary.com/norm.php

Price, D. (2012). How to read an Electrocardiogram (ECG). Part One: Basic principles of the 
	ECG. The normal ECG. South Sudan Medical Journal. Retrieved from
	http://www.southsudanmedicaljournal.com/archive/may-2010/how-to-read-an-	
	electrocardiogram-ecg.-part-one-basic-principles-of-the-ecg.-the-normal-ecg.html

Haque, A.K.M Fazlul & Ali, Hanif & Kiber, Md & Hasan, Md. Tanvir. (2009). Detection of 
	small variations of ECG features using wavelet. Journal of Engineering and Applied 
	Sciences. 4. Retrieved from
	https://www.researchgate.net/figure/Figure-2-Response-using-FFT-of-simulated-normal-
	a-and-noise-corrupted-b-ECG-signals_fig2_239927352