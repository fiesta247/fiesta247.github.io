---
title: 08\. 논리회로로의 확장
categories:
    - Embedded Recipes
tags:
    - Logic gate
    - AND
    - OR
    - Binary adder
toc: true
toc_label: "Contents"
toc_icon: "cog"
toc_sticky: true
---
Computer Architecture를 이해 하려면, TR과 R,L,C등이 어떻게 위치하고 있는지 알아야 한다.  

디지털 신호를 input으로 넣었을 때, 우리가 원하는 output을 만들어 내려면,  
논리적인 순서에 의해서 data를 manupulation할 필요가 있다.  

이것을 **논리 회로**라고 부른다.  

논리회로로 확장하기 이전에 논리회로가 구현되는가 알아보자.  

## AND
첫번째로 **AND**다.  

AND란, **논리곱**이라고도 부르며, `if (A && B)`와 같은 concept이다.  

두 개가 모두 TRUE (Logic 1)이어야 output이 TRUE. 즉, Logic 1이 되는 것을 의미하며 다음과 같이 표시하고 구현한다.  

![AND]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-01.jpg){: .full}  
<sub>TR을 이용한 회로는 여러가지 구현 방법이 있으나, 가장 간단한 예로 구현한 것이다.<sub>

Transistor로의 구현은 TR두개를 직렬로 연결하고,  
A와 B가 모두 입력되어야 TR이 모두 ON이 되어 output Y로 \\(V_{cc}\\)가 출력된다.  

위 symbol 단위를 **gate**라고 부르며, **AND gate**라고 부른다.  

## OR 
두번째로는 OR다.  

OR란 논리합이라고도 부르고 `if (A||B)`와 같은 의미 이다.  

두개 중 아무거나 하나가 TRUE가 되면 (Logic 1), output이 TURE, 즉, Logic 1이 되는 것을 의미하며, 다음과 같이 표시하고, 구현할 수 있다.  

![OR]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-02.jpg){: .full}  

Transistor로 구현은 TR두개를 병렬로 연결하고 A와 B중 어느 것이라도 1이라면 TR이 ON이 되어 Input \\(V_{cc}\\)가 output Y로 나가는 형태다.  

이 역시 **OR gate**라고 부른다.  

## Inverter
회로를 구성하다 보면, inverter가 필요할 때도 있다.  

inverter는 input을 반전시키는 일을 하며, 표시와 구현은 다음과 같이 한다.  

![Inverter]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-03.jpg){: .full}    

위 그림은 앞서 공부한 [pull up회로](/embedded%20recipes/pull-up-pull-down-open-collector/)의 형태와 매우 흡사한 것을 알 수 있다.  

A가 Logic 1일 때는 Y로 0이 출력되고, 0일 때는 Y로 1이 출력된다.  

* * *

이런식으로 TR을 잘 이용하면, Logic gate들을 만들어 낼 수 있다.  

이런 Logic gate들을 이용해서 Digital Logic 회로를 만들어 내고,  
Logic회로들을 잘 조합하여 CPU를 만들어 낼 수 있다.  

이런 Digital Logic Gate는 AND, OR, Inverter만 있는 것이 아니다.  

![Logic gate simbols]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-04.jpg){: .full}  

우리가 Chip vendor에서 사다가 쓰는 chip들의 내부는 이런 Logic Gate들을 integration해서 특정 목적을 수행하려는 Logic 회로이다.  

근래에는 이런 gate모임들도 VHDL이나 verilog등을 이용해서 Programming 언어로 표현하여, chip을 만들어 낼 수도 있다.  

마치 C언어를 다루 듯, input을 넣으면 어떤 Logic을 통해서 어떤 output이 나오도록 C의 함수처럼 chip을 구현한 후,  
마치 CD 굽듯 특정 chip burner에 넣으면 그런 Chip을 만들어 내는 기술이다  
(이런 chip들을 PLD/ PGA/ FPGA라고 부른다).  

## Logic gate의 응용
이런 Logic gate를 이용해서 무엇을 할 수 있는지에 대해 가장 간단한 예로 *1bit Binary Adder*를 하나 만들어 보면,  
Binary Adder의 진리표는 다음과 같다.  

![Binary adder truth table]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-05.jpg){: .full}  

보다 시피, 1 bit + 1 bit는 2bit가 된다.  

가장 낮은 LSB끼리 더하고 LSB가 둘다 1일 때만 carry 1 이 발생 한다.  

따라서, Binary Adder의 진리표는 다음과 같이 나눌 수 있다.  

![LSB & MSB binary Adder]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-06.jpg){: .full}  

왼쪽 표는 OR랑 비슷하고, 오른쪽 표는 AND그대로 인 것을 알 수 있다.  

그러면, carry는 AND를 이용하고, 왼쪽의 OR는 살짝 수정하면, OR는,  

![OR truth table]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-07.jpg){: .full}  

마지막 LSB진리표에 (2,2)자리인 1+1 자리에 1만 들어가면 OR와 같아진다.  

생각해 보면 이것은 NAND와 같다.  

NAND의 진리표는  

![NAND truth table]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-08.jpg){: .full}  

(2,2) 에 1+1자리만 0이다.  

따라서 두 개를 AND해 버리면 1의 자리만 더하는 <LSB>의 진리표가 나온다.  

이를 모두 합하면, 다음과 같은 논리회로를 만들어 낼 수가 있다.  

![2bit binary adder]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-09.jpg){: .full}  

간단하게 OR하고 NAND를 AND하여, Low LSB 1bit를 만들어내고, 나머지 High MSB 1bit는AND를 해서 만들어 낼 수 있다.  

하지만, OR하고 NAND를 AND해서 만들어 냈는데 보기 보다는 너무 복잡하다고 느낄 수 있다.  

다음 식을 참고하면,  

0 xor 0 = 0, 0 xor 1 = 1, 1 xor 1 = 0  

OR과 NAND를 AND한 것은 XOR(XOR는 두 input이 틀려야 TRUE가 되는 논리회로)과 같다는 걸 알 수 있다.  

XOR의 의미는 carry를 뺀 2진 합이다.  
 
조금더 간단하게 다시 그려보면,  

![simplified 2bit adder]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-10.jpg){: .full}  

위 그림과 같이 간단하게 2bit Adder를 만들어 낼 수 있다.  

이런 input과 원하는 output을 만들어 내기 위하여, Logic 회로를 구성하는  
방법중 하나가 흔히들 말하는 **카르노맵**이다.  

이런 카르노맵을 구사하면 간단하게 input에 대한 원하는 output을 만들어 내는 논리 조합을 만들어 낼 수 있다.  

물론 Macro하게 보면 이렇게 symbol로 간단하게 보고 있지만, 실제로는 저안에 많은 TR들이 들어 있다.  

2bit Adder를 Transistor들의 논리 회로들을 실제로 그림을 그리면 다음과 같이 그릴 수 있다.  
  
![2bit adder transistor logic circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-11.jpg){: .full}  

이런 논리 회로들은 다음과 같은 모양으로 IC라는 집적회로에 집적되기도 한다.  

![2bit adder IC circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-12.jpg){: .full}  

7번 pin과 6번∼ pin에 입력을 넣으면 5번 pin으로 AND output이 나온다.  
또는 3번 pin과 4번 pin에 입력을 넣으면 2번 pin으로 OR output이 나온다.  

이런 논리조합들을 잘 조절 하면 우리가 원하는 output을 만들어내는 회로를 만들어 낼 수 있다.  

Digital Chip set은 다음과 같이 논리회로가 가득차 있는 모양이다.  

![digital chipset]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-13.jpg){: .full}  

* * *

## 전압 notation
Vcc 와 Vee 등의 notation을 많이 사용하였는데, 그 의미를 되짚어 보면, 다음 표와 같다.  

![voltage notation]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/logic-circuit-14.jpg){: .full}  

BJT (Transistor)와 FET사이의 사용하는 notation이 다르다.  

Vcc는 Collector 전원, Vee는 Emitter전원, Vdd는 Drain 전원, Vss는 Source전원이다(FET는 BJT와 약간 다르게 Drain, Source, Gate로 다리가 구성되어 있다).  

요약하면, Vcc, Vdd는 전원으로 연결되고, Vee, Vss는 보통 Gound 단에 연결된다.  

근래에는 FET와 BJT가 혼합되어 사용되어 그 부분이 모호해져, Vcc와 GND로 전원과 GND를 그냥 표시하는 일이 비일비재해졌다.  

통상 BJT를 이용하여 꾸민 회로를 TTL (transistor - transistor Logic)이라고 부르며, FET를 이용하여 꾸민 회로를 CMOS 회로라고 부르는데, BJT나 FET나 하는 역할은 비슷하다.  

BJT와 마찬가지로 입력 전압으로 출력 전류를 제어 하는 역할을 하는데, 결과론적으로는 그렇고 원리는 많이 틀리다.  

FET는 높은 input impedance를 가지고 있어 잔력 사용 효율이 좋으며,  
단점으로는 속도가 느려 단순 스위치로는 적합하나, Linear Amplifier로서는 부적합하다.  

다시 풀어 얘기하면, FET는 Logic쪽에, BJT는 Amplifier쪽에 어울린다는 의미에서 시작하면,  
Logic 쪽에서는 VDD - VSS, Linear Operation쪽에서는 VCC - GND의 notation이 많이 사용된다.  

<sub>
출처: EMBEDDED RECIPES(corner book),
친절한 임베디드 시스템 개발자 되기 강좌 - 논리회로로의 확장 ([링크](http://recipes.egloos.com/4971109))
</sub>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
