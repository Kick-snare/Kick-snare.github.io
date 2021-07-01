---
layout: post
title: 극한의 단타충
comments: true
categories: [Project]

# Insight
# Project
# Retrospect
# PS
# LogicDesign

---

# Extreme daytrader 극한의 단타충
### 소개 영상
<iframe width="560" height="315" src="https://www.youtube.com/embed/AU-Lsnx2Pcw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<img src="https://raw.githubusercontent.com/Kick-snare/Extreme-DayTrader/6efc0c65e08a64a9cab82b73d59adc7766a93c17/public/images/logo.svg" style="width : 70%;"/>  

Service for user who addicted for day trading.  
provide real-time price fluctuation and flow for variety of Cryptocurrency.


![picture 2](https://user-images.githubusercontent.com/46425142/120894949-d7349780-c655-11eb-9c43-0f9ce56386fe.png)  


프로젝트 **극한의 단타충**은 코인 시장에서 (초)단타매매를 즐겨하는 사용자들을 위한 코인 거래소의 오픈 API를 이용하여 정보를 제공하는 서비스입니다.

가격 변동성이 커서 투자에 위험한 코인시장에서는 시시때떄로 암호화폐 차트와 숫자를 들여다 봐야합니다. 이 불편함을  해결하기 위해 시인성 좋은 시각적, 그리고 반복적인 청각적 정보로 쉽게 정보를 파악할 수 있도록 해줍니다.

코인의 실시간 가격 변동과 거래량, 그리고 차트 데이터를 그래프로 볼 수 있는 서비스 를 제공합니다. 실시간 정보를 토대로 코인을 매수 할 수 있으며 그에 따른 수익률을 텍스트로 표시하고 파악하기 쉽게 색상으로 구분합니다. 

바리오미터를 차트상에서 구현하여 반복적인 신호음을 소리로 출력하며 피치의 높낮이의 따라 상황을 판단할 수 있습니다. 

가격 정보 외에도 다른 코인의 가격이나, 종목과 관련된 뉴스들을 제공하여 사용자에게 관련정보를 제공합니다.

<br/>

### Installation Process

* **Node.JS 14.16.1 LTS** is required  
  
```
# Repository Clone
git clone https://github.com/Kick-snare/Extreme-DayTrader.git

# Install packages
cd Extreme-Daytrader
npm install

# Express Local Server Start
npm test

# http://localhost:3000
```

### Technique Used

|Node.js|Express.js|
|:---:|:---:|
|<a href="https://nodejs.org/"><img src="https://nodejs.org/static/images/logos/nodejs-new-pantone-black.svg" height="50px"></a>|<a href="https://expressjs.com"><img src="https://i.cloudup.com/zfY6lL7eFa-3000x3000.png" height="50px"></a>|

|HTML5|CSS3|Javascript|Highchart|Scss|
|:---:|:---:|:---:|:---:|:---:|
|<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/21/Devicon-html5-plain-wordmark.svg/640px-Devicon-html5-plain-wordmark.svg.png" height="55px">|<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/CSS3_logo_and_wordmark.svg/640px-CSS3_logo_and_wordmark.svg.png" height="55px">|<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Unofficial_JavaScript_logo_2.svg/1200px-Unofficial_JavaScript_logo_2.svg.png" height="50px">|<a href="https://www.highcharts.com"><img src="https://www.tangunsoft.com/storage/image/product/category/1589364597highcharts.png" height="50px"></a>|<a href="https://sass-lang.com"><img src="https://miro.medium.com/max/512/1*9U1toerFxB8aiFRreLxEUQ.png" height="55px"></a>|


## 후기
---

전공기초 중 **인터넷과 웹기초**라는 전공기초 수업에서 미드텀 대체로 api 쓰는 웹사이트 하나를 프로젝트로 만들래서 만들었다.

중간칠 때 쯔음에 착수 및 계획 보고서를 작성하였기 때문에, 시간이 많아 뭘 할지 한참 고민하였는데, 예전부터 생각하던 재미있는 아이디어를 사용하기로 했다. 그건 variometer와 같은 신호 출력을 암호화폐 차트 그래프에 적용하여 들려주는 서비스였다. 원래는 경험 기반으로 주식으로 할랬는데 코인이 24시간이라 더 재밌을 것 같아서 돌렸다.

바리오미터는 수직속도측정계인데 아래 영상과 같이 수직 속도에 따라 신호음을 다르게 준다.
<iframe width="560" height="315" src="https://www.youtube.com/embed/XLIa_OXW3DQ?start=362" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

주식 단타치다보면 밥먹거나 씻기도 에매한 경우가 있는데 그때 쓰면 재밌을거 같아서 만들기로 했다.

이번 프로젝트를 만들면서 node-express를 처음 써봤는데 로컬 서버에서 라우팅과 api request정도만 구현하면 되는 수준이라 그다지 어렵지 않았다. 언어도 js기반이다 보니 친숙해서 금방 익힌 것 같다.

만들다 보니 이것저것 dependency와 라이브러리등을 추가해서 만들었는데 나중에 조교 컴퓨터에서 안돌아가서 애를 먹었다. 제출하고 채점하는 기간사이에 node 버전 업데이트에 따라 sass가 버전업을 하였는데, 이를 반영해주지 않아 실행이 되지 않았고 직접 가서 업데이트 해야했다.

하다보니 재밌어서 디테일하게 만들었는데 다른 수강생 평균을 보면 학점만 노리는거라면 굳이 많이 시간투자 할 필요는 없는 듯하다.

[[깃헙레포링크]](https://github.com/Kick-snare/Extreme-DayTrader)

끝

