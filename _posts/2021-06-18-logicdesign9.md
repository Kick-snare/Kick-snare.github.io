---
layout: post
title: 논리회로설계 [9] Register & Register Transfer
comments: true
categories: [LogicDesign]

#Insight
#Contest
#Retrospect
#PS
#Subject

---

*본 포스팅은 Logic and Computer Design Fundementals (Pearson, 2013)의 내용을 다루고 있습니다.*

<br>

지난 포스팅까지 순차회로와 FSM 설계에 대하여 알아보았다. 이번시간에는 레지스터와 그 Transfer에 대하여 알아보도록 하자.

## Register & Register Transfer
---
레지스터란,  
소프트웨어의 변수 같이 하드웨어에서 임시로 어떠한 데이터를 저장해놓을 수 있는 공간이다. 단순하게 말하자면 n비트를 묶어두는 (저장하는) n개의 D flip-flop으로 이루어진 회로이다.

그렇다면 그 Transfer는 무엇인가?  
레지스터가 소프트웨어에서의 변수라면 레지스터 이전은 변수할당이다. 한 레지스터의 데이터를 특정 시간에 다른 곳으로 옮기는 것이다.


### 4-bit Register

![picture 47](../images/53da566d00c97c7f506143af83f5e40953523f21dd7f82a553a6149ba65e6bd1.png)
*4-Bit Register*

이해를 위해 4 bit 레지스터 회로를 살펴보자.

4개의 D flip-flop으로 이루어져 있으며 4비트 입력과 4비트 출력이 존재한다. 모두 같은 clock에 동기화 되어있고 초기화를 위한 Reset 인풋이 존재한다.

![picture 48](../images/bb3fc85cc8bc07f0e77c4cb62f7fc61ba74509aa336880d40a9a7b5df861a8fa.png)  
마찬가지로 레지스터 역시 심볼로서 간단하게 표현 가능하다. 아예 입력과 출력을 vector로 묶으면 더 간단할 것이다. 그리고 레지스터는 당연히 flip-flop으로 만들어지기 때문에, 당연히 clock이 존재함으로 심볼에서는 생략가능하다.

![picture 49](../images/92f383e161aa64f8faccf73a137e061151cc3109a13a1ff3d298bc8b5441f227.png)  
C 입력은 [이전 포스팅](../2021-04/logicdesign4) 배웠던 Enable 회로의 일종이다. ^Load와 Clock을 OR 게이트로 묶어 받으므로 Load 가 0이면 항상 clock에 1이 들어가고, 1일때 enable 되어 clock이 동기화 된다.

clock pulse에 따른 그래프를 그려보면 아래와 같다.
![picture 50](../images/48630695c92554fc3bca4e43547d627b26f61fef849fb8e82c5dab0978724cd7.png)  
Load가 1일때 clock의 rising edge에서 데이터의 변화가 일어난다는 것을 예측가능하다.

위 그림에서는 사실 latency를 고려하지 않았다. 이로 인하여 회로에 glitch 가 발생할 가능성이 있다. 예를 들면 항상 1을 유지해야하는 신호가 지연시간으로 인해 짧은 시간동안 유지하지 못하고 0 으로 내려갔다가 올라올 수 있다. 그 경우 내려갔다 올라오는 과정에서 의도치 않은 rising edge가 일어나며 Transfer가 일어날 수 있다. 아주 위험한 회로안 것이다.

그러므로 이런식의 레지스터 설계는 **옳지 않다**.

### 4-bit Register with Parallel Load

그렇다면 어떻게 이러한 문제를 해결할 수 있을까. 정답은 입력들을 레지스터 측에서 받아와 MUX로 처리하는 방법이다. 예시 회로를 보자. 
![picture 51](../images/3f7cf475830aa348aef3ecf107a35c432a638c789c979a918dce7b65e465c234.png)  

위 회로에서는 D flip-flop에 들어오는 D 입력과 Load에 추가적인 회로가 연결되어 있다. 

이를 잘 살펴보면 [이전에 배운](../2021-04/logicdesign5) MUX 임을 확인할 수 있다. EN(Load) 가 셀렉터 인풋으로써 새로운 입력 D를 전달할지, 현재 상태 Q를 전달할지 결정하므로, Load되지 않는다면 clock과 관계없이 D값이 전달되지 않고 상태를 유지한다.

![picture 52](../images/a7cf8a7f4523567b9cfa8dde41d021148f2c48842df4052e0b2f72cb7b8de5b4.png)  

이러한 추가적인 회로를 역시 한 레지스터 처럼 심볼화하여 위와 같이 나타낼 수 있다.

이러한 레지스터를 *Register with Parallel Load* 또는 *Loadable Register*이라고 한다.

---

<br>
이번 포스팅에서는 Register 와 Register Transfer에 대하여 알아보았다.  
다음 포스팅에선 복잡한 회로의 설계를 위한 Control Unit과 DataPath에 관하여 알아보도록 하자.
<br>

**[[Logic Design - 9]](../2021-06/logicdesign9)에 계속↗**