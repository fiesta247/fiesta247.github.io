---
title: 7\. RLC와 Transistor 感(감)
categories:
    - Embedded Recipes
tags:
    - Resistor
    - Inductor
    - Capacitor
    - Transistor
    - Decoupling Capacitor
toc: true 
toc_label: "Contents" 
toc_icon: "cog"
toc_sticky: true
---
## Capacitor Example  

![Capacitor example circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/rlc-and-transistor-01.jpg){: .full}  

가장 간단하게, Chip에 3V DC전원을 인가 하기 위한 회로이다.  

이 회로에서 C는 AC인 고주파만 통과시키고, 3V 전원이 인가 될 때, AC성분을 GND로 흘려 Chip에 들어가는 것을 차단하기 위한 Capacitor이다.  

여기에서 AC는 전원에서 발생하는 Noise 등이 있다. 또는 전원이 켜질 때 Transition으로 생기는 Noise따위를 제거 하기 위한 것이다.  

Ripple제거라고도 하는데,이런 작은양의 DC의 흔들림 (AC성분)을 Ripple이라고 부른다. [앞서 살펴본]({{ site.url }}{{ site.baseurl }}/embedded%20recipes/filter/) Low Pass Filter와 같고, 위 회로에서는 \\(C\\) 만 보이지만, \\(+3V_{VCC}\\) 를 거꾸로 따라가 보면, R이 붙어 있을 것이라는 것을 유추할 수 있다.  

## L, C Example  

![L, C example circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/rlc-and-transistor-02.jpg){: .full}  

이 회로에서 \\(+3V_{VCC}\\)가 전원이며, 이 전원이 \\(D_{CHIP}\\)의 \\(VCC_{IN}\\)에 drive되어 D_CHIP이 동작하도록 하는 것 이다.  

이 회로에서 \\(L\\)은 AC에게는 큰 저항, DC에게는 저항 없음과 같고, \\(C\\)는 AC에게는 저항 없음이고, DC에게는 큰 저항과 같다.  

두 소자의 역할은 \\(+3V_{VCC}\\)의 DC성분을 안정적으로 \\(VCC_{IN}\\)에 공급하기 위함이다(Ripple 제거용도).  

|    |\\(C\\)|\\(L\\)|
|----|----|----|
| 저 주파수 | 저항 큼   | 저항 작음 |
| 고 주파수 | 저항 작음  | 저항 큼  |  

\\(L\\) 대신 \\(R\\) 을 사용해도 될 것이라는 의문이 들수 있다.  

하지만, \\(L\\) 을 넣는 경우는 보통 그냥 코일이 아니라, bead라고 부르는 Inductor의 한 종류를 삽입하는데, 이 bead의 특성이 특정 주파수에서 저항의 역할을 톡톡히 하여, 마치 공진기 처럼 특정 주파수를 없애 버리는 역할도 같이 한다.  

결국 \\(R\\) 을 넣으면, 전체적으로 줄어 들긴 하나 특정 주파수를 제거하지는 못한다. 

따라서, \\(L\\) 을 넣으므로서 AC를 전체적으로 죽이면서도 특정 주파수를 없엘 수 있는 장점이 있다.  

이런 회로는 통신회로에 많이 사용되는데, 통신회로중 통신을 하는 carrier주파수에 영향을 없게 하기 위하여, 이런 bead를 삽입해서 그 주파수가 Board에 발생하지 못하도록 한다.  

바로 언급한 두개의 example에서 사용된 \\(C\\)를 바로 Bypass Capacitor 또는 Decoupling Capacitor라고 부른다.  

Bypass Capacitor는 Noise, Ripple성분을 주파수 특성을 이용하여 GND로 통과시켜 버린다는 의미고,또는 Decoupling Capacitor는 Noise, 또는 Ripple성분을 전원공급에서 떼 내어 버린다는 것을 의미한다.  

## USB_CONN, TR, C, Control

![L, C example circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/rlc-and-transistor-03.jpg){: .full}  

이 회로는 chip1에 CONTROL신호를 넣으면 USB_CONN/를 구동하는 회로다.  

다시 말하면,

    ⓐ 다른 어떤 chip으로부터 CONTROL High drive  
    ⓑ CHIP1은 pin 5에 High drive  
    ⓒ TR ON  
    ⓓ USB_CONN/ Low drive로 Active 됨.  

여기에서 R, TR, C는 어떤 용도로 쓰이는 지 확인해 보면,  

Capacitor C는 Control 신호가 CHIP1에 입력될 때, 쓸 데 없는 AC성분이 들어가지 않도록, AC를 GND로 흘려 보내는 역할을 하고,  

R은 USB_CONN/이 Low active 이므로, 평상시 default상태를 High로 만들기 위한 \\(+3V_{VCC}\\)와 함께 Pull up을 하기 위한 것이다.  

## R, TR  

이어서 R, TR의 경우,

![R, TR example circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/rlc-and-transistor-04.jpg){: .full}  

이 회로는 npn형 T1, pnp형 T2 트랜지스터가 맞물려 있으며, input으로는 +INPUT, CONTROL/가 있고, Output이 오른쪽 상단에 OUT port로 나와 있다.  

일단 이 회로는 DC회로이며, CONTROL/에 의해서 control된다. 이 회로는 R1과 +INPUT신호를 이용한 Pull up이다.  

일단 CONTROL/가 high일 때는 T1이 ON되며, 이때 그렇게 되면 +INPUT은 3번 port와 5번 port를 따라 전압을 소진하게 되면서 동시에 T2가 ON 된다.  

5번 port는 T1이 ON이 됨에 의하여 1번 port의 GND에 연결된다. 
그러므로 OUT으로 연결되는 T2가 ON 되었으니까 OUT에 INPUT이 거의 다 걸리게 된다.  

그러면 이번엔 반대 case인 CONTROL/의 신호가 Low인 경우에는 CONTROL이 Low가 되면서 T1이 off가 되고, T2도 덩달아서 off가 된다. 결국, +INPUT신호는 오갈 곳 없어지게 되고, OUT에는 아무 것도 걸리지 않게 된다.  

결국, CONTROL/신호가 LOW일 때 OUTPUT에 아무것도 걸리지 않고, CONTROL/ 신호가 High일 때는 +INPUT신호가 OUT으로 나가게 되는 회로가 된다.  

* * *

![Complex circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/rlc-and-transistor-05.jpg){: .full}  

이런 복잡한 회로도 자세하게 보면 간단하다.  

<sub>
출처: EMBEDDED RECIPES(corner book),  
친절한 임베디드 시스템 개발자 되기 강좌 - RLC와 Transistor 感 ([링크](http://recipes.egloos.com/4971060))
</sub>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>