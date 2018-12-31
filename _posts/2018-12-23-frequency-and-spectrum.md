---
title: 1\. lo신호와 주파수 영역 - spectrum analysis
categories:
    - Embedded Recipes
tags:
    - Frequency
    - Spectrum
    - Fourier Transform
---
## 주파수
주파수란 진동운동에서 단위 시간당 같은 것이 일어난 횟수이다.  

예를 들어 \\[cos(2\pi t)\\]라는 주기함수는 1초의 1번의 주기가 있는 함수를 말한다.  

이 함수는 일반화된 \\(cos(2\pi ft)\\)라는 함수에 주파수 \\(f=1Hz\\)을 넣고 만든 함수이다.  
\\(cos\\)이라는 함수는 주파수만 알면 한 줄로 표현해낼 수 있는 편리한 함수이다.

\\(f = 20kHz\\)일 때를 예를 들어 볼 때,  

![시간축과 주파수축]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/spectrum-analysis-01.jpg)
{: .full}  

\\(cos(2\pi(20kHz)t)\\)는 주파수 영역에서 \\(20kHz\\) 하나만의 성분을 가진다.  

보통 \\(cos\\)와 같이 주기를 갖는 신호를 **AC**라 하고, 주파수를 가지지 않는,  
계속해서 같은 크기의 레벨을 가지는 신호를 **DC**라고 부른다.  

결국 주파수가 \\(0Hz\\)인 신호를 DC라고 할 수 있다.  

![DC신호의 시간축과 주파수축]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/spectrum-analysis-02.jpg)
{: .full}

* * *
## Fourier Transform
모든 신호는 무한개의 \\(cos\\)또는 \\(sin\\)의 합으로 나타낼 수 있다.  

Fourier Transform를 하면 시간 축의 신호를 주파수 별로 분리해 준다.  

    어떤 신호 = 어떤 주기의 주파수 성분 + 또 어떤 주기의 주파수 성분 + 
              또 다른 어떤 주기의 주파수 성분 ...

이런 식이고, 어떤 신호를 이루기 위해서는 각각의 어떤 주기의 주파수 성분이 공헌하는 바들이 틀린데,  
그 공헌하는 바들이 각각 크기(Amplitude)로 나타난다.  

공헌하는 바를 어떤 주파수의 크기라고 할 때,  
    
    어떤 신호 = 어떤 주기의 주파수의 크기 * 어떤 주기의 주파수 +  
              또 어떤 주기의 주파수의 크기 * 또 어떤 주기의 주파수 + ...
    
이런식으로 표현이 가능하다.  

예를 들어 \\(Rect(t)\\) 는 무한히 많은 \\(cos\\) 함수의 합으로 풀어헤칠 수 있다는 것이 **Fourier Transform**이다.  

![Rectangular 함수의 Fourier Transform]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/spectrum-analysis-03.jpg)
{: .full}  

위 Rectangular 함수는 Amplitude가 1이고, Width(길이)는 \\(-\frac{\tau}{2}\\) 에서 부터 \\(\frac{\tau}{2}\\) 까지 즉 \\(\tau\\) 의 Width를 가지는 사각형 모양의 함수를 말한다.  

보통 Embedded system에서의 디지털 신호는 이런 Rectangular 신호로 이루어져 있다.  

Rectangular 신호를 주파수 영역에서 보면, 주파수가 0인 부분, 즉 DC 성분이 가장 큰 portion을 차지하고,  
그 크기는 Rectangular 신호의 시간 영역에서 넓이와 같다.  

Rectangular 신호의 주파수 영역에서의 모양은 **sinc function**이라고 부르는 함수의 모양으로 Transfrom이 가능하다.  

Rectangular 함수는 주파수 영역의 DC 성분의 크기가 가장 크면서 \\(\frac{1}{\tau}Hz\\) 마다 \\(\frac{1}{\tau}\\) 의 Harmonics의 주파수 성분은 0으로서 그 크기가 없고,  
나머지는 양쪽 축으로 무한히 퍼진 주파수 성분이 있음을 알 수 있다.  

쉬운 예로 \\(\tau=1\\) 인 예를 들면, \\(\frac{1}{\tau}=1\\) 이므로, 1, 2, 3, 4, 5 ... Hz에서는 주파수 성분이 없고, Rectangular 신호의 면적은 1이므로, DC 성분의 크기는 1이다.  

![Rectangular 함수의 Fourier Transform]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/spectrum-analysis-04.jpg)
{: .full}  

그래프를 보는 방법은 \\(f\\) 축은 \\(Rect(t)\\)를 FT하면 나오는 주파수 성분들을 나타낸다.  

\\(sinc(f)\\) 의 \\(f=1.0\\)에서의 값은 그래프에서 cos의 \\(1Hz\\) 성분을 의미한다.  

그 것은 ![cosine 그래프]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/spectrum-analysis-05.jpg) 성분이 없다는 것을 말한다.  

위 그림은 Rectangular 함수가 시간 축에서 어떤 \\(cos\\) 함수들이 어떤 크기로 합해 져야 되는지 표현되어 있고,  
주파수 축에서는 어떤 주파수들의 성분들이 주파수 영역에 있는지를 보여주고 있다.  

\\(F(f)\\)에서 F는 Fourier Transform, f는 주파수를 의미한다.  

> 결국, 이 세상의 모든 신호는 \\(cos\\)와 \\(sin\\)의 합으로 나타낼 수 있고,  
디지털 신호로 사용하는 rectangular 신호는 DC 에 가까운 완전 저주파 신호와,  
약간의 중주파(이 포스팅에서만 중주파라는 표현을 사용합니다) AC 신호들의 합과,  
완전 필요없는 전 대역에 걸쳐있는 자잘한 고주파 신호로 구성되었다는 것을 알 수 있다.  

Spectrum Analyzer로 어떤 신호를 들여다 보면 그 신호가 어떤 주파수들로 이루어졌는지를 눈으로 확인 할 수 있다.  
![spectrum Analyzer 로 본 어떤 신호]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/spectrum-analysis-06.jpg)
{: .full}  

* * *
### 주파수 영역에서 마이너스 크기의 주파수를 가지는 이유?
Fourier Transfrom은 \\(e^{jwt}\\) 라는 basis function의 합으로 나타내는데, 
이 함수가 complex 라서 \\(Xcos + jYsin\\)로 나타내게 된다.  
Euler공식에 의해 phase가 여기에 따라붙어 마이너스처럼 보이지만,  
실제 크기를 따질 때는, sinc function에 절대값을 제곱하여 Power Spectral Density를 구하여  
모두 +인 실제 Power로 크기를 따지면 된다.

<sub>
출처: EMBEDDED RECIPES(corner book),  
친절한 임베디드 시스템 개발자 되기 강좌 - 신호와 주파수 영역 [링크](http://recipes.egloos.com/4968600) 
</sub>
