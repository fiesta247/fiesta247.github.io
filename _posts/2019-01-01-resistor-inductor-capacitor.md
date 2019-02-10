---
title: 03\. 초간단 회로이론 R(저항), L(인덕터), C(캐패시터)
categories:
    - Embedded Recipes
tags:
    - Resistor
    - Inductor
    - Capacitor
toc: true 
toc_label: "Contents" 
toc_icon: "cog"
toc_sticky: true
---
## 저항(Resistor)  
저항은 ![resistor]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/resistor-inductor-capacitor-01.gif) ← 이렇게 표시한다.  
저항의 양단에 전압이 \\(V\\) 로 걸렸을 때 저항 \\(R\\) 에 흐르는 전류 \\(I\\) 의 양은 옴의 법칙 (\\(V=IR\\)) 에 의하여, \\(I=\frac{V}{R}\\) 이다.  
정해진 전압에 대하여, \\(R\\) 의 크기를 적당히 바꾸면 우리가 원하는 \\(I\\) 의 크기를 \\(R\\) 에 흘러가게 만들 수 있다.  
저항의 크기가 크면 작은 전류가, 저항의 크기가 작으면 큰 전류가 흐른다.   
즉 저항은 **회로의 특정부분에 흐르는 전류의 양을 제한 할 수 있다**.  
일반적으로는 전류는 저항이 가장 **낮은** 경로를 찾아가는 성질이 있다.    
저항의 단위는 \\(\Omega\\) 으로 그리고, **옴**이라고 읽는다.  

한 가지 전류가 저항을 지나고 나면 그 만큼의 전압이 원래 전압에서 빠져나가게 된다. 이것이 전압을 **potential**이라고 부르는 이유이다. 위치 에너지와 똑같이 어떤 전압과 전압 사이에 전위차(전압차)가 있고, 전압은 그 사이에 저항이 있으면(저항 \\(\times\\) 전류)만큼의 에너지를 소비한다.  

직렬과 병렬 연결에 대해서 생각해 본다면 저항의 크기가 동일하다고 할 때, 직렬의 경우, 전류가 흘러 가는데 저항이 계속 길게 늘어져 있는 것과 같기 때문에 전체 저항의 크기는 커진다.  

병렬의 경우, 전류가 흘러가는데 길이는 그다지 문제가 되지않고 전류가 갈 수 있는 길이 많아 진 것과 같다. 따라서 전체 저항의 크기는 작아진다.  

캐패시터와 인덕터에 대해서 첨언을 하고 시작한다면, 캐패시터와 인덕터는 주파수를 가진 전압, 전류(**교류** 전압, 전류)입장에서 보았을 때 주파수에 따라 저항값이 다르게 보인다.  

캐패시터의 경우에는 높은 주파수의 **전압** 일수록 저항을 못느끼고, 인덕터의 경우에는 높은 주파수의 **전류** 일수록 저항을 더 크게 느낀다(Capacitor는 **전기**장에 의한 효과가 major하기 때문에 전압과 관련 되고, 인덕터의 경우는 **자기**장에 의한 효과가 major하니까 전류에 관련 된 것이다).  

## 캐패시터(Capacitor)  
캐패시터는 ![capacitor]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/resistor-inductor-capacitor-02.gif) ← 이렇게 표시한다.  
앞서 말했듯이 높은 주파수 교류전압 일수록 저항을 못느낀다. 따라서 캐패시터를 통해서 교류성분은 통과, 직류성분(주파수가 0)은 저항이 크니까 통과 하지 못한다.  
이 것을 수식으로 나타내면, \\[\frac{dV}{dt} = \frac{I}{C}\\] 이렇게 표현 할 수 있다. 전압의 시간에 따른 변화율이 클수록 전류를 더 잘 통과시키며, 저항이 작다. 또 어떤 정해진 주파수에서 보면 C값이 크면 클수록 저항이 적게 느껴진다. \\(C\\)는 캐패시터 용량으로서 상수이다.  

결과적으로, 커패시터를 일정한 전류를 흘리기 위한 주파수 성분을 가진 전압에 대한 **저항**이라고 보면 된다. 일정한 전류를 흘리면서도 전압에 대해서는 낮은 주파수 성분의 전압은 통과를 못하게 한다. 캐패시터는 이렇게 DC성분과 AC성분을 분리해 내는 능력을 가지고 있다. AC만 통과 시킨다. 결국 \\(C\\) 값이 클수록 전류는 많이 흐를 수 있다.  
 
교류전압만 통과시키는 역할을 하기 때문에 DC block, bypass cap 이라고도 부른다. 미리 말하면, cap은 전류를 충전했다가 방전하는 성질도 있는데, 이는 급격한 전압의 변화를 막는다는 뜻이다.  

흔히 Hardware Engineer가 말하는 Tantal (탄탈)이라는 것도 용량이 큰 (\\(C\\)가 큰) 캐패시터이다. 캐패시터의 단위는 \\(F\\)라고 쓰고, 패럿이라고 읽는다. 크기는 \\(nF\\)에서부터 \\(F\\)까지 다양하다.

## 인덕터(Inductor)  
마지막으로, 인덕터는 ![inductor]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/resistor-inductor-capacitor-03.gif) ← 이렇게 표시한다.  
인덕터의 역할은 전류가 변화하지 못하도록 한다.  
앞서 말했듯이, 인덕터는 교류성분의 전류가 쳐다보면낮은 주파수의 전류일수록 저항을 못느낀다.  
이것을 수식으로 나타내면 \\[V = L \frac{dI}{dt}\\] 라고 쓸 수 있다.  
수식에서 볼 수 있듯 결국 저주파의 전류만이 통과 할 수 있다. 이 말은 즉, 급격한 신호의 흐름을 막는다는 뜻이다.  
정해진 주파수에서 L이 크면 클 수록 전류가 작아지며, 전류의 시간에 대한 변동을 전압이라는 형태로 품고 있다.  
이런걸 캐패시터와 반대로 AC blocking, choke라고도 한다.  
\\(C\\)와는 반대로 \\(L\\)의 경우 \\(L\\)값이 커지면 전류가 더 흐르지 못한다.  

작은 크기의 고주파 흡수용으로 사용되는 인덕터는 Bead (비드)라고도 불리는데, 약간 원리는 틀리지만, 어차피 고주파 흡수용으로 사용하는 건 매 한가지다. 인덕터의 단위는 \\(H\\)라고 쓰고 헨리라고 읽는다.

* * * 
정리하면, 어떤 원하는 정해진 전압에 대해서 전류량을 정할 수 있는데,

    R 의 경우  R 이 클수록 전류를 더 조금 흐르게 할 수 있고,
    C 의 경우  C 가 작을 수록  전류는 더 조금 흐르게 할 수 있고,
    L 의 경우  L 이 클수록 전류는 더 조금 흐르게 한다.

주파수 측면에서 바라보면 정해진 RLC값에서

    R 은 주파수를 타지 않고,
    C 는 높은 주파수 일수록 저항이 작고, (전류가 더 많이 흐르고)
    L 은 높은 주파수 일수록 저항이 크다. (전류가 흐르기 어렵다)

* * *

### Impedance?  
위에서는 이해하기 편하게 저항이라고 통일해서 기술했지만, 교류로 넘어가면 impedance로 기술하는것이 맞다. 저항은 크기 값만 표현하는 것이고, 교류로 넘어가게 되면 전류의 흐름을 방해하는 값이 교류 전압의 진동수에 의존하게 되어 위상값 또한 가지게 되기 떄문에 복소수로 표현해야한다. Impedance는 저항을 복소수로 표현하는 방법인데, 이것에 대해 깊게 다루지는 않을 것이다.  

### Open? Short?
회로를 보다 보면 open이나 short라는 말이 자주 나오는데, open은 말 그대로 연결이되어 있지 않다는 말이고, short라는 말은 연결되어 있다는 말이다.  

### Filter
\\(L\\)은 저주파를 통과, \\(C\\)는 고주파를 통과 시키기 때문에 Noise를 제거할 때 filter로 많이 쓰인다. 예를 들면, \\(L\\)을 달아놓으면 저주파만 통과하고, \\(C\\)를 달아 놓으면 고주파만 빼낼 수 있다.

### Condenser and Capacitor
"전기회로에서 \\(C\\)로 표현되는 전하를 축적하는 소자를 흔히 콘덴서 (condenser) 또는 캐패시터 (Capacitor)라고 부른다.  
학술적으로 순수하게 정전용량 (Capacitance)만을 가지는 이상적인 소자를 **캐패시터**라고 부르고,  
등가저항이나 등가 인덕턴스까지 고려한 실제의 소재를 **콘덴서**라고 부르는 경향이 있다고 합니다.  
대부분의 회로 해석시에 모든 영문원서에서는 **캐패시터**라는 용어를 사용하며, 그 이유로는 이상적인 소자로 해석하기 때문이다.  

![condensor and capacitor]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/resistor-inductor-capacitor-04.jpg){: .full}  

### 저항도 신호를 바꿀 수 있다
저항도 마찬가지로 전자가 뚫고 지나가기 힘든 통로이므로 진행속도가 느려져 실제 신호는 늘어지게 된다.

### 0옴 저항을 쓰는 이유
첫번째 이유로는 AC용 ground와 DC용 ground를 같은 전위로 만들어주기 위해 사용한다. 
보통 AC용 ground와 DC용 ground를 분리해서 만든다. 그 이유는 AC의 노이즈가 DC ground를 흔들리게 할 수 있기 때문이다. 그런데, 두개의 절대 전위는 같아야 하니까, 두개를 연결 해줘야한다. 그럴 때 0옴을 사용한다. 그러면, 두개의 ground를 따로 만들었지만, 전위는 같게 만들 수 있다.  

두번째로는 회로를 꾸밀 때 option으로 Hardware를 꾸밀 때 0옴을 달기도 한다.  
예를 들면, 어떤 회로가 필요해서 달긴 했는데, 요놈을 잘 보니까, option으로 쓸 수도 있고, 아닐 수도 있고하는 경우가 발생한다. 그럴 때 0옴을 달아놓고 떼었다 붙였다 해서 flexible하게 회로를 꾸밀때도 사용한다.  
어쩔 때는 특정 관심 pin에 0옴을 달아서 jumper (측정용 라인) 대신으로 사용할 때도 있다.  

PCB 에 간혹 테스트 포인터(TP)가 있다. 이것이 0옴저항을 달아서 점퍼 대신에 넣는것이다. Board에 사용되는 chip들은 ball type이 많아서 찍어볼 수 있는 다리가 나와있지 않다. 그러다보니 테스트 및 측정 하기가 어렵다. 그래서 중요한 pin에는 0옴을 달아서 board위에 나올 수 있도록 한다.

<sub>
출처: EMBEDDED RECIPES(corner book),  
친절한 임베디드 시스템 개발자 되기 강좌 - 초간단 회로이론 R (저항) L (인덕터) C (캐패시터) ([링크](http://recipes.egloos.com/4968668))
</sub>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>