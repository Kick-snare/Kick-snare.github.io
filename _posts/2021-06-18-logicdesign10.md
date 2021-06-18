---
layout: post
title: 논리회로설계 [10] Register Circuit of Operations
comments: true
categories: [LogicDesign]

# Insight
# Project
# Retrospect
# PS
# LogicDesign

---

*본 포스팅은 Logic and Computer Design Fundementals (Pearson, 2013)의 내용을 다루고 있습니다.*

<br>

지난 포스팅까지 레지스터와 레지스터 전달에 대하여 알아보았다. 이번시간에는 심볼과 연산자 표기, 그리고 여러가지 연산을 수행하는 레지스터 회로를 살펴보자.

<br>

## Symbols for Register Transfers
---
### Basic Symbol
![picture 58](../images/dd1c1f1fa7fe5142c261a3ac2df0f6180688f6256060449de3206b6577292b3a.png)
*Basic Symbols for Register Transfers*

레지스터 전달을 심볼로서 표기할 때는 여러가지 기호들이 사용된다. 보통 알파벳 레터와 숫자로 레지스터를 표기하고, 그 둘을 잇는 화살표로 전달자와 피전달자를 구분한다.

만약 comma로 쓰여있다면 동시에 수행, 즉 같은 clock cycle에 같이 연산되는 전달이다. []의 경우 메모리를 참조한다는 뜻이다.

### Arithmetic
![picture 59](../images/ed3e297a7e2878e6bf52a997af413d015f9cf4f7c1ebe38555adb5dff49ceb89.png)  
위와 같은 arithmetic 연산들도 수행할 수 있겠다.

`R0 ← R1 + R2`와 같이 두개의 레지스터를 더하여 다른 레지스터에 전달하는 경우 adder와 같은 조합회로를 거쳐서 전달된다.

### Logic 

![picture 60](../images/0030c0f4907be6abc40c7f8eacf9335e785d02399f69befdc5a2ea5c3c0d4161.png)  
논리 연산도 가능하다.

### Shift

![picture 61](../images/c46f21b7ec8360f4a35f8ec0f7b1461e4dbde82245a4a5cbd10896e7ec6ee680.png)  
당연히 Shift 연산도 가능하다.

## Various Register Transfer Circuits
---
이제 레지스터 전달로 연산을 수행하는 여러가지 회로와 구현방법에 관해 살펴보자.

### Add & Subtract Microoperation

레지스터 전달 회로로 가감산기를 구현할 수 있다.

![picture 62](../images/6977b14b3203b3d11b0d4412fb2d0796fdb891c3a5b342830cff4ec7ab5a741d.png)  

구조를 보면 Selector 입력 X에 의해 R1에 R2를 더하거나, 빼는 micro 연산을 수행한다.

K1 로드 입력에 의해 컨트롤 되며, carry를 통해 오버플로우를 체크하는 V와 C를 저장하는 레지스터가 존재한다.

### Register Selecting

두 개의 레지스터 `R1`과 `R2` 중 한 개를 골라 또 다른 레지스터 `R0`에 전달하는 회로를 만든다고 하자.  
아래와 같이 구현할 수 있다.
![picture 63](../images/bdeb704f7cbf9efe2a6306505626bf02f9b467b69c92f25c5a2dd2d6868c6f7a.png)  

2가지 Load 입력 K1 과 K2를 이용하여,
- **K1 = 1** 일때 `R0 ← R1`
- **K2 = 1** 일때 `R0 ← R2`

4비트의 데이터를 굳이 다이어그램에 다 표기할 필요는 없다.

![picture 64](../images/63bd959746945a542367e2ec41fe0a7b0d0fd0f3e90d467156ec00978ce46fa3.png)  
위와 같이 vector로 묶어 나타내면 간단하고 알아보기 쉽다.

### 4-Bit Shift Register

Shift 연산을 수행하는 레지스터 회로를 만들어 볼 수도 있겠다.
![picture 65](../images/8d0fe698cbc4a4e33b1602c55eebcb63aa54d28c914693364edc700308491e88.png)  

4개의 flip flop이 직렬적으로 연결되어있다. 각각 한 비트라고 하면 1 clock cycle당 각 레지스터의 오른쪽으로 transfer 되면서 Shift연산이 일어난다. 우측으로 shift 되므로 Right Shift 이다.

![picture 66](../images/203d2e31659b2161cabb025597096f7d4f5fa732f2623491d4f011598030afbf.png)  
심볼화하여 위와같이 간단하게 나타낼 수 있겠다.

### 4-Bit Shift Register with Parallel Load
![picture 67](../images/25844ed60895a4fce9b788eaab86ed865a94cfc09618348da6063d330ad80856.png)  
같은 4-Bit Shift 레지스터이지만 parallel load가 가능한 회로이다.

![picture 68](../images/8b8359b9a5a2cb09e55782ce5a8d873ee7df721b9e81b47b39b4022d3a03acf0.png)  

- Shift 0  Load 0 이면 상태를 유지
- Shift 0  Load 1 이면 입력 D를 로드
- Shift 1  Load x 이면 Shift left

레지스터로 들어가는 값은 `shift * Q(i-1) + ^shift * load * D(i) + ^shift * ^load * Q(i)` 로 나타낼 수 있다.

### Bidirectional Shift Register with Parallel Load

![picture 69](../images/2588e7a0976f3658da5af649a9d2d85bf8d7467e0e626b045da9418730fb8ce2.png)  
위의 3가지 행동을 수행할 수 있는 Shift 레지스터와 달리 위 그림의 회로는 left shift와 right shift 모두 연산 가능한 bidirectional 한 레지스터이다.

![picture 70](../images/9d432f9a825f36cab7ef2169b0bd1a66740054a4a4905f43cddcd00856abdcc4.png)  

Selector 입력에 따라 4가지 연산(LR shift, hold, load)중 한가지를 연산함으로 각 플립 플롭에 4to1 MUX 를 이용한다. 그림에서는 가운데 레지스터만의 mx를 표시하였다.
![picture 71](../images/34c7fbd5b0d17f2fc38943bb83cb7e0ea70b3a1f1d224822c22e6d4d3b9fdab0.png)  
위와 같이 심볼화하여 나타낸다.

---
<br>

이번 포스팅에서는 레지스터 전달을 위한 심볼들과, 여러가지 종류의 레지스터 회로에 대해 알아보았다.  
다음 포스팅에서는 입력이 없는 레지스터 회로 Counter에 대해 알아보도록 하겠다.
<br>

**[[Logic Design - 11]](../2021-06/logicdesign11)에 계속↗**