---
title: 2\. Analog 신호와 Digital 신호, 그리고 Ground
categories:
    - Embedded Recipes
tags:
    - Analog Signals
    - Digital Signals
    - Ground
---
## Analog 신호와 Digital 신호의 관계  
Digital 신호는 Analog 신호의 일종이며, "대부분" DC 성분으로 이루어진 "있다/없다"의 Boolean Logic값이다.  

Analog 신호는 보통 AC 와 DC (교류와 직류) 성분으로 이루어져 있다. AC 는 주파수를 가지기만 하면 AC라고 부르고, 극성이 바뀌지 않고 steady 한 상태의 신호를 DC 라고 부르는데, 신호와 주파수의 영역에서 보았듯이, 모든 신호는 여러 개의 주파수 성분으로 이루어져 있다.  

![보통의 AC+DC 신호]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/analog-digital-and-ground-01.jpg)
{: .full}  

* * *
## Digital 신호  
Digital 신호는 High/Low 두 개의 Logic value만을 가질 수 있으며, 그 크기(Level)는 정하기 나름이다(3.3V, 5V 등).  

Digital 신호는 한계 값 또는 임계 값(Threshold)라는 특정 값 이상이면 High, 그 값 이하이면 Low로 판단한다.  
예를 들어, 1.5V가 Threshold라면, 1.5V가 넘는 값들은 Logic1(High), 넘지 않는 값들은 Logic0(Low)로 분류 될 수 있다면 이는 바로 Digital 신호이다.  

![Digital 신호]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/analog-digital-and-ground-02.jpg)
{: .full}  

하지만 Ideal Digital 신호는 없다.  
대부분의 신호는 Bounce하면서 변하게 되는데 이런 Transition에 관련하여, 이런 요동이 얼마나 크냐에 따라 시스템에 영향을 줄 것이냐 아니냐를 판가름하기도 한다.  

![Bouncing이 있는 Digital 신호]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/analog-digital-and-ground-03.jpg)
{: .full}  

이런 현상은 전원 line (Power)에서도 자주 볼 수 있는데, System의 어떤 chip이 동작을 시작하는 시점에서 갑자기 전류를 더 끌어다 쓸 수 있어, Bounce되는 것처럼 보이기도 한다.  
최초로 Bounce되는 시점에서 원하는 전압이나 전류보다 더 작은 양이 흐르기도 한다. 이런 경우에서는 회로는 전력문제에 직면할 수도 있다. 최악의 경우, System이 멈출 수도 있다.  
게다가 이런 Bouncing이 있으면, Digital 신호의 Level 인식 문제가 발생 할 수도 있다(0인데 1로, 1인데 0으로).  

* * *
## Ground(GND)  
Ground(GND)는 모든 전기, 전자 회로에서 다른 모든 전위에 대하여 기준이 되는 0V를 말하며, 일반적으로 전기의 -(마이너스)극을 의미하기도 한다. GND는 system내부에서 모든 current가 모이는 곳이다.  

Ground가 중요한 이유는 Digital System에서 1과 0을 제대로 구분하는 기준점이 되기 때문이다.

GND의 symbol은 ![ground]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/analog-digital-and-ground-04.jpg)로 표시한다. 이 symbol에 연결 되어 있는 회로상의 모든 pointsms 0V로 같다는 것을 의미한다.  
Ground는 Earth와 Signal Ground로 나뉘게 된다.  
Earth는 말 그대로 지면을 의미한다. Earth는 실제 전위 0V를 의미하지는 않으나, 저항이 크지않아, 웬만한 전류를 빨아들이게 된다.  
따라서 큰 전지기기의 GND는 직접 땅에 연결한다.  
Signal Ground는 Hardware 측면에서 어떤 전자기기의 GND를 의미하게 된다. 이는 system 내부의 모든 전위에 대해서 기준이 되는 점을 말한다. 보통은 전지의 -(마이너스)극을 저항이 적은 넓은 모양의 case나 PCB기판의 뒷면 등에 연결하여 전류가 몰려들 수 있는 환경을 만들어 놓은 후, 전위 기준으로 사용한다.  

* * *
### 왜 Digital 신호를 사용하는가?  
송신 쪽과 수신 쪽 사이에 있는 매개체는 왜곡 (distortion), 잡음 (Noise)등을 실어서 송신 신호에 덧붙여서 수신을 쉽지 않게 만든다. Analog 신호 자체가 information이라고 한다면 error가 날 것은 뻔할 것이고, 다시 바로 잡기도 힘들다. 하지만 모든 정보를 Digital화 해서 받는 쪽에서 Logic 1, Logic 0만 제대로 구분해 내면, error가 나도 FEC(forward error correction)나, CRC등을 이용해서 복구 하기 용이하기 때문에 조금 더 reliable하다. 또한, 깨끗한 디지털 신호로 reproduce할 수 있다는 장점이 있다.  
Voice 신호를 예를 들면, 진짜 analog 신호를 Digital화 해서 만든 것이다. 원래 voice를 완벽하게 다시 복구하는 것은 어렵지만, 수신자가 이해할 수 있게 끔 decoding이 가능하다.  
CDMA는 이런 Digital의 장점 뿐 아니라, Digital화를 한 후, channel을 Code로 Multiplexing하여, 여러사람이 동시에 나눠 쓸 수 있다는 장점도 있다.  

### Bouncing하는 신호는 어떻게 해결하는가?  
전원에서 Bouncing되는 부분은 상당히 회로적으로 불안하다. 이런 의미에서 C (Capacitor)를 한쪽은 Power 선에, 다른 한쪽은 GND에 달아 (다른 말로는 병렬로 달아) Capacitor를 마치 건전지 처럼 사용하여, Power line의 전압, 전류가 순간적으로 낮아질 때 Capacitor가 저장하고 있던 전기 에너지를 다시 방출하여 Power line의 전압을 원래대로 유지하는 용도로 문제를 해결하기도 한다. 이런 Capacitor를 Decoupling condenser 또는 Bypass condenser라고 부르며, 보통 전원선의 주변에 병렬로 길게 깔아 놓기도 한다.  

### AGND & DGND?
AGND 는 Analog Ground, DGND 는 Digital Ground이다. Analog 신호는 Analog 신호들의 GND, Digital 신호는 Digital 신호들의 GND에 모아둔다. Analog랑 Digital은 서로 성질이 틀려 같이 맞물려 놓으면 서로의 신호에 영향을 준다. 전위는 같게 해야하니까 0옴 저항 등으로 연결하는 방법을 사용한다. 

<sub>
출처: EMBEDDED RECIPES(corner book),  
친절한 임베디드 시스템 개발자 되기 강좌 - Analog 신호와 Digital 신호, 그리고 Ground [링크](http://recipes.egloos.com/4968642) 
</sub>
