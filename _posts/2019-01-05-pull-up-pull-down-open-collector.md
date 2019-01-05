---
title: 6\. Pull up, Pull down 그리고 Open collector
categories:
    - Embedded Recipes
tags:
    - Pull up resistor
    - Pull down resistor
    - Open collector
toc: true 
toc_label: "Contents" 
toc_icon: "cog"
toc_sticky: true
---
## Low & High active
보통 Digital System의 pin에 인가되는 값은 Logic 0일 때 동작 상태, 또는 Logic 1일 때 동작 상태로 사용된다.  

어느 상태이건 만드는 사람 마음대로 동작상태를 정하기 나름이지만 일단 동작 상태를 Active라고 부르며, 이때 Logic 0 Active인 pin을 **Low Active**라고 부르고, Logic 1 Active인 pin을 **High Active**라고 부른다.  

Low Active의 예를 들어, 만일 CS (Chip Select)라는 pin이 Low Active일 때는 그것을 명확히 하기 위하여, /, _N, -, * 등을 붙여서 **CS/, CS_N, CS, CS\*** 등으로 표기하며, **CS bar** 라고 읽는다.  

만약에 누군가가 "CS bar 가 동작을 잘 안해" 라고 말한다면 CS라는 pin이 전압 LOW 상태에서 동작하는데 그게 잘 안되는구나 라고 이해하면 된다.  
High Active 라는 건 그 반대이며, 아무것도 붙이지 않는다.  

Low Active의 경우에는 Low가 되었을 때만 동작이 되도록 확실하게 하기 위하여 평소 Default 값을 High로 만들어 놓고, Active되었을 때만 Low로 만들어주는 것이 가장 확실한 방법일 것이다.  

반대로 High Active는 평소에 Low상태로 만들어 주었다가, Active 되었을 때만 3V High로 만들면 되는 것이다.  

다음은 Pull up 저항의 사용 예이다.  

![Pull up 1]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/pull-up-pull-down-open-collector-01.jpg){: .full}  

Digital Chip은 R에 비해 많이 큰 저항일 때, Low Active case에서의 Pull up이라는 것은 Digital Chip의 입장에서 ①번 Switch On 상태에서는 Digital chip input에 GND 즉 0V의 전압이 가해지며, ②번 Switch Off상태에서는 Digital chip input에 3V에 가까운 전압이 가해지게 된다는 뜻이다.  

이는 즉, Swtich가 On될때는 Low 값이 Digital Chip에 인가됨을 의미한다. 만일 이 Digital chip은 input이 0일 때 동작가능하다고 한다면, 평소에는 3V의 input을 유지할 수 있는 그림과 같은 회로 구성이 가장 타당하다.

반대로 High Active Pull down이라는건 Pull up과 완전 반대로 평상시에는 Low를 유지하다가, Switch ON을 시켰을 때, High를 Digital chip에 인가 시켜주는 것을 의미한다. ①은 switch on이며, ON을 시켰을 경우에는 확실하게 High 3V가 인가되며, Off시켰을 경우에는 Digital Chip에 0V가 인가된다.  

![Pull up 2]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/pull-up-pull-down-open-collector-02.jpg){: .full}  

이렇듯, Pull up & down은 Digital 신호의 기본적인 Default Level을 무엇으로 둘 것이냐의 문제인데, 원래 Ideal한 것으로 따지면 필요 없는 회로일 것이다.  

하지만 real world 에서는 조금 더 reliable하게 확실한 default 값을 보장하기 위해서 pull up이나 pull down이 회로 level에서 필요하다.
예를 들어 High Active로 동작하는 Digital chip의 경우에 system이 정전기를 맞았거나, 사람이 칩을 만졌을 때, 외부 요인에 의하여 순간적으로 그때의 input이 High가 되어버린다면 Digital chip은 의도와 상관없이 동작하게 되는 경우가 있기 때문이다.  

Transistor를 이용해서 pull up system을 구현하면,  

![Pull up with TR]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/pull-up-pull-down-open-collector-03.jpg){: .full}

일단 Master의 output pin이 High를 주느냐, Low를 주느냐에 따라 Slave가 동작을 하게 되는데, 일단 Master는 Slave를 동작시키고 싶을 때, High를 주고, Slave를 동작시키지 않을 때는 Low를 준다고 가정해보자(low active slave).  

회로를 분석해 보면 \\(V_{cc}\\)는 Pull up을 위한 전원이고, \\(R_{c}\\)는 Pull up을 위한 저항이다. Transistor는 Switch역할을 한다. \\(R_{1}\\)은 보통 Master chip의 output이 Logic 0일때, 0V를 제대로 내어 줘야 되는데 약간의 전압을 내보낼 때도 있다.  

이를 대비하여, 만일 TR이 ON 될 만큼의 전압이하에서는 확실하게 0V로 만들어 주기 위하여 R1을 달아 Base로 전류가 흐르지 못하게 만들어 준다. 보통 이런식으로 switch로 사용하는 Transistor는 B와 E를 저항으로 직접 연결된 Transistor를 한개의 소자로 해서 팔기도 한다.  

Master가 0을 주면 Transistor는 off상태이며, Slave로 들어가는 input은 Pull up되어 High가 된다. 따라서 Slave 가 동작을 하지 않는다. 반대로 Master가 1을 주면 Transistor는 On이 되어, Slave로 들어가는 input은 0V를 넣어주어 Slave chip이 동작하도록 한다.  

## Open collector

앞서 설명한 Switch가 Master chip에 아예 들어가 있는 경우까지 scope를 extend 해서 볼 수 있다. 이런 Switch가 Master chip 내부에 아예 들어가 있는 경우를 **Open collector** 라고 부르는데, 이런 구조는 Collector가 output으로 나와 있으며 아무것도 연결되어 있지 않아 Open Collector라고 부르며, 
Open Collector는 다음 그림과 같이 여러개의 Master가 한개의 Slave에 연결될 때 아주 유리한 구조이다.  

![OR instruction circuit]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/pull-up-pull-down-open-collector-04.jpg){: .full}

명령1 OR 명령2 회로(low active임에 유의 할 것)  

각 Master의 명령 input앞에 달려 있는 
![inverter]({{ site.url }}{{ site.baseurl }}/assets/images/embedded-recipes-book-images/pull-up-pull-down-open-collector-05.jpg)는 inverter로서 input의 상태를 반전시킨다. 
위의 예시와 같이 실제 master가 주는 신호와 반대의 신호가 slave로 흘러가기 떄문에, Master가 Low를 주었을 때, Slave가 Low를 받게 하려면 inverter를 달면 편하다.  

하나 이상의 여러개의 Master는 Low Active인 Slave의 Out (Slave입장에서는 input) 에 Low를 주기 위하여, High를 주게 되는데, 위의 표와 마찬가지로 평소에는 High Pull up상태를 유지하다가 둘중에 하나만 Low가 되면 Slave에는 Low가 전달되어 Slave가 동작하도록 한다. 
결국에는 Low와 High가 같이 공통 버스에 인가 되어도 서로 부딪치지 않고 Low가 된다.  

보통 chip과 chip사이에 이런 공통 버스로 연결되어 있는 경우 한 chip에서는 High, 다른 한 chip에서는 Low를 한꺼번에 공통버스에 올려놓았을 때 그 두 chip들 사이에 저항이 없다면 순간 무한 전류가 흘러버려 system이 타 버리게 되지만, 이런 open collector의 경우에는 서로 달라도 상관 없는 구조다. 
일종의 Low Active 버스라고도 볼 수 있고, 다르게 표현 하면 예를 들어 Low OR로서 어느 하나만 Low가 되면 Slave 동작 이 되기 때문에, 여러개의 Interrupt를 하나의 Interrupt로 인식할 때 (Slave가 Main Processor 따위의 경우) 유리하다.  

Open Collector구조는 하나의 Master와 하나의 Slave에서도 사용 가능하지만, 여러개의 Master를 Slave에 붙여서, 전원 하나와, 저항 하나로 회로를 간단하게 만들 수 있는 장점이 있다.  

보통 Digital chip의 pin description을 보면 open collector인 pin은 open collector라고 쓰여 있어, 그것을 고려하여 회로를 구성할 수록 더욱 더 진가를 발휘한다.
 
이런 구조는 전문용어로 **Wired OR** 라고 부르기도 한다.  

여러개의 Master 출력을 한번에 묶을 수 있으니까, 회로도 간단해 지고, 또한 서로 다른 Master의 출력을 Slave의 정격 규격 - 전류나 전압 -을 Pull up에 의하여 쉽게 맞출 수가 있어 편리하게 이용된다.

<sub>
출처: EMBEDDED RECIPES(corner book),  
친절한 임베디드 시스템 개발자 되기 강좌 - Pull up, Pull down 그리고 Open collector ([링크](http://recipes.egloos.com/4971029))
</sub>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>