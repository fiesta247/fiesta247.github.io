---
title: 5\. Transistor 1%
categories:
    - Embedded Recipes
tags:
    - Transistor
toc: true 
toc_label: "Contents" 
toc_icon: "cog"
toc_sticky: true
---
## Transistor
Transistor는 Trans-Resistor이다. 간단한 회로이론에 의하여, Resistor값을 변화 시킬 수 있다는 의미다. Resistor의 용도는 전류의 양을 조절하는 것이다. Transistor는 전류의 양을 조절할 수 있다는 뜻이다.  
 
TR은 npn ![npn]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/transistor-01.gif) 형과 pnp ![pnp]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/transistor-02.gif) 형 두가지가 있다.  

![Inside transistor]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/transistor-03.jpg){: .full}  

회로에 직접 그려보면

![Transistor circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/transistor-04.jpg){: .full} 

npn형 TR의 Trans-Resistor의 기본 형태는 위의 그림과 같다.  

Transistor의 symbol를 살펴보면, B는 base, E는 Emitter, C는 Collector라고 부른다.   
B는 Transistor가 동작하게 하는 Switch역할이고, B에 의해 Switch가 ON되면 C와 E사이에 전류가 흐르게 됩니다.  
(화살표는 여러가지 의미를 가지고 있지만, 전류가 흐르는 방향이라고 보면 된다).
 
**Trans**-Resistor 의 의미를 다시 생각해보자.  
Switch를 더 세게 누르면 C와 E사이에 전류가 더 많이 흐르고, Switch를 덜 세게 누르면 C와 E사이의 전류가 덜 흐른다고 가정해볼때,  
B를 얼마나 세게 누르느냐에 따라 C와 E사이에 흐르는 전류량도 바뀌게 된다.  

결과적으로 저항값이 변한다고 봐도 무방하다.  

Switch를 세게 누른다는 건 B와 E사이에 전압을 얼마나 세게 주느냐로 생각하면 된다.  
TR은 평소에는 전류가 흐르지 못하다가 화살표 방향으로 전압을 넣어주어, 전압의 양을 얼마나 넣어줄꺼냐에 따라 C와 E사이의 전류량을 결정할 수 있다.  

가장 중요한 한가지는 B에 넣어주는 전압(전류)량의 미묘한 변화에도 저항값이 많이 바뀐다는 것이다.  
결국 EC간의 전류 값도 많이 변한다는 뜻이다.
 
Switch (base)에 넣어주는 전압량(전류량)에 따라 포화영역, 활성영역, 차단영역이 생긴다.  
CE간에 전류가 B의 작은 입력에 대하여, 급격하게 변해주는 영역을 **활성영역**, B에 흐르는 전압(전류)가 너무 낮아서 CE사이에 전류가 흐르지 못하는 영역을 **차단영역**, 그리고, 마지막으로 B에 흐르는 전압(전류)가 너무 높아서 CE사이의 전류가 더이상 흐르지 못하는 영역을 **포화영역**이라고 부른다.  

TR의 주요 기능 둘은 **증폭기능**과 **Switching기능**이다. Switching기능은 Digital 신호 - 0과 1로만 이루어진 - 영역에서 사용되는 ON/OFF기능으로서 아예 흐르지 않거나, 흐르는 두가지 상태만을 표현하면 되기 때문에, **차단영역**과, **포화영역**을 이용하여,
ON/OFF를 표현한다. (B의 switch성질을 이용해서 다른 chip의 전원을 on/off하여 그 chip의 동작을 on/off 할 수 있다).  

증폭기능 즉, Amplifier는 Trans-Resistor의 의미 그대로인 **활성영역**에서 이용할 수 있다. 결국 증폭기능이란 아주 작은 전압 신호를 B에 흘려주면 CE간에 전류가 더 큰 폭으로 빠르게 움직이는 원리를 이용하는 것이다.  

![Amplifying]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/transistor-05.jpg){: .full} 

* * *
### Transistor의 증폭회로
TR의 증폭회로는 3종류가 있다. 3개의 pin중 어느 핀이 접지되었는가에 따라 **Emitter 접지**회로,**Collector 접지**회로, **Base 접지**회로로 구분 할 수 있다.  

Emitter 접지의 경우 **전류 & 전압증폭**이 되고 입력과 출력은 **역상**이다.  
Emitter 접지는 전압,전류증폭이 모두 가능하므로 일반적인 증폭기에 가장 많이 애용되고 있다.  
TR를 스위치 형태로 사용할 때 도, emitter를 접지시켜 collector에 전원을 달고, base로 ON/OFF를 하는 구조다. 

Collector 접지는 **전류증폭**만 되고 입력과 출력은 **동상**, 주로 최종단에서 전류 증폭용 또는 임피던스 매칭용으로 사용한다.  

Base 접지는 **전압증폭**만 되고 입력과 출력은 **동상**이다. 주파수 특성이 좋아 고주파에 많이 애용된다.  

<sub>
출처: EMBEDDED RECIPES(corner book),  
친절한 임베디드 시스템 개발자 되기 강좌 - Transistor 1% ([링크](http://recipes.egloos.com/4971003))
</sub>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>