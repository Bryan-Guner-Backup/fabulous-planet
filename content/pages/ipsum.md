---
title: Ipsum dolor sit amet
subtitle: Aliquam lobortis faucibus blandit
seo:
  title: Ipsum dolor sit amet
  description: Aliquam lobortis faucibus blandit
  extra:
    - name: 'og:type'
      value: website
      keyName: property
    - name: 'og:title'
      value: Ipsum dolor sit amet
      keyName: property
    - name: 'og:description'
      value: Aliquam lobortis faucibus blandit
      keyName: property
    - name: 'twitter:card'
      value: summary
    - name: 'twitter:title'
      value: Ipsum dolor sit amet
    - name: 'twitter:description'
      value: Aliquam lobortis faucibus blandit
layout: page
---
Time series![](https://miro.medium.com/max/60/1\*LEMR7jO3KS9G-Hdz7VJd2A.png?q=20)![](https://miro.medium.com/max/756/1\*LEMR7jO3KS9G-Hdz7VJd2A.png)![](https://miro.medium.com/max/60/1\*ALzD4ieg-1UP5RB0VlYDCA.png?q=20)![](https://miro.medium.com/max/410/1\*ALzD4ieg-1UP5RB0VlYDCA.png)![](https://miro.medium.com/max/60/1\*3d9V2NHDEtwq8qcsbwjXFw.png?q=20)![](https://miro.medium.com/max/208/1\*3d9V2NHDEtwq8qcsbwjXFw.png)![](https://miro.medium.com/max/60/1\*Q8m8uj8xsYA0XJuUdInxJg.png?q=20)![](https://miro.medium.com/max/756/1\*Q8m8uj8xsYA0XJuUdInxJg.png)![](https://miro.medium.com/max/60/1\*U\_6R4Zub5C_NTPKSnt4w2Q.png?q=20)![](https://miro.medium.com/max/756/1\*U\_6R4Zub5C_NTPKSnt4w2Q.png)![](https://miro.medium.com/max/60/1\*As39Moa6jgeb-sS8PG2YeQ.png?q=20)![](https://miro.medium.com/max/756/1\*As39Moa6jgeb-sS8PG2YeQ.png)![](https://miro.medium.com/max/60/1\*bOLwVYKbJfM18cWwYI9aFA.png?q=20)![](https://miro.medium.com/max/756/1\*bOLwVYKbJfM18cWwYI9aFA.png)



Time series is a sequence of data captured at an equally-spaced period of time. While this type of data is nothing new in weather measurements, stock market and mobile data transmission, the exponential increase in the volume of data generated in recent years is driven by new technologies within the realm of Internet of Things (IoT) where data is continuously generated and recorded over time even during their idle state.

A quick look at a time series plot, for example, the representation of sound waves from a music clip may be very hard to interpret since the underlying pattern behind the jagged peaks and troughs are very cannot be easily detected in its raw form.

## Decomposing time series

Using a simpler example below, we can decompose the underlying components of a time series using Statsmodel using its seasonal_decompose function into its trend, seasonality and residual elements.

In order to build a model to forecast the raw time series, we approach this problem by breaking it into smaller tasks by dealing with each of its component above separately. A trend that appears to follow a linear relationship may be modelled using a linear or logistic regression model, and while residual is by definition should be a random element, there are techniques out there such as ARCH model that could help in its prediction.

For the seasonality component, if the underlying pattern behind it is still unclear as in the case above, we can approach the problem using Fourier transformation.

## Back to basics — sine function

Before we dive further into Fourier transformation, let’s first go back to basics and define a sine function:

Amplitude (A) is the maximum height of the sine function from its zero base.

Frequency (f) is the number of complete cycles in a set period. When working in Hertz (Hz), frequency is defined as the number of complete cycles within 1 second. In the example above, the green function completes 2 cycles in a second and thus has a frequency of 2 Hz. The angular frequency (ω) is simply a notation to represent 2π×f.

Phi (φ) is its phase or time shift. It is defined as the proportion of a complete cycle that has passed at time zero, measured in radians. For the purpose of this blog, we will simplify the examples below by setting the phase to zero.

While the amplitude and frequency of a simple sine function can be deduced visually, it gets tricky when more complicated cases are presented, as in the case in the example at the beginning of this post.

## Fourier transform

Fourier transform (FT) decomposes a time-domain function into the frequency domain. Simply put, an audio wave in the time domain is decomposed into its constituent frequencies and volume (amplitude). Mathematically, FT involves taking the integral of a complex number notation (note the letter *i*) which we will not be covered here.

The code below defines as a sine function of amplitude 1 and frequency 10 Hz. We then use Scipy function *fftpack.fft* to perform Fourier transform on it and plot the corresponding result. Numpy also has a similar *np.fft* function, but Scipy is preferred as it has other additional FT functions that we can use.

In the second plot, we can clearly observe a peak value at 10 Hz with a magnitude of one while all other frequencies hover around zero. We can verify this from the original signal where there are 10 complete cycles in a second with an amplitude of one.

When a similar principle is applied to a more complicated time series as shown in the green plot below, we can deduce from its Fourier transform that the data comprises of 3 different elementary components with 3 different frequencies (2, 5 and 10 Hz) at 3 different amplitudes (0.5, 1 and 2).

To convert the frequency-domain data back to time-domain original data, simply use the inverse FTfunction *fftpack.ifft* in Scipy:

Now that we have the frequency and amplitude information on the three constituent parts of the time series, we can define their corresponding sine functions and visualize them separately.
